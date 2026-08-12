---
name: seo-geo-audit
description: Provede SEO a GEO audit webu — title, meta description, nadpisy, sémantika, structured data, sitemap, robots.txt, OG obrázky, rychlost, interní prolinkování, a zvlášť připravenost pro AI vyhledávače a jazykové modely (ChatGPT, Perplexity, Google AI Overviews). Použij tento skill, když uživatel žádá o SEO audit, kontrolu SEO, GEO, AI SEO, LLM optimalizaci, ptá se "jak na tom jsem se SEO?", "najde mě Google?", "budu vidět v ChatGPT?", nebo řeší meta tagy, sitemapu, structured data a indexaci.
---

# SEO + GEO audit

Dvě věci najednou:
- **SEO** — aby web našel a správně pochopil vyhledávač.
- **GEO** (Generative Engine Optimization) — aby web dokázaly citovat AI nástroje jako ChatGPT, Perplexity, Claude a Google AI Overviews.

Principy se překrývají, ale ne úplně. Klasické SEO řeší hodně signály a odkazy; GEO stojí na tom, jak jasně a citovatelně je obsah napsaný.

## Postup

1. **Zjisti typ webu a téma** — bez znalosti toho, na co má být web nalezen, nemá audit smysl. Když to není jasné z kódu, zeptej se, na jaké dotazy chce být uživatel vidět.
2. **Přečti reálné soubory** — metadata (`layout.tsx`, `<head>`, `metadata` export), obsah stránek, `robots.txt`, `sitemap.xml`, `next.config`.
3. **Projdi oba checklisty** níže.
4. **Vypiš výstup** podle struktury a seřaď podle dopadu.
5. **Nabídni**, že P0 a P1 věci hned doplníš do kódu.

## SEO checklist

### Základní metadata (nejčastěji chybí)
- **Title** — má každá stránka unikátní title, cca 50–60 znaků, s klíčovým slovem vpředu? Není tam pořád defaultní "Create Next App" nebo "Vite + React"?
- **Meta description** — 120–160 znaků, popisuje konkrétní obsah, ne obecná fráze. Chybí-li, vyhledávač si text vybere sám.
- **Jeden `<h1>`** na stránku, který odpovídá tématu.
- **`lang`** atribut na `<html>` (u českého webu `lang="cs"`).
- **Canonical URL**, hlavně když je stejný obsah dostupný na víc adresách.
- **Favicon** a `apple-touch-icon`.

### Sdílení na sociálních sítích
- Open Graph: `og:title`, `og:description`, `og:image` (1200×630), `og:url`, `og:type`.
- Twitter card: `twitter:card` (`summary_large_image`).
- **Ověř, že OG obrázek fyzicky existuje** na uvedené cestě. Odkaz na neexistující obrázek je častá chyba.

### Struktura a obsah
- Logická hierarchie nadpisů (h1 → h2 → h3, bez přeskakování).
- Má stránka dost skutečného textu, nebo jen pár slov a obrázky? (Prázdná landing page se hůř řadí i cituje.)
- Popisné texty odkazů — místo "klikněte zde" použij "ceník služeb".
- Alt texty u obrázků (pomáhají SEO i přístupnosti).
- Interní prolinkování mezi souvisejícími stránkami.
- Čitelné URL (`/cenik` místo `/page?id=42`).

### Technické SEO
- **`robots.txt`** — existuje a neblokuje omylem celý web (`Disallow: /`)?
- **`sitemap.xml`** — existuje a je uvedená v `robots.txt`?
- Není někde `<meta name="robots" content="noindex">` zapomenutý z vývoje?
- Vykresluje se obsah tak, aby ho robot viděl? (Čistě klientský rendering bez SSR obsah zhoršuje.)
- Rychlost: velikost obrázků (WebP místo 4 MB JPEG), lazy loading, velikost bundlu.
- HTTPS a fungující přesměrování z `www` / non-`www` na jednu variantu.

### Structured data (pomáhá SEO i GEO)
- JSON-LD schema podle typu webu: `Organization`, `LocalBusiness`, `Product`, `Article`, `FAQPage`, `BreadcrumbList`.
- Odpovídá schema tomu, co je na stránce reálně vidět?

## GEO checklist (AI vyhledávače a LLM)

AI nástroje si vybírají obsah, který dokážou jednoznačně pochopit a odcitovat. Na co se zaměřit:

- **Přímé odpovědi na konkrétní otázky.** Sekce s otázkou v nadpisu a odpovědí hned v prvním odstavci se cituje mnohem snáz než dlouhý marketingový text.
- **Odpověď hned na začátku.** Nejdřív tvrzení, pak vysvětlení — ne naopak.
- **Konkrétní fakta místo frází.** "Doba odezvy do 2 hodin, ceny od 15 000 Kč" je citovatelné. "Špičková kvalita a individuální přístup" ne.
- **Kdo, co, kde, za kolik** — jasně a na jednom místě. Kdo za webem stojí, co konkrétně nabízí, pro koho to je, kolik to stojí, jak ho kontaktovat.
- **FAQ sekce** s reálnými dotazy zákazníků, ideálně i s `FAQPage` structured data.
- **Samostatně stojící odstavce.** Text, který se dá vytrhnout z kontextu a pořád mu jde rozumět.
- **Signály důvěry** — jméno autora, datum aktualizace, kontaktní údaje, reference, čísla.
- **Text jako text, ne jako obrázek.** Klíčová informace na obrázku nebo ve videu pro AI neexistuje.
- **Přístupnost pro AI crawlery** — neblokuje `robots.txt` boty jako `GPTBot`, `PerplexityBot`, `ClaudeBot`, když má web být citovaný?
- **Konzistence napříč webem** — stejný název firmy, stejná adresa, stejné tvrzení o tom, co děláte.

## Struktura výstupu

```
## Stav
Dvě věty: jak je web připravený pro Google a jak pro AI vyhledávače.

## P0 — Bez tohohle tě nenajdou
- **[Nález]** — `soubor:řádek`
  Dopad: ...
  Oprava: konkrétní kód nebo text k doplnění

## P1 — Výrazně to pomůže
(stejný formát)

## P2 — Doladění
(stejný formát)

## GEO — připravenost pro AI vyhledávače
Zvlášť, protože se to od klasického SEO liší.

## Návrh konkrétních textů
Když chybí title, description nebo OG texty, napiš rovnou hotové znění k použití.

## Neověřeno
Co nejde zkontrolovat z kódu (zpětné odkazy, reálné pozice ve vyhledávání, Search Console).
```

## Zásady

- **Piš hotové texty, ne zadání.** Místo "doplň meta description" napiš přesné znění včetně délky ve znacích.
- **Žádné keyword stuffing.** Nedoporučuj napchat klíčová slova do textu; poškodí to čitelnost i výsledek.
- **Nic negarantuj.** Nikdo neslíbí pozici ve vyhledávání ani citaci v ChatGPT. Mluv o připravenosti a pravděpodobnosti.
- **Rozliš, co jsi ověřil v kódu, a co se dá zjistit jen z reálného provozu.**
- U nového webu buď realistický: nejdřív dořeš základy (title, description, sitemap, obsah), a až potom pokročilé věci.
