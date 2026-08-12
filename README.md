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

- **Ďáblův advokát** — ruthless critical feedback
- **Image Prompt Enhancer** — multi-style English image-generation prompts

## Repo layout

```text
.cursor-plugin/
  marketplace.json
plugins/
  clientology-toolkit/
    .cursor-plugin/plugin.json
    skills/
      dabluv-advokat/SKILL.md
      image-prompt-enhancer/SKILL.md
    assets/logo.svg
```

## Add another skill later

1. Create `plugins/clientology-toolkit/skills/<skill-name>/SKILL.md` (YAML frontmatter with `name` + `description`).
2. Commit and push to `main`.
3. Refresh / re-import the marketplace in Cursor if it doesn’t update automatically.
