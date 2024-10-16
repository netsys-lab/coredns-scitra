# scitra

## Name

*scitra* - resolves SCION TXT records to SCION-mapped IPv6 addresses

## Description

This CoreDNS plugin is a companion to [SCION-IP Address Translators][1] that returns special AAAA
addresses (SCION-mapped IP addresses) for host that announce SCION support in a TXT record.

TXT records recognized by this plugin must have the form "scion=<ISD-ASN>,<Host>" where <ISD-ASN> is
a SCION AS and <Host> is an IPv4 or IPv6 address.

[1] https://github.com/netsys-lab/scion-ip-translator

## Syntax

```txt
scitra [prefix PREFIX]
```

* `prefix` **PREFIX** is an 8 bit long IPv6 prefix in CIDR notation that is used by translators to
  identify SCION-mapped IPv6 addresses. The default prefix is `fc00::/8`.

## Compilation

Add the following to `plugin.cfg` and recompile CoreDNS:
```txt
# add this line right before cache:cache
scitra:github.com/netsys-lab/coredns-scitra
```

## Example

Forward queries to another DNS server and rewrite SCION addresses.
```txt
. {
    forward . 1.1.1.1
    scitra
    cache
}
```
