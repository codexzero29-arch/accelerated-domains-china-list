# accelerated-domains-china-list

Small PHP utilities that turn a domain list into DNS forwarder configuration for common resolvers.

This repository is designed around a plain text file named `china_domains.txt`, where each line contains a domain name. The scripts generate DNS forwarding rules for:

- dnsmasq
- BIND
- Unbound

The result is a lightweight way to forward selected Chinese domains to specific upstream resolvers without maintaining separate manual config for each target.

## Repository layout

- `bind.php` — generates BIND `zone` forward definitions.
- `dnsmasq.php` — generates `server=/domain/ip` entries for dnsmasq.
- `unbound.php` — generates `forward-zone` blocks for Unbound.
- `generate-confs-from-raw-list` — runs all three generators and writes `bind.conf`, `dnsmasq.conf`, and `unbound.conf`.
- `generate-raw-list-from-dnsmasq-conf` — extracts domain names from `server=/domain/ip` style lines and writes them to `china_domains.txt`.

## Input format

The tool expects `china_domains.txt` to be present in the repository root. Each line should contain one domain, for example:

```text
apple.com
example.net
google.com
