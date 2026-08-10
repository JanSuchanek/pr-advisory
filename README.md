# P&R Advisory — web

Jednostránkový prezentační web P&R Advisory, s.r.o. — financování nákladní techniky
(úvěr, leasing, pojištění) a poradenství v oblasti nástaveb.

**Živě:** https://pradvisory.cz/

## Struktura

| Soubor | K čemu je |
|---|---|
| `index.html` | Celý web. Soběstačný — CSS i všechny obrázky jsou vložené přímo v souboru (base64 data URI), takže stránka nedělá žádný požadavek navíc kromě Google Fonts. |
| `logo-mark.webp` | Favicon. Jediný externí asset. |
| `CNAME` | Custom doména pro GitHub Pages. **Nemazat** — bez něj se web po deployi odpojí od `pradvisory.cz`. |
| `.nojekyll` | Vypíná Jekyll build na Pages. |
| `robots.txt`, `sitemap.xml` | SEO. |

V repu **není** (vylučuje `.gitignore`, leží to lokálně v pracovní složce):

- zdrojová loga v plném rozlišení — `pr-advisory-logo*.png`, `logo-full.png`,
  `logo-cernobile.png`, `moderni-logo.png`, `barevne-schema.png`
- ZIP záloha
- `verze2/` a `verze3/` — alternativní designové varianty (vzájemně identické).
  Nasazuje se pouze root; pokud se některá varianta schválí, přepíše se jí root.

## Deploy

GitHub Pages, zdroj = branch `main`, adresář `/` (root). Deploy proběhne automaticky po pushi:

```bash
git push
```

Za pár desítek sekund je změna živá. Stav buildu je vidět v záložce **Actions** repozitáře.

## Úpravy obsahu

Všechno se edituje v `index.html`. Pozor na to, že soubor obsahuje dlouhé base64 řetězce
s obrázky — při hledání v editoru je praktické zapnout „word wrap off".

Pokud se mění logo nebo grafika, je potřeba nový obrázek znovu zakódovat do base64
a nahradit příslušný data URI (nebo obrázek uložit jako samostatný soubor a odkázat ho
běžně přes `src`).

## Doména a DNS

Doména je registrovaná u VAS Hostingu, DNS spravuje jejich portál
(`portal.vas-hosting.cz`). Web servíruje GitHub Pages:

- apex `pradvisory.cz` → A záznamy `185.199.108–111.153`
- `www.pradvisory.cz` → CNAME `jansuchanek.github.io.` (GitHub přesměruje na apex)

**Mail zůstává u VAS Hostingu** — MX `mail.vas-hosting.cz`. Při jakékoli změně DNS na MX
a TXT (SPF/DKIM) nesahat.

## TODO

- [ ] Doplnit `og:image` — pro náhled při sdílení na sociálních sítích. Musí to být
      samostatný soubor s absolutní URL (base64 v `og:image` nefunguje), ideálně 1200×630 px.
