# AGENTS.md — Super SEO Spam Suppressor

## What this repo is

A data repository that generates multiple blocklist formats (uBlacklist, AdBlock, Hosts, DNS, Fediverse CSV, etc.) from source files in `sources/`. There is no package manager, test suite, or build system beyond bash + Python 3 scripts.

## Do not edit generated files

The blocklist files (`domains.txt`, `ublacklist.txt`, `adblock.txt`, `hosts.txt`, `hosts_ipv6.txt`, `dnsmasq.txt`, `pdnsd.txt`, `unbound.txt`, `mastodon.csv`, `fediblockhole.csv`, `fediverse_domains.txt`) are **generated** and are no longer committed to the repository. They are published as GitHub Release assets.

The combined source lists (`sources/domains.txt`, `sources/urls.txt`, `sources/pages.txt`, `sources/tlds.txt`, `sources/expressions.txt`, `sources/regex.txt`, `sources/fediverse_domains.txt`) are also generated and must not be committed. All are listed in `.gitignore`.

Edit files under `sources/` subdirectories only.

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

- Comments and empty lines are preserved in individual source files, but removed from the combined root lists.

## CI behavior

- `.github/workflows/update.yml` triggers on pushes to `sources/**.txt` (excluding `sources/imports/**`), runs `./scripts/update.sh`, and creates a GitHub Release with the generated blocklists as assets.
- There is no automated import workflow; run `./scripts/import.sh` manually if you need to refresh external lists.

**Note:** the `sources/domains/_imported/`, `sources/imports/original/`, and `sources/imports/modified/` directories were removed when the automated import workflow was deleted. External lists are no longer merged automatically.
