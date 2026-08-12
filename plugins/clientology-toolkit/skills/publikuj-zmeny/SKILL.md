---
name: publikuj-zmeny
description: Uloží a nahraje všechny rozpracované změny do GitHub repozitáře za uživatele — zkontroluje stav, stáhne případné cizí změny, napíše commit zprávu, commitne a pushne, a vše vysvětlí bez git žargonu. Použij tento skill, když uživatel žádá o publikování, uložení nebo nahrání změn, říká věci jako "ulož to", "nahraj to na GitHub", "publikuj změny", "zapiš to", "commitni to", "je všechno nahrané?", "mám to na gitu?", nebo se ptá, jestli má rozpracované věci uložené.
---

# Publikuj změny

Uživatel je začátečník a nezná git. Tvým úkolem je odbavit celý postup za něj a mluvit s ním lidsky — žádné `commit`, `staging area`, `HEAD`, `origin/main`. Prostě "uložím tvoje změny na GitHub".

## Postup

Projdi kroky v tomto pořadí. Nepřeskakuj kontrolu bezpečnosti.

### 1. Zjisti stav

```bash
git status --short
git branch --show-current
git remote -v
git log --oneline -1
```

Podle výsledku pokračuj:

| Situace | Co udělat |
| --- | --- |
| Nejde o git repozitář | Nabídni založení. Postupuj podle sekce "Když ještě nic není". |
| Není nastavený `origin` | Repozitář na GitHubu chybí. Sekce "Když ještě nic není". |
| Žádné změny a nic neodeslaného | Řekni, že je vše uložené, a skonči. Nic nevytvářej. |
| Jsou změny | Pokračuj krokem 2. |

### 2. Bezpečnostní kontrola (nikdy nevynechávej)

Než cokoliv uložíš, projdi seznam souborů, které by se měly nahrát, a hledej:

- `.env`, `.env.local`, `.env.production` a podobné soubory s nastavením
- soubory s klíči a přihlašovacími údaji: `credentials.json`, `*.pem`, `*.key`, `serviceAccount*.json`
- vzory tajných klíčů v obsahu nových změn: `sk-`, `sk_live`, `AIza`, `ghp_`, `xoxb-`, `AKIA`
- složky, které do repozitáře nepatří: `node_modules/`, `.next/`, `dist/`, `build/`
- neobvykle velké soubory (nad 10 MB)

**Když něco takového najdeš:** zastav se, vysvětli lidsky, co to je a proč se to nemá nahrávat na internet, a nabídni přidání do `.gitignore`. Pokračuj až po odpovědi uživatele. Nikdy nenahraj klíče nebo hesla na GitHub, ani když uživatel řekne "prostě nahraj všechno".

### 3. Stáhni změny z GitHubu

Ověř, jestli na GitHubu není něco, co uživatel nemá u sebe:

```bash
git fetch origin
git status -sb
```

- **Nic nového na GitHubu** — pokračuj krokem 4.
- **Na GitHubu jsou novější změny** — stáhni je před nahráním:

```bash
git pull --no-rebase --no-edit origin <branch>
```

- **Nastane konflikt** — zastav se. Neřeš to sám. Vysvětli lidsky: "Ty a někdo další (nebo ty z jiného počítače) jste upravili stejné místo ve stejném souboru. Musíme rozhodnout, která verze platí." Vypiš seznam dotčených souborů a zeptej se, jak postupovat. Teprve po odpovědi konflikt vyřeš a pokračuj.

### 4. Ulož změny

```bash
git add -A
git commit -m "<popis změn>"
```

Commit zprávu **napiš sám** z toho, co se reálně změnilo (`git diff --cached --stat` a obsah změn). Nikdy se uživatele neptej, co tam má napsat — on to neví, to je celý smysl tohohle skillu.

Pravidla pro zprávu:
- V jazyce, kterým s tebou uživatel mluví (píše-li česky, piš česky).
- Jedna věta, konkrétně co se změnilo: "Přidána sekce s cenami na hlavní stránku" místo "update".
- Popisuj věcný obsah, ne názvy souborů.

### 5. Nahraj na GitHub

```bash
git push origin <branch>
```

Když je to úplně první nahrání dané větve:

```bash
git push -u origin <branch>
```

Pokud push selže:
- **Odmítnuto kvůli novějším změnám na GitHubu** — vrať se ke kroku 3, stáhni změny a zkus znovu.
- **Chyba přihlášení** — vysvětli, že se Cursor potřebuje přihlásit k GitHubu, a naveď uživatele. Nezkoušej to obcházet.
- **Nikdy nepoužívej `--force`** ani žádnou variantu, která přepíše historii na GitHubu.

### 6. Potvrď výsledek

Napiš krátké shrnutí bez git termínů:

```
Hotovo — tvoje změny jsou na GitHubu.

Uloženo: [1 věta, co se změnilo]
Souborů: [počet]
Repozitář: [odkaz na GitHub]
```

Když jsi něco vynechal (např. `.env`), zmiň to a řekni proč.

## Když ještě nic není

**Není to git repozitář** (chybí `.git`):

1. Vysvětli, co se stane: "Založím ti historii verzí a nahraju projekt na GitHub."
2. Vytvoř `.gitignore` odpovídající typu projektu, **než** cokoliv přidáš.
3. `git init`, pak krok 2 a 4 z hlavního postupu.
4. Na vytvoření repozitáře na GitHubu potřebuješ `gh`. Ověř `gh auth status`. Když `gh` není k dispozici, řekni uživateli, ať vytvoří prázdný repozitář na [github.com/new](https://github.com/new) a pošle ti odkaz — pak nastavíš `origin` a nahraješ.

**Je to git repozitář, ale chybí `origin`:** stejné jako bod 4 výše.

## Pravidla, která nikdy neporušuj

- **Žádný `push --force`, `reset --hard`, `git clean -fd` ani přepisování historie.** Když se zdá, že by to problém vyřešilo, zastav se a zeptej.
- **Nikdy neměň nastavení gitu** (`git config`) — hlavně ne jméno a e-mail uživatele.
- **Nepřeskakuj hooky** (`--no-verify`).
- **Neupravuj poslední commit** (`--amend`), pokud o to uživatel výslovně nepožádá.
- **Nemazej žádnou práci uživatele**, ani rozpracovanou.
- **Nikdy nenahrávej secrets** — viz krok 2.
- Když si nejsi jistý, **zastav se a vysvětli**, místo hádání. U začátečníka je ztracená práce mnohem horší než jeden dotaz.

## Jak mluvit s uživatelem

| Neříkej | Řekni |
| --- | --- |
| "Commitnu a pushnu na origin/main" | "Uložím tvoje změny a nahraju je na GitHub" |
| "Máš 3 uncommitted changes" | "Máš 3 rozpracované soubory, které nejsou nahrané" |
| "Musíš udělat pull, jsi behind" | "Na GitHubu jsou novější změny, nejdřív je stáhnu k tobě" |
| "Merge conflict v index.html" | "Ve stejném souboru jsou dvě různé verze, musíme vybrat, která platí" |
| "Working tree je clean" | "Všechno máš uložené, není co nahrávat" |
