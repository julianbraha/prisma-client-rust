---
title: rspc Integration
layout: ../../layouts/MainLayout.astro
---

Prisma Client Rust has first-class support for [rspc](https://github.com/oscartbeaumont/rspc),
a server-agnostic router that can automatically generate TypeScript bindings.

The examples use the following schema:

```prisma
model Post {
    id        String   @id @default(cuid())
    title     String

    comments Comment[]
}

model Comment {
    id        String   @id @default(cuid())
    content   String

    post   Post   @relation(fields: [postID], references: [id])
    postID String
}
```

## Setup

When the `rspc` feature is enabled for both `prisma-client-rust` and `prisma-client-rust-cli`,
all data types generated by PCR will implement `rspc::Type`,
and a `From<queries::Error>` implementation is generated for `rspc::Error`.

## Queries

The following is possible when combining PCR and rspc:

```rust
use rspc::Router;

fn main() -> Router {
    Router::<prisma::PrismaClient>::new()
        .query("posts", |db, _: ()| async move {
            let posts = db
                .post()
                .find_many(vec![])
                .exec()
                .await?;

            Ok(posts)
        })
        .build()
}
```

When TypeScript is generated it will look something like this:

```ts
export type Operations = {
    queries: { key: ["posts"], result: Array<Post> }
};

// rspc can export types that aren't even directly used in any operations!
export interface Comment { id: string, content: string, postID: string, post: Post | null }

export interface Post { id: string, title: string, comments: Array<Comment> | null }
```

This also works for [select & include](/select-include):

```rust
use rspc::Router;

fn main() -> Router {
    Router::<prisma::PrismaClient>::new()
        .query("posts", |db, _: ()| async move {
            let posts = db
                .post()
                .find_many(vec![])
                .select(post::select!({
                    id
                    title
                }))
                .exec()
                .await?;

            Ok(posts)
        })
        .build()
}
```

The generated TypeScript will look something like this:

```ts
export type Operations = {
    // select and include types are generated as inline objects
    // rather than having a dedicated type, not even for named selections
    // since TypeScript can just infer return types
    queries: { key: ["posts"], result: Array<{ id: string, title: string}> }
};
```

## Error Handling

Since `rspc::Error` can implement `From<queries::Error>`,
all of Rust's regular error handling conventions are available.

The `?` operator can be used to extract success values and return early if an error is encountered,
automatically converting the Prisma error to an rspc error.
This has the problem of needing to wrap the extracted value in `Ok` before return from a resolver.

Another approach is adding `.map_err(Into::into)` before returning from a resolver.
This causes the Prisma error to be converted to an rspc error while keeping the Result intact,
as demonstrated below:

```rust
use rspc::Router;

fn main() -> Router {
    Router::<prisma::PrismaClient>::new()
        .query("posts", |db, _: ()| async move {
            db
                .post()
                .find_many(vec![])
                .exec()
                .await
                .map_err(Into::into)
        })
        .build()
}
```

For specifics on error handling in rpsc, see [the documentation](https://rspc.otbeaumont.me/server/error-handling/).