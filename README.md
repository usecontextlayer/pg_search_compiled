# pg_search_compiled

Precompiled packages of [ParadeDB pg_search](https://github.com/paradedb/paradedb) for use with [theseus-rs/postgresql-embedded](https://github.com/theseus-rs/postgresql-embedded).

This repository contains a GitHub Actions workflow that watches ParadeDB releases, downloads the platform-native packages (.pkg for macOS, .deb for Linux), extracts the raw extension files, and repackages them as `.zip` archives with naming conventions compatible with the theseus `postgresql_extensions` crate.

## Release assets

Each release produces archives for the supported platforms:

```
pg_search-aarch64-apple-darwin-pg17.zip
pg_search-aarch64-apple-darwin-pg17.tar.gz
pg_search-x86_64-unknown-linux-gnu-pg17.zip
pg_search-x86_64-unknown-linux-gnu-pg17.tar.gz
```

Release tags follow the pattern `v0.{pg_major}.{run_number}` (e.g., `v0.17.1`). The release body includes the upstream ParadeDB version.

## Archive contents

Each archive contains the extension files needed by PostgreSQL:

```
pg_search-{triple}-pg17/
  lib/
    pg_search.dylib   (macOS)
    pg_search.so       (Linux)
  share/
    extension/
      pg_search.control
      pg_search--*.sql
```

## Usage with theseus-rs

Register a custom `Repository` implementation pointing at this repo, then call `postgresql_extensions::install()`. See [contextlayer/pgx](https://github.com/usecontextlayer/pgx) for a working integration.
