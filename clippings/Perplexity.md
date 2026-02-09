---
title: "Perplexity"
source: "https://www.perplexity.ai/search/what-is-2-1-and-2-dev-null-on-XluCGqfmTbyxJxfX4oq7eg"
author:
  - "[[Perplexity AI]]"
published:
created: 2026-02-09
description: "Perplexity is a free AI-powered answer engine that provides accurate, trusted, and real-time answers to any question."
tags:
  - "clippings"
---
[Read](https://www.perplexity.ai/spaces/read-pxlYtQlOTeqY8SFq1xHlgg)

## what is 2>&1 and 2>/dev/null on linux

In Linux shells, `2>&1` and `2>/dev/null` are redirection operators that control where a command sends its error messages. They work with the standard file descriptors: `0` (stdin), `1` (stdout), and `2` (stderr).

## Basics of file descriptors

- Every process has three standard streams: input (`0`), output (`1`), and error (`2`).
- `>` redirects standard output (`1`) unless you specify another descriptor number before it.
- Writing `2>` means “redirect file descriptor 2 (stderr) somewhere”.

## What 2>/dev/null does

- `/dev/null` is a special device that discards anything written to it (a “black hole”).
- `2>/dev/null` means “send stderr (file descriptor 2) to `/dev/null` ”, effectively hiding all error messages from that command.

Example:

```
bash
cmd 2>/dev/null
```

- Normal output (stdout) still appears.
- Only errors are suppressed.

## What 2>&1 does

- `&1` means “the same place file descriptor 1 (stdout) is currently going”, not a file named `1`.
- `2>&1` means “redirect stderr (2) to wherever stdout (1) is currently redirected”.

Examples:

```
bash
cmd >out.log 2>&1
```

- First, `>out.log` sends stdout to `out.log`.
- Then, `2>&1` sends stderr to the same place as stdout, so both stdout and stderr go into `out.log`.

```
bash
cmd >/dev/null 2>&1
```

- Stdout is redirected to `/dev/null`.
- Then stderr is redirected to “where stdout is”, which is `/dev/null`.
- Result: both normal output and errors are discarded.

## Order matters

These two are different:

```
bash
cmd >/dev/null 2>&1   # both stdout and stderr discarded
cmd 2>&1 >/dev/null   # stderr goes to original stdout; stdout goes to /dev/null
```

In the second case, stderr still appears on the terminal because it was redirected to stdout *before* stdout was changed.

if i cant connect to a database with dbeaver without being connected to a VPN (company's policy) does that mean i am trying to connect to it using its private IP address? otherwise, if that were its public IP address i would be able to connect to it regardless of the VPN connection? how does dbeaver usually connects to databases (postgres btw), using the private or public IP?

Needing the VPN almost certainly means the database is only reachable on a private network (private IP or private DNS endpoint), not directly over the public internet.[learn.microsoft +1](https://learn.microsoft.com/en-us/answers/questions/2284612/vpn-connected-but-cannot-resolve-private-postgresq)

## Why VPN is required

- Many companies expose PostgreSQL only inside their VPC/on‑prem network or via a “private endpoint”, which has a private IP (e.g. 10.x/172.16.x/192.168.x).[cloud.google +1](https://cloud.google.com/database-migration/docs/postgres/configure-connectivity-vpns)
- When you connect your VPN, your machine joins that private network (or gets routes into it), so `host:port` becomes reachable.[learn.microsoft +1](https://learn.microsoft.com/en-us/answers/questions/2284612/vpn-connected-but-cannot-resolve-private-postgresq)
- Without VPN, your traffic never reaches that private network, so the TCP connect fails (timeout / no route) regardless of credentials.

If the DB had a true public IP or a public DNS endpoint that resolves to a public address and the company allowed access from your home IP, you would not need the VPN to reach it. In many setups, firewall rules additionally restrict which client IPs can hit the DB, often to a VPN IP range only.[learn.microsoft +2](https://learn.microsoft.com/en-us/answers/questions/529653/connecting-to-postgresql-through-vpn)

## How DBeaver connects

- DBeaver uses JDBC; you configure `host`, `port` (default 5432), `database`, `user`, `password`, or a full JDBC URL.[cdata +2](https://www.cdata.com/kb/tech/postgresql-jdbc-dbvr.rst)
- The `host` can be:
	- A private IP or private DNS name (requires VPN or being inside that network).[dbeaver +1](https://dbeaver.io/2011/05/16/dbeaver-external-database-hosting/) YouTube
	- A public DNS name / IP for hosted Postgres (Neon, RDS with public endpoint, etc.).[neon +1](https://neon.com/guides/dbeaver-hosted-postgres)
- DBeaver itself does not “prefer” private or public; it just connects to whatever host you configure. Your company policy and network design decide whether that host is only reachable through VPN.[dbeaver +1](https://dbeaver.com/docs/dbeaver/Database-driver-PostgreSQL/)

## Practical checks

- Look at the DBeaver connection “Host” field:
	- If it is an RFC1918 address (10.x, 172.16–31.x, 192.168.x) or something like `*.private.postgres.database.azure.com`, it’s a private endpoint.[learn.microsoft](https://learn.microsoft.com/en-us/answers/questions/2284612/vpn-connected-but-cannot-resolve-private-postgresq)
	- If it’s a generic public hostname from a cloud DB provider, it’s likely public, but access may still be IP‑restricted.[cloud.google +1](https://cloud.google.com/database-migration/docs/postgres/configure-connectivity-vpns)
- If you want to avoid full VPN, typical options are:
	- SSH tunnel / bastion host configured in DBeaver’s SSH settings.[dbeaver +2](https://dbeaver.com/docs/dbeaver/SSH-Configuration/)
	- A managed public endpoint with tight IP allowlists and SSL.[neon +1](https://neon.com/guides/dbeaver-hosted-postgres)

So: you are almost certainly connecting to a private address (IP or DNS) or at least to an endpoint only routable/allowed via VPN, and DBeaver just uses whatever host your company gave you.

the IPs are actually 52.90.223.211 and 3.90.57.87 respectively, is there anything that can be inferred from those? is there a way to "check" if they're public or private (i dont know, trying to search for them or ping them maybe?)

Those two addresses (52.90.223.211 and 3.90.57.87) are public IPs, not private. They are in ranges owned by cloud providers (e.g., AWS), not in the RFC1918 private blocks.[datatracker.ietf +3](https://datatracker.ietf.org/doc/html/rfc1918)

## How to tell public vs private

RFC1918 defines private IPv4 ranges as: 10.0.0.0/8, 172.16.0.0–172.31.0.0/12, and 192.168.0.0/16.[techtarget +2](https://www.techtarget.com/whatis/definition/RFC-1918)  
Any address outside those ranges (like 3.x.x.x or 52.x.x.x) is globally unique and considered public, assuming it is announced on the internet.[arin](https://www.arin.net/reference/research/statistics/address_filters/)

So just by looking:

- 52.90.223.211 → not 10/8, 172.16–31/12, or 192.168/16 → public.
- 3.90.57.87 → same logic → public.

## Ways to “check” them

- Compare against the private ranges above; if it’s not in those, it’s public space.[datatracker.ietf +2](https://datatracker.ietf.org/doc/html/rfc1918)
- Use a WHOIS / IP lookup site (ipinfo, ARIN, whois.com, etc.) to see which organization owns the IP and confirm it is routable public space.[lacnic +3](https://www.lacnic.net/1040/2/lacnic/whois)
- `ping` or `traceroute` can tell you if there is a route/reply, but not whether the IP is “private vs public” in the RFC sense; many public IPs just drop ICMP.[arin](https://www.arin.net/reference/research/statistics/address_filters/)

## Why VPN is still required

Even though the DB IPs are public, your company can still:

- Bind Postgres to those public IPs but firewall them so only connections from VPN address ranges are allowed.[ceiamerica +1](https://www.ceiamerica.com/blog/defining-private-addresses/)
- Put the DB behind security groups, ACLs, or other controls that only permit traffic from inside the corporate network or VPN.[cloud.google +1](https://cloud.google.com/database-migration/docs/postgres/configure-connectivity-vpns)

So, in your case: those addresses are public, but firewall / security policy is almost certainly blocking traffic from your normal home IP and only allowing it when you are on the VPN.

neither nslookup, dig or host are available commands (currently on my arch linux OS), do i need to install them, if so, how?

Yes, `nslookup`, `dig`, and `host` are not installed by default on minimal Arch Linux setups. Install them via the `bind` tools package.

## Install command

Run as root (or with `sudo`):

```
bash
sudo pacman -S bind-tools
```

This provides `dig`, `host`, and `nslookup` from ISC BIND.[datatracker.ietf](https://datatracker.ietf.org/doc/html/rfc1918)

## Verify and use

After installation:

```
bash
dig temporal.oficinareserva.com
host temporal.oficinareserva.com
nslookup temporal.oficinareserva.com
```

All three will now work and show the IP addresses.

## Alternative (no install needed)

Arch's base system has `getent`, which uses your system's resolver:

```
bash
getent hosts temporal.oficinareserva.com
```

Outputs lines like `52.90.223.211 temporal.oficinareserva.com` without needing extra packages. This respects your DNS settings (VPN or not).

ok so i found out with 'host' the 3 IP addresses resolved from the DNSes i wanted to search. they are respectively 3.81.235..., 18.209.56..., 34.202.230... are these three public IPs? can it be told just by looking at them?

Yes, all three IP addresses (3.81.235.*, 18.209.56.*, and 34.202.230.\*) are public IPs. They can be identified as public just by looking at them, as none fall into the RFC 1918 private ranges.

## Private IP ranges recap

Private IPv4 addresses are strictly limited to:

- 10.0.0.0–10.255.255.255 (10.0.\*/8)
- 172.16.0.0–172.31.255.255 (172.16–31.\*/12)
- 192.168.0.0–192.168.255.255 (192.168.\*/16)

Anything outside these (like 3.*, 18.*, or 34.\*) is public address space assigned by IANA/regional registries.

## Quick check for these IPs

- 3.81.235.\* → Starts with 3 (AWS-owned public range). Public.
- 18.209.56.\* → Starts with 18 (AWS EC2 public range). Public.
- 34.202.230.\* → Starts with 34 (Google Cloud public range). Public.

These patterns match known cloud provider public blocks, confirming they're routable on the internet (though firewalls may still restrict access without VPN).

what is the concept of public and private IP addresses? how does this concept applies to cloud providers such as what you've been referring to as "AWS-owned public range" or "AWS EC2 public range"?

Public IP addresses are globally unique identifiers routable across the entire internet, assigned by ISPs or registries from non-reserved space. Private IP addresses come from specific reserved ranges (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 per RFC 1918) and are only valid within local networks, never routed publicly to avoid conflicts.

## Key differences

| Aspect | Public IP | Private IP |
| --- | --- | --- |
| Scope | Global/internet-wide | Local network only |
| Uniqueness | Unique worldwide | Reusable across networks |
| Routing | Directly accessible online | Blocked by internet routers; needs NAT |
| Assignment | By ISP/IANA registries | By local router/DHCP |
| Security | Exposed; needs firewalls | Isolated by design [geeksforgeeks +1](https://www.geeksforgeeks.org/computer-networks/difference-between-private-and-public-ip-addresses/) |

Private IPs enable efficient internal communication (e.g., your home devices), while public IPs handle external traffic via Network Address Translation (NAT), where one public IP represents many private ones.

## Cloud providers like AWS

Clouds like AWS own massive public IP blocks (e.g., 3.0.0.0/8, 18.0.0.0/8, 52.0.0.0/8) allocated by registries.[geeksforgeeks](https://www.geeksforgeeks.org/computer-networks/difference-between-private-and-public-ip-addresses/)

- **Public instances/endpoints**: AWS assigns an Elastic IP or public IPv4 from their range (like your 3.81.*, 18.209.*, 52.90.\* examples). Directly reachable from anywhere, but security groups/NACLs control access—often restricting to VPN/CIDRs.
- **Private subnets**: Instances get RFC1918 IPs (10.x.x.x). Only accessible within VPC or via VPN/Direct Connect; public internet can't route there.
- **Dual-stack**: Many resources have both (public for ingress, private internally). Your PostgreSQL IPs are AWS public, but company policy (security groups) blocks non-VPN traffic.[jumpcloud +1](https://jumpcloud.com/it-index/whats-the-difference-between-a-public-and-private-ip-address)

Follow-ups