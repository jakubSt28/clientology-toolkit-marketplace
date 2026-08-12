---
name: design-audit
description: Provede kritický design a UX audit webu nebo stránky včetně přístupnosti (accessibility) — vizuální hierarchie, typografie, barvy, kontrasty, CTA, alt texty, focus stavy, struktura nadpisů. Použij tento skill, když uživatel žádá o design audit, revizi designu, kontrolu UX, zhodnocení vzhledu stránky, kontrolu přístupnosti / accessibility / a11y, nebo říká věci jako "vypadá to nějak divně", "je to takové generické", "zkontroluj mi design", "co zlepšit na vzhledu", "projdi mi tu landing page".
---

# Design audit (s accessibility)

Kritický audit designu, UX a přístupnosti. Cílem není chválit, ale najít konkrétní věci, které zhoršují dojem nebo použitelnost, a navrhnout opravu.

## Postup

1. **Zjisti, co auditovat.** Konkrétní stránka/komponenta, nebo celý web? Když to není jasné, vezmi hlavní stránku (`page.tsx`, `index.html`, `App.tsx` apod.).
2. **Přečti skutečný kód** — komponenty, styly, Tailwind classy, globální CSS, design tokeny. Nikdy nehádej podle názvu souboru.
3. **Když je web spuštěný**, podívej se na něj v prohlížeči a udělej screenshot (desktop). Vizuální kontrola odhalí věci, které z kódu nepoznáš.
4. **Projdi checklist** níže a zapisuj jen skutečné nálezy s odkazem na soubor a řádek.
5. **Vypiš výstup** ve struktuře uvedené dál.
6. **Na konci se zeptej**, jestli má agent P0 a P1 nálezy hned opravit.

Nevymýšlej si problémy, které v kódu nejsou. Když něco nemůžeš ověřit, napiš to jako "neověřeno" místo tvrzení.

## Checklist

### Vizuální hierarchie
- Je na první pohled jasné, co je nejdůležitější prvek stránky?
- Kolik různých velikostí písma a barev se používá? (Víc než 4–5 velikostí = chaos.)
- Dýchá to? Nebo je všechno nalepené na sobě (chybí padding, margin, whitespace)?
- Je hlavní CTA vizuálně nejvýraznější prvek, nebo se ztrácí?

### Typografie
- Kolik fontů? (Víc než dva = obvykle chyba.)
- Řádkování u delších textů (ideálně 1.5–1.7 u odstavců).
- Délka řádku — nad ~90 znaků se text čte špatně.
- Je velikost základního textu aspoň 16px?

### Barvy a kontrast
- Má web soudržnou paletu, nebo se barvy náhodně mění mezi sekcemi?
- **Kontrast textu vůči pozadí:** běžný text min. 4.5:1, velký text min. 3:1. Spočítej to u hlavních kombinací a napiš konkrétní čísla.
- Nese informaci pouze barva? (Např. chyba formuláře jen červeným rámečkem bez textu = problém.)

### Generičnost (AI vygenerovaný vzhled)
- Vypadá to jako každá druhá AI šablona? (Fialový gradient, tři karty s ikonkami, vágní nadpis typu "Elevate your workflow".)
- Řekne nadpis konkrétně, co produkt dělá, nebo je to prázdná fráze?
- Jsou v textech placeholdery, lorem ipsum, nebo nedopsané pasáže?

### UX a interakce
- Pochopí návštěvník do 5 sekund, co to je a co má udělat?
- Mají klikatelné prvky hover a active stav? Je poznat, že jsou klikatelné?
- Má formulář jasné labely, viditelné chybové stavy a stav při odesílání?
- Co se stane při prázdném stavu, chybě, dlouhém načítání? Existuje pro to vůbec něco?

### Přístupnost (accessibility)
- **Alt texty:** má každý `<img>` smysluplný `alt`? Dekorativní obrázky mají `alt=""`.
- **Struktura nadpisů:** jeden `<h1>` na stránku, žádné přeskakování úrovní (h1 → h3).
- **Focus stavy:** je vidět, kde je klávesnicový focus? Není někde `outline: none` bez náhrady?
- **Sémantika:** používají se `<button>`, `<a>`, `<nav>`, `<main>`, nebo je všechno `<div>` s onClickem?
- **Klikací plochy:** interaktivní prvky min. 44×44 px (hlavně na mobilu).
- **Ikony bez textu:** mají `aria-label`?
- **Formuláře:** je každý input svázaný s labelem (`htmlFor` / `id`)?
- **Jazyk stránky:** má `<html>` správný `lang` (u českého webu `lang="cs"`)?

## Struktura výstupu

Piš stručně a konkrétně. U každého nálezu: co je špatně, kde to je, proč to vadí, jak to opravit.

```
## Celkový dojem
2–3 věty. Přímo. Co je největší problém.

## P0 — Opravit hned
- **[Nález]** — `soubor:řádek`
  Problém: ...
  Oprava: ...

## P1 — Výrazně to zlepší
(stejný formát)

## P2 — Detaily a vychytávky
(stejný formát)

## Co funguje
Max 3 body. Jen když si to opravdu zaslouží.
```

Řazení podle dopadu, ne podle pořadí v kódu:
- **P0** — blokuje použití nebo kazí první dojem (nečitelný text, rozbité rozložení, chybějící CTA, nedostatečný kontrast).
- **P1** — funguje to, ale vypadá to amatérsky nebo to zbytečně zdržuje uživatele.
- **P2** — jemné doladění.

## Tón

Přímý a konkrétní, bez omáčky. Místo "mohlo by to být čitelnější" napiš "šedý text `#9CA3AF` na bílém pozadí má kontrast 2.8:1, což je pod minimem 4.5:1 — použij `#4B5563`".

Nezačínej chválou. Když je něco vážně špatně, řekni to.
