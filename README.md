# Rust Release Workflow Example

An example Rust project showcasing an automated release workflow using `cargo-release` and GitHub Actions.

## Setup

Run the development setup script to install `cargo-release`:

```bash
./devsetup.sh
```

## Releasing a New Version

To release a new version (bumping version, running tests, committing, tagging, and pushing):

```bash
./release.sh <major|minor|patch>
```

This uses the configuration defined in `.config/release.toml`.

## GitHub Actions Workflow

When a tag matching `v*` is pushed to GitHub:

1. **Test**: Runs cargo tests via `cargo-nextest`.
2. **Build**: Compiles binaries for multiple target architectures:
   - `x86_64-unknown-linux-gnu` (Linux native)
   - `x86_64-unknown-linux-musl` (Linux static musl via `cross`)
   - `aarch64-unknown-linux-gnu` (Linux ARM64 via `cross`)
   - `x86_64-pc-windows-msvc` (Windows MSVC)
3. **Publish**: Packages and uploads binaries to a new GitHub Release.
