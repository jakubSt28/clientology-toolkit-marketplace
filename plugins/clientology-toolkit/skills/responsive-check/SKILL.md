---
name: responsive-check
description: Zkontroluje, jak web funguje na mobilu a tabletu — horizontální přetékání, čitelnost textu, velikost klikacích ploch, navigace a hamburger menu, obrázky, tabulky, sticky prvky a bezpečné zóny. Použij tento skill, když uživatel žádá o kontrolu mobilní verze, responzivity, ptá se "funguje to na mobilu?", "na telefonu je to rozbité", "zkontroluj mi responsive", nebo řeší breakpointy, media queries a mobilní zobrazení.
---

# Responsive / mobile check

Kontrola, co se na malých displejích rozbije. Většina lidí přijde na web z mobilu, takže tohle se řeší dřív než detaily na desktopu.

## Postup

1. **Přečti kód** — komponenty, Tailwind breakpointy (`sm:`, `md:`, `lg:`), media queries v CSS, layout soubory.
2. **Ověř `<meta name="viewport">`** v `layout.tsx` / `index.html`. Bez něj responzivita nefunguje vůbec a je to automaticky P0.
3. **Když web běží**, otevři ho v prohlížeči a projdi tři šířky: **375 px** (menší mobil), **768 px** (tablet), **1440 px** (desktop). U mobilní šířky udělej screenshot.
4. **Aktivně hledej horizontální scroll** — nejčastější a nejviditelnější mobilní chyba.
5. **Vypiš nálezy** podle struktury níže, u každého konkrétní šířku, kde problém nastává.
6. **Nabídni opravu** P0 a P1 nálezů.

## Checklist

### Přetékání a šířky (nejčastější problém)
- Existuje na 375 px horizontální scroll? Když ano, najdi konkrétní prvek, který ho způsobuje.
- Fixní šířky v px (`width: 600px`) bez `max-width: 100%`.
- Prvky s `min-w-` nebo `whitespace-nowrap`, které se nevejdou.
- Dlouhé nedělitelné texty — URL, e-maily, dlouhá slova bez `break-words`.
- Kontejnery s `w-screen` v kombinaci s paddingem nebo scrollbarem.
- Tabulky bez wrapperu s `overflow-x-auto`.
- Obrázky bez `max-width: 100%` / `w-full`.

### Layout a rozložení
- Zůstává někde vícesloupcový grid na mobilu, kde se sloupce zmáčknou do nečitelna? (`grid-cols-3` bez `grid-cols-1` varianty.)
- Flex řádky, které by se měly na mobilu zabalit (`flex-col` na malých šířkách).
- Padding a margin: má obsah na mobilu odsazení od okrajů, nebo je text nalepený na hranu?
- Neomezeně vysoké prvky nebo `height: 100vh` sekce, kde se obsah nevejde a je odříznutý.

### Typografie na mobilu
- Není základní text menší než 16px? (Pod 16px iOS navíc zoomuje formuláře při kliknutí do inputu.)
- Nadpisy, které jsou na desktopu OK, ale na mobilu zaberou půl obrazovky — mají menší mobilní variantu?
- Nezůstávají `clamp()` nebo `vw` velikosti, které na malé šířce spadnou do nečitelných hodnot?

### Dotykové ovládání
- Mají klikatelné prvky aspoň **44×44 px**? (Malé ikonky, křížky, odkazy v patičce.)
- Nejsou dva klikatelné prvky tak blízko, že se dají snadno přehmátnout?
- Spoléhá se někde na hover? Na mobilu hover neexistuje — je tam varianta pro tap?
- Funguje otevírání a zavírání menu prstem?

### Navigace
- Existuje mobilní navigace, nebo se desktopové menu jen zmáčkne?
- Jde hamburger menu **zavřít**? (Častá chyba: otevře se a nejde ven.)
- Zamyká otevřené menu scrollování pozadí?
- Nepřekrývá sticky nebo fixed header obsah po kliknutí na anchor odkaz?

### Obrázky a média
- Nemají obrázky pevné rozměry, které přetékají?
- Nenačítá se na mobilu obrovský desktopový obrázek? (Pomalé připojení, drahá data.)
- Mají obrázky definovaný poměr stran, aby layout při načítání neposkakoval?
- Jsou videa a iframy (YouTube, mapy) responzivní?

### Formuláře na mobilu
- Jsou inputy dost velké a mají font min. 16px?
- Používají správný `type` a `inputmode`, aby se vyvolala vhodná klávesnice (`type="email"`, `type="tel"`)?
- Nepřekrývá klávesnice tlačítko pro odeslání?

## Struktura výstupu

```
## Verdikt
Jedna věta: použitelné na mobilu, nebo ne?

## P0 — Rozbité na mobilu
- **[Nález]** — `soubor:řádek`, projeví se od šířky X px
  Problém: ...
  Oprava: ...

## P1 — Funguje, ale nepohodlné
(stejný formát)

## P2 — Doladění
(stejný formát)

## Zkontrolováno na šířkách
375 px / 768 px / 1440 px — co bylo v pořádku.
```

## Zásady

- **Vždy uveď šířku**, na které se problém projeví. "Rozbité na mobilu" je nepoužitelná zpětná vazba.
- **Konkrétní oprava, ne obecná rada.** Místo "udělej to responzivní" napiš "přidej `flex-col md:flex-row` na `Hero.tsx:24`".
- **Mobile first.** Když je něco špatně na 375 px i na desktopu, priorita je mobil.
- Když nemůžeš web spustit, řekni jasně, že jde o kontrolu z kódu, a vypiš, co je potřeba ověřit vizuálně.
