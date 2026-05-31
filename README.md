# Super SEO Spam Suppressor (SSSS)

A blocklist targeting websites abusing SEO tactics: junk news, content farms, scams, impersonations, and other search-engine spam.

Released into the public domain ([WTFPL](LICENSE)).

<p align="center">
  <a href="https://addons.mozilla.org/firefox/addon/ublacklist/">
    <picture>
      <source srcset="https://i.imgur.com/ZluoP7T.png" media="(prefers-color-scheme: dark)">
      <img height="58" src="https://i.imgur.com/4PobQqE.png" alt="Firefox add-ons">
    </picture>
  </a>
  <a href="https://chromewebstore.google.com/detail/ublacklist/pncfbmialoiaghdehhbnbhkkgmjanfhe">
    <picture>
      <source srcset="https://i.imgur.com/XBIE9pk.png" media="(prefers-color-scheme: dark)">
      <img height="58" src="https://i.imgur.com/oGxig2F.png" alt="Chrome Web Store">
    </picture>
  </a>
  <a href="https://ublacklist.github.io/rulesets/subscribe?url=https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/ublacklist.txt">
    <picture>
      <source srcset="assets/badge-ublacklist-dark.png" media="(prefers-color-scheme: dark)">
      <img height="58" src="assets/badge-ublacklist-light.png" alt="Add to uBlacklist">
    </picture>
  </a>
</p>

## Quick start

### Browser extensions

- **uBlacklist**: subscribe to [`ublacklist.txt`](https://ublacklist.github.io/rulesets/subscribe?url=https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/ublacklist.txt) ([docs](https://github.com/iorate/ublacklist))
- **AdBlock Plus / AdGuard**: subscribe to [`adblock.txt`](https://subscribe.adblockplus.org/?location=https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/adblock.txt)

### DNS / network level

- **Hosts file / Pi-hole**: use [`hosts.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/hosts.txt)
- **Dnsmasq**: use [`dnsmasq.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/dnsmasq.txt)
- **pdnsd**: use [`pdnsd.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/pdnsd.txt)
- **Unbound**: use [`unbound.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/unbound.txt)

### Fediverse

- **Mastodon**: import [`mastodon.csv`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/mastodon.csv)
- **Fediblockhole**: import [`fediblockhole.csv`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/fediblockhole.csv) ([docs](https://github.com/eigenmagic/fediblockhole))

## Download

| Format | File | Supports |
|--------|------|----------|
| **uBlacklist** | [`ublacklist.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/ublacklist.txt) | Domains, TLDs, URLs, pages, expressions, regex |
| **AdBlock Plus** | [`adblock.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/adblock.txt) | Domains, TLDs, URLs, pages, regex |
| **Hosts** | [`hosts.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/hosts.txt) / [`hosts_ipv6.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/hosts_ipv6.txt) | Domains |
| **Dnsmasq** | [`dnsmasq.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/dnsmasq.txt) | Domains, TLDs |
| **pdnsd** | [`pdnsd.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/pdnsd.txt) | Domains, TLDs |
| **Unbound** | [`unbound.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/unbound.txt) | Domains, TLDs |
| **Mastodon** | [`mastodon.csv`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/mastodon.csv) | Fediverse domains |
| **Fediblockhole** | [`fediblockhole.csv`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/fediblockhole.csv) | Fediverse domains |
| **Domains only** | [`domains.txt`](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest/download/domains.txt) | Domains |

All files are available on the [latest release](https://github.com/autowert66/Spam-Suppressor-NOOVERBLOCKING/releases/latest).

## Contributing

1. Add one entry per line to `.txt` files in `sources/domains/` (or the relevant `sources/` subdirectory).
2. Use subfolders and filenames to organize by category.
3. Fediverse domains should go in `.txt` files with `fediverse` in their name so they are included in the Fediverse blocklists.
4. Push changes to the `sources` folder; GitHub Actions will regenerate the blocklists and publish a release.
5. Alternatively, [open an issue](../../issues) with URLs to add or remove.

### Build locally

```bash
./scripts/update.sh   # requires bash and python
```
