# Rustrak for musl

Static `x86_64-unknown-linux-musl` builds of [Rustrak](https://github.com/rustrak/rustrak) for servers without glibc
(Alpine) and without Docker. The server is built from an unmodified upstream commit, pinned here as the git submodule
`rustrak`, with the upstream release profile. This repository holds only the workflow that does it. It is not affiliated
with the Rustrak project.

## What a release holds

- `rustrak-<tag>-x86_64-unknown-linux-musl.tar.gz`: the `rustrak` server binary;
- `SHA256SUMS`: its SHA-256 (`sha256sum -c SHA256SUMS`);
- the release notes name the upstream commit it was built from.

The dashboard is not built here (it needs Node and pnpm): take the static files from the upstream image
(`/app/static`), which are the same on every platform.

## Build another version

1. Move the submodule to the upstream tag and commit it:
   `git -C rustrak fetch --tags && git -C rustrak checkout v0.33.0 && git add rustrak && git commit -m "Pin Rustrak v0.33.0"`
2. Push, then Actions, "Build Rustrak for musl", Run workflow, with the same tag.

The run stops if the pinned commit is not the commit of that tag. No third-party action is used: only `git`, `apk`,
`rustup` and the `gh` CLI, on `alpine:3.24`.

## Licenses

The files of this repository are MIT ([LICENSE](LICENSE)). Rustrak is AGPL-3.0-only; the binaries are unmodified builds of
its source, which every release names.
