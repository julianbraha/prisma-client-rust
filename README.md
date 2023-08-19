<div align="center">
    <h1>Prisma Client Rust</h1>
    <p><b>Type-safe database access for Rust</b></p>
    <img src="https://img.shields.io/badge/latest-0.6.9-blue?style=flat-square" alt="Latest version of Prisma Client Rust is 0.6.9">
    <a href="https://prisma.io">
        <img src="https://img.shields.io/static/v1?label=prisma&message=v4.8.0&color=blue&logo=prisma&style=flat-square" alt="Latest supported Prisma version is 4.8.0">
    </a>
    <img src="https://img.shields.io/github/actions/workflow/status/Brendonovich/prisma-client-rust/ci.yaml?branch=main&label=tests&style=flat-square" alt="Test Status"/>
    <a href="https://prisma.brendonovich.dev/"/>
    <img src="https://img.shields.io/badge/docs-latest-blue?style=flat-square" alt="Link to latest Documentation files">
    </a>
    <a href="https://discord.gg/5M6fpszrry">
        <img alt="Prisma Client Rust uses Discord as a place to chat and ask questions" src="https://img.shields.io/discord/1011665225809924136?color=blue&style=flat-square&logo=discord">
    </a>
</div>

<br>

Prisma Client Rust is an autogenerated query builder that provides simple and fully type-safe database access utilising the Prisma ecosystem. It is an alternative to ORMs like [Diesel](https://diesel.rs/) and [SeaORM](https://www.sea-ql.org/SeaORM/) and tools like [SQLx](https://github.com/launchbadge/sqlx).

## Why Prisma Client Rust?

For experienced Rust developers, Prisma Client Rust provides a consistent and understandable API on top of Prisma's powerful database technology.

For developers looking to step away from NodeJS and create faster, more efficient applications, Prisma Client Rust harnesses existing tooling and terminology that Prisma Client JS users will be familiar with, making developing applications in Rust more approachable.

Also - perhaps for the first time - using Prisma in a frontend application is easy.
Using Prisma Client Rust in a desktop application powered by [Tauri](https://tauri.studio/) allows the entire Prisma ecosystem to be used while developing desktop applications.

## Getting Started

Read the [installation instructions](https://prisma.brendonovich.dev/getting-started/installation) to get started and setup the CLI.

For more general information about Prisma and its CLI, check out the [official Prisma docs](https://www.prisma.io/docs/).

## Support

If you have any questions, feel free to ask them in the Prisma Client Rust + [rspc](https://github.com/oscartbeaumont/rspc) [Discord server](https://discord.gg/5M6fpszrry).

## Versioning

Prisma Client Rust is not stable.

Breaking changes will be documented and released under a new MINOR version following this format.

`MAJOR`.`MINOR`.`PATCH`

There is no release schedule, as I work on this alone and can't guarantee updates.

## Affiliation

Prisma Client Rust is not an official Prisma product, but has been [generously supported](https://twitter.com/prisma/status/1554855900124438529) as part of their FOSS Fund.

## Acknowledgements

- [steebchen](https://github.com/steebchen) and all other contributors to [Prisma Client Go](https://github.com/prisma/prisma-client-go) for writing a lot of code and documentation that Prisma Client Rust basically copies.
  Without Prisma Client Go, this project would not have even been attempted.
- [seunlanlege](https://github.com/seunlanlege) for their work on [prisma-client-rs](https://github.com/polytope-labs/prisma-client-rs) which was used while integrating Prisma's query engine crates.
- [Prisma](https://prisma.io) for developing a brilliant and flexible open source ORM, and providing sponsorship.
- [Robert Craige](https://github.com/sponsors/RobertCraigie) for writing tests for [Prisma Client Python](https://github.com/RobertCraigie/prisma-client-py) that I have adapted.
- [Spacedrive](https://spacedrive.com) for hiring me and letting me work on this.
  (sure I'm a founding member but thanks anyway!)
