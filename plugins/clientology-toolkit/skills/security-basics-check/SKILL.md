---
name: security-basics-check
description: Zkontroluje základní bezpečnost webu nebo aplikace — API klíče a secrets v kódu, .env a .gitignore, veřejně vystavené endpointy, autentizace, validace vstupů, XSS, nezabezpečené formuláře a nebezpečné závislosti. Použij tento skill, když uživatel žádá o security audit, bezpečnostní kontrolu, kontrolu před nasazením / spuštěním webu, ptá se "je to bezpečné?", "nemám tam někde klíče?", "můžu to pustit do světa?", nebo řeší secrets, API keys a .env soubory.
---

# Security basics check

Praktická kontrola bezpečnosti pro weby a malé aplikace. Cíl: najít věci, které reálně způsobí škodu — uniklé klíče, otevřené endpointy, chybějící validace. Ne teoretický seznam všech možných hrozeb.

## Postup

1. **Zjisti typ projektu** — statický web, Next.js, backend s databází? Určuje to, co má vůbec smysl kontrolovat.
2. **Projdi checklist** níže. Používej hledání v souborech, nespoléhej na odhad.
3. **Ověř každý nález** otevřením souboru. Falešné poplachy jsou horší než žádný audit.
4. **Vypiš výstup** podle struktury níže.
5. **Nabídni opravu** P0 nálezů. U uniklých klíčů vždy zdůrazni, že samotné smazání z kódu nestačí — klíč se musí zneplatnit a vygenerovat nový.

## Checklist

### Secrets a API klíče (nejčastější reálný problém)
- Prohledej repo na vzory: `sk-`, `sk_live`, `AIza`, `ghp_`, `xoxb-`, `AKIA`, `-----BEGIN`, `password =`, `secret =`, `token =`, `apiKey`.
- Je `.env` (a `.env.local`, `.env.production`) v `.gitignore`?
- **Je `.env` už commitnutý v gitu?** Zkontroluj `git ls-files` — pokud ano, je to P0 i po smazání, protože zůstává v historii.
- Existuje `.env.example` s názvy proměnných bez hodnot?
- **Frontend vs. backend proměnné:** cokoliv s prefixem `NEXT_PUBLIC_`, `VITE_`, `PUBLIC_` je viditelné komukoliv v prohlížeči. Je tam něco, co by nemělo?
- Volá se placený nebo privilegovaný API (OpenAI, Stripe, databáze) přímo z frontendu s klíčem v kódu?

### Autentizace a autorizace
- Jsou chráněné stránky opravdu chráněné na serveru, nebo se jen skrývá UI na klientovi?
- Kontroluje každý API endpoint, že uživatel je přihlášený **a** že smí pracovat právě s těmi daty?
- Nejde načíst cizí data jen změnou ID v URL nebo requestu?
- Nejsou v kódu natvrdo napsané přihlašovací údaje nebo "dočasný" admin bypass?

### Vstupy a data
- Validují se data přicházející od uživatele na serveru (ne jen v prohlížeči)?
- Skládají se SQL dotazy stringem, nebo se používají parametrizované dotazy / ORM?
- Vkládá se někde uživatelský obsah přes `innerHTML` nebo `dangerouslySetInnerHTML`? (XSS)
- Má formulář ochranu proti spamu a zneužití — rate limiting, captcha, honeypot?
- U uploadu souborů: kontroluje se typ a velikost?

### Nasazení a konfigurace
- Běží web na HTTPS?
- Nevypisují se uživateli detailní chybové hlášky se stack tracem, cestami nebo SQL dotazy?
- Nejsou v produkci vystavené debug endpointy, admin panely bez hesla nebo testovací stránky?
- Je CORS nastavený rozumně, nebo `*` u endpointů s citlivými daty?
- Jsou zapnuté základní security hlavičky? (U statického webu není P0, u aplikace s přihlášením ano.)

### Závislosti
- Spusť `npm audit` (nebo ekvivalent) a vypiš **jen** high a critical nálezy, které se týkají kódu v produkci.
- Nejsou v projektu balíčky, které se nikde nepoužívají?

## Struktura výstupu

```
## Verdikt
Jedna věta: můžu to pustit do světa, nebo ne?

## P0 — Kritické, opravit před nasazením
- **[Nález]** — `soubor:řádek`
  Riziko: co konkrétně se může stát
  Oprava: ...

## P1 — Opravit brzy
(stejný formát)

## P2 — Dobrá praxe do budoucna
(stejný formát)

## Zkontrolováno a v pořádku
Krátký seznam — ať je vidět, co bylo prověřeno.

## Neověřeno
Co jsem nemohl zkontrolovat z kódu (např. nastavení na hostingu).
```

## Zásady

- **Priorita podle reálného dopadu.** Uniklý klíč od placeného API nebo přístup do cizích dat je P0. Chybějící security hlavička na osobním portfoliu je P2.
- **Nestraš teorií.** Nepiš o hrozbách, které se daného projektu netýkají.
- **U uniklého klíče vždy tři kroky:** 1) zneplatnit a vygenerovat nový, 2) odstranit z kódu a přesunout do `.env`, 3) ověřit `.gitignore` a historii gitu.
- **Nikdy nevypisuj celou hodnotu nalezeného secretu** — ukaž jen prvních pár znaků a cestu k souboru.
- Když je vše v pořádku, řekni to jasně. Nevymýšlej nálezy, aby audit vypadal užitečněji.
