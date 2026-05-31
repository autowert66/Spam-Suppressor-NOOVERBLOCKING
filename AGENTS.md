# AGENTS.md — Super SEO Spam Suppressor

## What this repo is

A data repository that generates multiple blocklist formats (uBlacklist, AdBlock, Hosts, DNS, Fediverse CSV, etc.) from source files in `sources/`. There is no package manager, test suite, or build system beyond bash + Python 3 scripts.

## Do not edit generated files

All `.txt` and `.csv` files at the repo root (`domains.txt`, `ublacklist.txt`, `adblock.txt`, `hosts.txt`, `hosts_ipv6.txt`, `dnsmasq.txt`, `pdnsd.txt`, `unbound.txt`, `mastodon.csv`, `fediblockhole.csv`) are **generated**. Edit files under `sources/` only.

## Source layout

| Directory | Content |
|---|---|
| `sources/domains/` | One domain per line in `.txt` files. Subfolders organize categories. |
| `sources/urls/` | URL patterns (one per line). |
| `sources/pages/` | Page patterns (one per line). |
| `sources/tlds/` | TLD entries (one per line, without leading dot). |
| `sources/expressions/` | uBlacklist expressions. |
| `sources/regex/` | Regex patterns for adblockers. |
| `sources/imports/` | External list definitions, originals, cleaned copies, and allowlist. |
| `sources/offline/` | `offline_domains.txt` — domains pruned from all generated domain lists. |
| `sources/headers/` | Header templates prepended to generated blocklists. |

## Build commands

- `./scripts/update.sh` — normalizes source files, combines them, prunes offline domains, and regenerates all root-level blocklists. Requires `bash` and `python`.
- `./scripts/import.sh` — downloads external lists, cleans them, applies the allowlist, and copies them to `sources/domains/_imported/`. Requires `bash`, `curl`, and `python`.

**Command order for imports:** run `./scripts/import.sh` *before* `./scripts/update.sh` (the CI `import.yml` workflow does this automatically).

## Contributing rules

- Add one entry per line in `.txt` files inside `sources/domains/` (or the relevant `sources/` subdirectory).
- Use subfolders and `.txt` filenames to organize by category.
- Use inline comments (`#`) and `.md` files in the same folder for documentation and references.
- Fediverse domains: put them in `.txt` files with `fediverse` in the name (e.g. `Bad Fediverse.txt`) so they are included in `mastodon.csv` and `fediblockhole.csv`.

## Importing external lists

Add a line to `sources/imports/importlist.txt` in this format:

```
filename.txt|https://example.com/list.txt
```

The allowlist (`sources/imports/allowlist.txt`) removes false positives from imported lists before they are merged.

## Normalization gotchas

- `./scripts/update.sh` mutates source files in place when run locally. It lowercases domains, strips protocols (`http://`, `https://`), `www.` subdomains, and paths, and deduplicates lines per file.
- Comments and empty lines are preserved in individual source files, but removed from the combined root lists.

## CI behavior

- `.github/workflows/update.yml` triggers on pushes to `sources/**.txt` (excluding `sources/imports/**`), runs `./scripts/update.sh`, and auto-commits.
- `.github/workflows/import.yml` triggers on pushes to `sources/imports/**.txt` or on a cron schedule, runs `./scripts/import.sh` then `./scripts/update.sh`, and auto-commits.

## Verification

There is no automated test suite. Verify changes by running `./scripts/update.sh` locally and inspecting the generated root files. If you run `import.sh`, expect `sources/imports/original/` and `sources/imports/modified/` to change.
