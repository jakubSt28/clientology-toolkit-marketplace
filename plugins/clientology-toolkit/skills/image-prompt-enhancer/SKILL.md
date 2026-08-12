---
name: image-prompt-enhancer
description: >-
  Rewrites a user's rough image idea into a highly detailed English image-generation
  prompt across multiple visual styles. Use when the user asks to improve an image
  prompt, enhance a generation brief, prepare an image prompt for Midjourney/DALL-E/Flux,
  or mentions vibecoding image creation. Styles: Hyperrealistic Photo; Studio Ghibli /
  Retro Anime; 3D Pixar / Glossy Render; Flat 2D / Modern Vector; Whiteboard / Sketch
  Doodling. Always ask which style to use before writing the final prompt.
---

# Image Prompt Enhancer (Multi-Style)

Transform a rough image idea into a **highly detailed English prompt** optimized for AI image generators. Support five styles. Never invent a final prompt until the user picks a style.

## Mandatory workflow

1. **Receive the user's rough idea** (Czech or English is fine).
2. **STOP and ask which style to use** — before writing any enhanced prompt.
3. After the user picks a style, **rewrite the idea** into a full English prompt using that style's recipe below.
4. **Output only the enhanced English prompt** in a single fenced code block (plus a one-line Czech note of which style was used, if helpful). Do not generate the image unless the user explicitly asks.

### Style picker (required) — MUST use AskQuestion UI

**Hard rule:** For the style choice you MUST call the `AskQuestion` tool in the same turn you acknowledge the user's idea. This is what renders the clickable checkbox / option cards in Cursor.

**Forbidden:** Do NOT write a numbered/bulleted list of styles in chat prose and ask the user to type a number. That is a failed picker.

**Call AskQuestion exactly like this** (single-select, one question only):

- **prompt / question:** `Jaký vizuální styl mám použít pro prompt?`
- **options (exact labels, in this order):**
  1. `Hyperrealistic Photo`
  2. `Studio Ghibli / Retro Anime`
  3. `3D Pixar / Glossy Render`
  4. `Flat 2D / Modern Vector`
  5. `Whiteboard / Sketch Doodling`

In that first turn: briefly restate the idea in one short sentence, then **immediately** invoke `AskQuestion`. Do not write the enhanced image prompt yet. Wait for the tool result.

**If `AskQuestion` is not in your available tools** (common in some Agent-mode / model combinations):
1. Say one short Czech line: `V tomto módu/modelu nemám AskQuestion (klikací výběr). Přepni na Plan mode, nebo zkus jiný model (Claude / GPT) — jinak napiš název stylu.`
2. Only then fall back to asking in prose — still **no fake checkbox markdown**.
3. Do not pretend the UI exists.

Rules:
- Do **not** assume a style from context, even if the user hint suggests one.
- If the user already named a style in the same message, skip the picker and proceed with that style.
- If they want multiple styles, produce **one separate English prompt per style**.

## Global rules (all styles)

1. **Final prompt language = English only.** User input may be Czech; translate and expand.
2. **Preserve user intent.** Enhance specificity; do not change the subject, story, or meaning.
3. **Make colors explicit.** Name exact colors for clothing, objects, and environment.
4. **Make lighting explicit.** One coherent lighting setup — never vague "nice lighting."
5. **Include aspect ratio** unless the user specified one (default sensible choice per use: `1:1`, `16:9`, or `9:16`).
6. **End with a Strict negatives block** tailored to that style (keeps the generator from drifting).
7. **No brand-infringing celebrity likeness** unless the user explicitly asks for a public figure; prefer descriptive lookalikes.
8. Keep prompts **dense but readable**: short paragraphs + bullet blocks where the style recipe uses them.

## Shared extraction checklist

From the rough idea, lock these before writing:

- [ ] Subject(s) — who/what, age range, role
- [ ] Action / pose
- [ ] Setting / background
- [ ] Mood / emotion
- [ ] Key objects / props
- [ ] Aspect ratio (ask only if critical and missing)
- [ ] Must-keep constraints from the user (text on image, no people, etc.)

Fill gaps with plausible specifics that serve the chosen style. Flag any assumption only if it could change meaning.

---

## Style 1 — Hyperrealistic Photo

Use when the image must look like a real photograph / smartphone capture.

### Structure (always in this order)

1. **Technical foundation** — aspect ratio + realism declaration + subject basics  
2. **Framing & composition** — shot type, crop, camera position, time of day  
3. **Subject details** — pose, expression, hair, clothing materials + colors, accessories  
4. **Skin realism block** (people only)  
5. **Color & light block**  
6. **Camera behavior**  
7. **Overall aesthetic**  
8. **Strict negatives**

### Required blocks

```
Skin realism is the focus:
• Visible pores and fine micro-texture (or clean-but-natural if requested)
• Natural oil sheen only on high points (cheekbone, nose), matte elsewhere
• No symmetry correction
Skin looks healthy and alive — luminous from real light only, not effects.
No retouching, no smoothing, no beauty filters. Natural imperfections preserved.
```

```
Color & light (IMPORTANT):
• Real daylight with slight warmth, not neutral grey
• Natural contrast (not flat, not cinematic)
• Accurate white balance
• True-to-life colors — skin tones rich and dimensional, [colors named]
• No faded, dusty, pastel, or washed-out colors
```

```
Camera behavior: phone-camera realism, slight edge softness, natural focus falloff, subtle sensor grain.
```

```
Strict negatives: faded colors, pastel tones, beige aesthetic, flat lighting, overexposed whites, AI glow, plastic skin, skincare-ad look, studio lighting, cartoon or 3D style, text or logos.
```

### Quality rules
- Color specification is mandatory.
- Skin realism block is non-negotiable for people.
- Prefer documentary / editorial realism over beauty-campaign polish unless asked.

### Mini example

**Input:** `Selfie Asiatky v mikině`  
**Style:** Hyperrealistic Photo  

```
9:16 vertical aspect ratio, ultra-realistic smartphone mirror selfie of a South Asian woman in her late 20s, taken indoors near a window during daytime. Close-up from collarbone to top of head. She holds a phone partially covering one side of her face, calm neutral expression. Dark hair tied back with loose flyaways. Light grey cotton hoodie with true fabric texture. Small silver stud earrings.

Skin realism is the focus:
• Visible pores and fine micro-texture
• Uneven pigmentation and subtle redness
• Natural oil sheen only on high points, matte elsewhere
• No symmetry correction

Color & light (IMPORTANT):
• Real daylight with slight warmth
• Natural contrast, accurate white balance
• True-to-life colors — grey hoodie clearly separated from skin

Camera behavior: phone-camera realism, slight edge softness, natural focus falloff, subtle sensor grain.
Overall aesthetic: modern, clean, intimate, editorial-documentary. Feels like a real person, real skin, real moment.
Strict negatives: faded colors, pastel tones, beige aesthetic, flat lighting, overexposed whites, AI glow, plastic skin, studio lighting, cartoon or 3D style, text or logos.
```

---

## Style 2 — Studio Ghibli / Retro Anime

Hand-painted anime still: soft atmospheric worlds, gentle characters, nostalgic warmth — closer to classic Ghibli / 80s–90s anime cel than modern hard-line webtoon.

### Structure

1. Aspect ratio + style declaration  
2. Scene & atmosphere (weather, time, air)  
3. Subject(s) — soft features, expressive eyes, simple appealing design  
4. Environment — layered depth, lived-in detail  
5. Color & light — watercolor-adjacent palettes, luminous skies  
6. Medium cues — hand-painted backgrounds, subtle film grain / cel shading  
7. Strict negatives  

### Style declaration (include early)

```
Studio Ghibli-inspired hand-painted anime still, retro 1980s–1990s anime aesthetic, soft watercolor backgrounds, gentle cel shading, nostalgic atmosphere, whimsical but grounded
```

### Required cues
- Soft, rounded character design; large expressive eyes without modern ultra-gloss “AI anime” look
- Backgrounds rich with small lived-in details (tools, plants, dishes, wind in grass)
- Wind, light particles, or quiet motion often help
- Palette: warm greens, sky blues, soft ambers — never neon cyberpunk unless asked

### Strict negatives

```
Strict negatives: photorealistic skin, CGI, 3D render, modern webtoon hard ink, oversharped lines, neon cyberpunk colors, uncanny realism, busy UI, text, logos, deep-fried contrast.
```

### Mini example

**Input:** `Dívka na kole u venkovského nádraží při západu slunce`

```
16:9 aspect ratio, Studio Ghibli-inspired hand-painted anime still, retro 1980s–1990s anime aesthetic. A young girl with short windblown brown hair rides a simple bicycle past a small rural train station at sunset. Soft cel-shaded character, gentle expression, red cardigan over a white dress. Hand-painted watercolor background: wooden station building, telephone wires, tall summer grass, warm amber sky with soft clouds. Quiet nostalgic mood, subtle film grain, luminous air.
Strict negatives: photorealistic skin, CGI, 3D render, modern webtoon hard ink, neon colors, text, logos.
```

---

## Style 3 — 3D Pixar / Glossy Render

Appeal-driven 3D character / scene like a high-end animated feature still: rounded forms, subsurface skin, big readable emotions, cinematic studio lighting, glossy materials.

### Structure

1. Aspect ratio + style declaration  
2. Camera & composition (hero angle, shallow depth feel)  
3. Character design — proportions, face appeal, materials  
4. Props / set dressing — toy-like clarity, readable silhouettes  
5. Material & shader block  
6. Cinematic lighting block  
7. Strict negatives  

### Style declaration

```
Pixar-style 3D animated still, high-end glossy CGI render, appealing stylized proportions, subsurface scattering skin, soft global illumination, cinematic film lighting, octane/redshift quality
```

### Material block

```
Materials:
• Soft subsurface skin with gentle cheek bloom
• Glossy plastic / vinyl accents where appropriate
• Fabric with subtle weave, not photoreal pores
• Eyes glassy with crisp catchlights
• Clean, premium animation-studio finish
```

### Lighting block

```
Lighting:
• Key + soft fill + rim light separating subject from background
• Warm practicals or colorful bounce for emotional tone
• Soft contact shadows; no harsh documentary flash
```

### Strict negatives

```
Strict negatives: photoreal human pores, uncanny valley, horror distortion, flat 2D vector, anime cel, sketch lines, muddy materials, overexposed bloom, text, logos, low-poly game asset look.
```

### Mini example

**Input:** `Robot kuchář s nerezovou čepicí v pastelové kuchyni`

```
1:1 aspect ratio, Pixar-style 3D animated still, high-end glossy CGI render. Cute round robot chef with big expressive eyes and a polished stainless-steel toque, holding a wooden spoon. Pastel mint kitchen set with oversized utensils, soft bounce light, rim light on metal surfaces, subsurface warmth on cheeks.
Materials: soft SSS skin-like face panels, glossy enamel body, brushed steel hat, fabric apron weave.
Strict negatives: photoreal pores, uncanny valley, flat vector, anime cel, sketch lines, text, logos, low-poly look.
```

---

## Style 4 — Flat 2D / Modern Vector

Clean contemporary illustration: limited palette, crisp shapes, minimal gradients, poster/UI/explainer friendly.

### Structure

1. Aspect ratio + style declaration  
2. Composition — strong silhouette, clear hierarchy  
3. Subject — geometric simplification, consistent stroke (or no stroke)  
4. Palette — 3–5 named colors max  
5. Background — flat fields, soft geometric props  
6. Strict negatives  

### Style declaration

```
Flat 2D modern vector illustration, clean geometric shapes, limited color palette, crisp edges, minimal shading, contemporary editorial / product-illustration style
```

### Required cues
- Explicit palette list (e.g., “coral #FF6B5A, ink navy, off-white, soft sage”)
- Consistent corner radius / stroke weight if outlines are used
- Negative space as a design element
- No noisy texture unless asked

### Strict negatives

```
Strict negatives: photorealism, heavy gradients, 3D render, skeuomorphism, anime eyes, sketchy pencil lines, cluttered detail, noisy textures, drop shadows stacked, text, logos (unless user requested text).
```

### Mini example

**Input:** `Tým u whiteboardu řeší customer journey`

```
16:9 aspect ratio, flat 2D modern vector illustration, clean geometric shapes, limited palette: coral, ink navy, soft sage, off-white. Four simplified people at a large whiteboard with journey-map sticky notes, crisp silhouettes, minimal shading, generous negative space, contemporary editorial explainer style.
Strict negatives: photorealism, 3D render, heavy gradients, anime eyes, sketch lines, clutter, text (except tiny unreadable marks), logos.
```

---

## Style 5 — Whiteboard / Sketch Doodling

Looks like a facilitator drew it live: marker lines, imperfect handwriting energy, stick-adjacent but readable figures, paper tooth / dry-erase vibe.

### Structure

1. Aspect ratio + style declaration  
2. Surface — whiteboard or notebook paper  
3. Drawing language — marker weight, hatching, arrows, underlines  
4. Content layout — left-to-right or hub-and-spoke clarity  
5. Color — mostly black marker + 1–2 accent markers  
6. Strict negatives  

### Style declaration

```
Whiteboard sketch doodle, hand-drawn marker illustration on a clean white board, imperfect human linework, lively workshop energy, simple iconic figures, arrows and annotations
```

### Required cues
- Wobbly but confident lines; slight overlap; not CAD-perfect
- Simple faces (dots/arcs), not detailed portraits
- Optional: “black dry-erase marker with blue and orange accents”
- If concepts are labeled, keep labels short English words the user asked for; otherwise prefer icons + arrows without readable paragraphs

### Strict negatives

```
Strict negatives: photorealism, polished vector UI, 3D glossy render, anime, Pixar CGI, perfect symmetric geometry, dense paragraphs of fake lorem text, neon cyberpunk, photographic shadows.
```

### Mini example

**Input:** `Funnel: awareness → consideration → purchase`

```
16:9 aspect ratio, whiteboard sketch doodle in black dry-erase marker with orange accent arrows on a clean white board. Hand-drawn three-stage funnel labeled Awareness, Consideration, Purchase, imperfect linework, simple stick-adjacent people icons, hatching for shading, lively workshop energy, slight marker texture.
Strict negatives: photorealism, polished vector, 3D render, anime, Pixar CGI, perfect geometry, dense fake text, photographic shadows.
```

---

## Output format

After style selection, reply with:

1. One short line: `Styl: [chosen style]`
2. The full English prompt inside a single markdown code block
3. Optional: 2–4 bullet “assumptions” only if you filled meaningful gaps

Do not add long essays. Do not generate the image unless asked.

## Quality checklist (before sending)

- [ ] Style was confirmed via `AskQuestion` UI (or unambiguously stated by user) — not via a typed numbered list
- [ ] Prompt is fully English
- [ ] Aspect ratio present
- [ ] Style declaration matches the chosen recipe
- [ ] Colors named; lighting specific
- [ ] User’s core subject/action preserved
- [ ] Style-appropriate negatives included
- [ ] No mixed-style contradictions (e.g., “photoreal pores” inside Pixar)
