<div align="center">

# pg_search_compiled

Prebuilt [pg_search](https://github.com/paradedb/paradedb) binaries for [postgresql-embedded](https://github.com/theseus-rs/postgresql-embedded).

[![CI](https://github.com/usecontextlayer/pg_search_compiled/actions/workflows/repackage.yml/badge.svg)](https://github.com/usecontextlayer/pg_search_compiled/actions/workflows/repackage.yml) [![Release](https://img.shields.io/github/v/release/usecontextlayer/pg_search_compiled)](https://github.com/usecontextlayer/pg_search_compiled/releases/latest) [![License](https://img.shields.io/github/license/usecontextlayer/pg_search_compiled)](LICENSE)

</div>

This repo doesn't contain source code. A GitHub Actions workflow watches [ParadeDB](https://github.com/paradedb/paradedb) releases, downloads the official pg_search packages, and repackages them into the archive layout that postgresql-embedded expects. If you're looking to use pg_search in your project, see [pgx](https://github.com/usecontextlayer/pgx).

- **Automatic tracking** -- a daily cron checks for new ParadeDB releases and repackages on detection, no manual intervention needed.
- **Two platforms** -- builds for macOS ARM64 (`aarch64-apple-darwin`) and Linux x86_64 (`x86_64-unknown-linux-gnu`), each as `.zip` and `.tar.gz`.
- **Stable release tags** -- versioned as `v0.{pg_major}.{run_number}`, with the upstream pg_search version recorded in the release body.
- **Minimal footprint** -- ships only the shared library (`.dylib`/`.so`), control file, and migration SQL. Nothing else.

### How it works

The workflow downloads the official `.pkg` (macOS) or `.deb` (Linux) from ParadeDB, extracts the extension files, and repacks them into a flat `lib/` + `share/extension/` layout. That archive is what postgresql-embedded resolves at runtime to install pg_search into an embedded Postgres instance.

MIT License
