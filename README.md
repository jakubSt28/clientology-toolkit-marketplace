# Clientology Toolkit Marketplace

Cursor marketplace with Clientology skills. Add this GitHub URL in Cursor and install the **Clientology Toolkit** plugin.

**Repo:** https://github.com/jakubSt28/clientology-toolkit-marketplace

## How to add in Cursor

1. Open **Cursor Settings → Plugins** (or **Customize → Plugins / Marketplace**).
2. Add / import a marketplace from a GitHub URL.
3. Paste: `https://github.com/jakubSt28/clientology-toolkit-marketplace`
4. Install **Clientology Toolkit**.

Team / Enterprise admins can also import it under [cursor.com/dashboard](https://cursor.com/dashboard) → **Settings → Plugins → Team Marketplaces → Import**.

## What’s inside

One plugin: `clientology-toolkit`

- **Publikuj změny** — commits and pushes to GitHub for non-technical users
- **Ďáblův advokát** — ruthless critical feedback
- **Image Prompt Enhancer** — multi-style English image-generation prompts
- **Design audit** — design, UX and accessibility review
- **Security basics check** — secrets, exposed endpoints, input validation
- **Responsive check** — mobile and tablet issues
- **SEO + GEO audit** — search engines and AI answer engines

Plus one always-on rule:

- **Netechnický uživatel** — keeps the agent in plain Czech, no jargon, runs technical steps itself

## Repo layout

```text
.cursor-plugin/
  marketplace.json
plugins/
  clientology-toolkit/
    .cursor-plugin/plugin.json
    rules/
      netechnicky-uzivatel.mdc
    skills/
      publikuj-zmeny/SKILL.md
      dabluv-advokat/SKILL.md
      image-prompt-enhancer/SKILL.md
      design-audit/SKILL.md
      security-basics-check/SKILL.md
      responsive-check/SKILL.md
      seo-geo-audit/SKILL.md
    assets/brand-v2.png
```

## Add another skill later

1. Create `plugins/clientology-toolkit/skills/<skill-name>/SKILL.md` (YAML frontmatter with `name` + `description`).
2. Commit and push to `main`.
3. Refresh / re-import the marketplace in Cursor if it doesn’t update automatically.
