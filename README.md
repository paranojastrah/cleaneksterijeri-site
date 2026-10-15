# cleaneksterijeri.com

Statička stranica (placeholder / "u obnovi") za **cleaneksterijeri.com**, hostana na GitHub Pages.

## Zašto postoji

Domena je bila preusmjerena (302) s `nginx/1.26.3` na `89.58.16.234`
(quicksrv.de VPS, NS `dns1/dns2.wndp.pt`) na `https://www.google.com/search?q=shit&udm=2`
za **svaku** putanju. HTTPS je uz to servirao cert `*.todaynet.top` (tuđi domain).

## Što je promijenjeno

- Registar (Spaceship): nameserveri prebačeni s `dns1/dns2.wndp.pt` na `launch1/launch2.spaceship.net`
- DNS: `A @` → GitHub Pages (185.199.108–111.153), `CNAME www` → `paranojastrah.github.io`
- Mail: `MX 0 .` (RFC 7505 null MX) + `TXT v=spf1 -all` + DMARC `p=reject`
  (mail se ne koristi; ovime je domain zatvoren za spoofing)
- HTTPS: GitHub Pages izdaje Let's Encrypt cert nakon što DNS propagira

## Rollback

Originalno stanje (zona operatora wndp.pt):

```
NS   ns1.wat1.wndp.pt / ns2.wat1.wndp.pt
SOA  serial 2024122600, hostmaster.cleaneksterijeri.com
A    @, www, mail, smtp, pop, ftp, webmail -> 89.58.16.234
AAAA @ -> 2a0a:4cc0:0:c9b::1
MX   10 mail.cleaneksterijeri.com
TXT  "v=spf1 a mx ip4:89.58.16.234 include:relay.wndp.pt ~all"
```

Vraćanje: `domain_set_nameservers` s `provider: "custom"`, `hosts: ["dns1.wndp.pt","dns2.wndp.pt"]`.

## Deploy

`main` branch, root folder. GitHub Pages servira `index.html` s custom domainom `cleaneksterijeri.com`.
