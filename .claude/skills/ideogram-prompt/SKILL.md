---
name: ideogram-prompt
description: >-
  Generate Ideogram v4 images with three prompting modes: Verbose prompt
  (natural language, best for scenes, art, and design), JSON prompt (structured
  v4 JSON with MP OFF, best for precise text/color control), or Style
  inspiration (extract a style from reference images and apply it to a new
  subject). Use when the user wants to generate images via the Ideogram MCP
  or asks about v4 prompting best practices.
---

# Ideogram Prompt Skill

Generate Ideogram v4 images using the best prompting strategy for the task.
Three modes — pick one and follow its instructions completely.

---

## Mode Detection

Pick based on the request:

- **Verbose prompt** — default for everything: scenes, portraits, illustrations, design artifacts (logos, posters, covers, packaging), anything where you expand the brief into a rich description
- **JSON prompt** — when the user explicitly needs precise text rendering, exact brand colors, or pixel-level element control
- **Style inspiration** — when the user provides reference images and wants to clone or blend that visual style

Default to **verbose** unless the user specifically asks for structured control or provides reference images. Don't ask which mode — pick and proceed.

---

## v4 Gotchas (apply to ALL modes)

1. **Transparent background** — write `"transparent background"` directly in the prompt or `background` field. Do NOT chain `remove_background` — it 500s.
2. **Grain** — photographic grain wording (`35mm grain`, `ISO noise`, `sensor noise`) renders smooth in v4. Use print language instead: `risograph grain`, `halftone dots`, `dithered noise`, `print noise`.
3. **Aspect ratio** — use `aspect_ratio` (e.g. `"3:2"`, `"4:5"`, `"16:9"`), not resolution enums. Many enum values are rejected by the backend.
4. **Lossless URLs** — the MCP returns preview URLs with `balanced` in the path. Swap `balanced` → `lossless` to get full resolution.

---

## Verbose Prompt

Use for: scenes, portraits, illustrations, paintings, design artifacts, logos, posters, packaging — anything where Ideogram's enrichment is welcome.

### Creative mandate

Every brief has a default rendering — the obvious angle, the safe palette, the centered subject in comfortable neutral light. That is not the goal. Before writing anything, ask what the mediocre version looks like, then pick something more specific and alive. Commit to every decision; don't hedge with "slightly" or "perhaps." A specific wrong choice is better than a vague correct one — the renderer fills vagueness with noise.

Don't mutate what the user named. Enrich the scene around subjects, but don't add new characters, change what something IS, or humanize non-human subjects. Treat headline/slogan text as typography only — "COFFEE DUDE" over a cat means render the cat and the words, not a cat holding a mug.

### Write in this order

1. **Medium first** — open with the physical medium and its surface character before any subject. "An oil painting on linen canvas, thick impasto in the lights, thinly glazed darks —" not "A painting of..." Include the artifact of the process: brushstroke direction, grain density, halftone coarseness, ink bleed.

2. **Focal point** — state it explicitly: "X is the focal point." One thing only.

3. **Elements** — for each major element: position in frame, how light acts on its surface (not material names), specific color (named or hex), scale relative to frame, state or action.

4. **Light** — ONE specific source with direction and shadow geometry. "Raking side light from the left, throwing long hard shadows to the right." Not "dramatic lighting."

5. **Atmosphere** — grain, haze, moisture, dust. Clear flat air is the absence of atmosphere.

### Compositional fidelity — run as a checklist before outputting

**Frame coverage.** Tell the model what occupies every region — subject, surroundings, background, negative space. "A woman with flowing hair" leaves the frame to chance. "Figure centered against a dark seamless background extending to all edges" does not. If a region is intentionally empty, say so: "plain void behind," "negative space above."

**Scale.** When a figure exists inside an environment, state the scale relationship. Without it, the model either fills the frame with the figure or reduces it to a speck. "Figure occupies the lower-center third; the vaulted ceiling extends up and around her into the distance."

**Text surfaces.** Any surface that could carry text — clothing, labels, signs, walls, screens, packaging — must either receive exact content or be explicitly cleared. "Shirt reading exactly 'THE HAMPTONS'" or "blank shirt, no text." An emphasized undefined text surface is a structural failure.

**Material behavior.** Describe how light acts on surfaces, not material names. "Denim with crisp white highlight threads along fold ridges" not "denim jacket." "Glass catching a bright caustic streak along one side" not "glass bottle."

**Coherence.** Conflicting signals don't average — the model picks. Check: tight crop + elaborate background, full figure + extreme portrait crop, subject fills frame + deep environment, minimalist + dense. Resolve toward dominant intent.

### Quality rules

- Be specific enough that the fragment could only describe one image. "Car on road" → "1967 Mustang on cracked desert two-lane."
- Palette: push unexpected. A wolf doesn't have to be grey; a night scene doesn't have to be cool blue-grey.
- Framing: full subject centered is the absence of a decision. Tighter crop, lower angle, unexpected proximity is almost always more alive.
- No filler adjectives. "Beautiful," "stunning," "dramatic" mean nothing. Name what makes it those things.
- State what the image IS doing. "The face dissolves into falling data at the bottom" is actionable. "A cool futuristic portrait" is not.

### When the brief is thin

Expand before generating. Commit ALL of these:
- A named, limited palette that makes the subject feel surprising (not its obvious natural hues)
- A specific medium + art movement/era ("woodcut illustration", "1970s psychedelic", "Art Deco geometric") + the medium's surface character
- ONE specific light source with direction and shadow geometry
- A compositional principle (centered, rule of thirds, radial, diagonal, vertical stack) — not the absence of one. IMPORTANT: these describe element arrangement on the canvas, not physical world geometry — "vertical stack" = headline above image above subhead, not objects physically stacked in the scene
- Setting: a coherent environment for scenes; isolated design artifacts (logo, sticker, transparent-background) stay on a plain ground

For **photoreal people**: build a specific candid moment in a real context — mid-gesture, mid-laugh, mid-task — not a posed line-up. Name the expression. Prefer natural available light over flat studio-bright perfection.

### Design artifacts

For designed artifacts (logos, posters, covers, packaging, t-shirt graphics, stickers): you are the art director, not just the describer. Make opinionated choices. The default is the enemy — name the expected interpretation, then reject it.

**Aspect ratio by format** (unless user specifies): posters, book covers, flyers → portrait (2:3, 3:4); album covers (vinyl/EP/CD/streaming) → square (1:1), always; banners, slides → landscape (16:9); magazine spreads → landscape (3:2); t-shirt/sticker/logo → square (1:1); social → 1:1 or 4:5; stories → 9:16.

**Typography.** Pair two complementary typefaces — a distinctive display/headline face + a clean secondary. Build a clear scale hierarchy: headline large and dominant (a real frame-filling element, not a caption), subhead smaller, body smallest. Spell out every text run concretely with the exact words, typeface category + weight, color, and effect (3D extrusion, drop shadow, arched, stacked). Type is not a polite label floating above the subject — it collides with it, competes with it, or frames it.

**Typeface vocabulary** — use these specific terms rather than generic "serif" or "sans":
Didone (extreme stroke contrast, cold precision), Slab/Egyptian (heavy square serifs, authoritative), Old-style humanist serif (low contrast, warm), Grotesque (early-20th-century sans, slight irregularity), Geometric sans (circles and bars, Bauhaus), Humanist sans (editorial, friendly), Ultra-condensed grotesque (gig-poster density), Blackletter (gothic, alt-weekly), Stencil (military/streetwear), Woodblock display (letterpress folk), Brush script (visible bristle, fast rhythm), Monospaced typewriter (bureaucratic-mechanical), Deconstructed/experimental (rules violated intentionally).

**Fill the canvas.** Posters, covers, packaging should read dense and edge-to-edge — headline, supporting subjects, decorative accents. Large empty margins = unfinished. Exception: t-shirt/sticker/logo → a contained centered motif with clear margin on all sides, never bled to canvas edges, on a plain solid ground.

**Logotypes** — pick the mark type and name it:
- Wordmark — brand name in a chosen typeface, no separate icon
- Lettermark/monogram — initials only, icon-like
- Symbol/icon — non-typographic mark, name set separately below
- Combination mark — symbol + wordmark locked together
- Emblem — text and symbol integrated inside a containing shape (badge, seal, crest)

Brand register → typeface: luxury/fashion → Didone or old-style humanist; tech/SaaS → geometric or extended grotesque; craft/artisan → woodblock, slab, brush script; heritage/institutional → old-style serif, blackletter; youth/street → blackletter, stencil, ultra-condensed grotesque; playful/consumer → brush script, rounded geometric.

After naming the mark type: state the lock-up composition (stacked vs horizontal vs contained), the negative space ratio (air around the mark), and palette with hex codes.

**Flat-graphic negatives** — for flat illustration/screen-print/vector: add "no photoreal, no naturalistic gradients, flat graphic lighting" so the renderer doesn't drift to realism. Do NOT add these to subjects that need dimensionality: NEON signs, chrome, glass, liquid, luminous subjects.

**NEON** → glowing glass tubes with halo/bloom, dimensional tubing, dark surround — NOT a flat vector icon. NEON overrides any logo/flat-graphic default.

---

## JSON Prompt

Use for: exact text rendering, brand-consistent colors, precise element placement, or when magic prompt enrichment would fight your intent.

Call `generate_image` with the prompt as minified JSON and `magic_prompt_option: "OFF"`.

**v4 JSON structure** (key order is strict — the model was trained on this exact sequence):

```json
{
  "style_description": {
    "medium": "photograph | digital illustration | vector art | 3D render | oil painting | watercolor | ink drawing | pencil sketch | mixed media | collage",
    "aesthetics": "<colors/palette>, <composition principle>, <mood>",
    "photo": "<depth of field, focus, angle, lens> — null for non-photo",
    "art_style": "<named movement/era + style> — null for photos",
    "lighting": "<conditions>, <direction>, <shadows>",
    "color_palette": ["#RRGGBB", "#RRGGBB"]
  },
  "high_level_description": "Natural sentences — as many as needed — carrying medium, grain/surface treatment, palette, mood, and composition. This field survives to the image model. Load it.",
  "compositional_deconstruction": {
    "background": "Setting, atmosphere, lighting, palette, grain/film treatment, spatial layout — natural prose. Atmospheric components always go here. This field survives.",
    "elements": [
      {"type": "obj", "desc": "One distinct subject — identity, position in frame, relative size, material light behavior (not material names), surface colors, texture, orientation.", "color_palette": ["#RRGGBB"]},
      {"type": "text", "text": "VERBATIM\nTEXT", "desc": "Size/hierarchy, position/layout, typeface category + weight, color, effects."}
    ]
  }
}
```

**Critical:** `style_description` is discarded before the image model sees it — except `color_palette`, which IS live. Repeat all style detail in `high_level_description` and `background`. Never put a detail only in `style_description`.

**Key ordering:** top-level: `style_description` → `high_level_description` → `compositional_deconstruction`. Within `style_description`: `medium` → `aesthetics` → `photo`/`art_style` → `lighting` → `color_palette`.

**`bbox` coordinates** — `[y_min, x_min, y_max, x_max]` in normalized 0–1000 units, origin top-left. y: 0=top, 1000=bottom. x: 0=left, 1000=right. A full-width band near the top: `[80, 100, 180, 900]`. Optional — omit when you don't need precise placement.

**`color_palette` steering:**
- `style_description.color_palette`: up to 16 uppercase hex colors — steers the dominant image palette
- `elements[*].color_palette`: up to 5 hex per element — controls that element's color
- Always uppercase: `#1B1B2F` not `#1b1b2f`

**Rules:**
- `high_level_description` and `background` are the primary fields — put style detail here, not only in `style_description`
- One subject = one element; its parts are attributes within its `desc`
- `text` field holds REAL words — never a description ("a compelling headline" → write the actual words)
- Multi-line text: `\n` inside the string. Each text string appears exactly ONCE
- Transparent background → `"background": "transparent background"` (also say so in `high_level_description`)
- For grain: `risograph grain`, `halftone dots`, `dithered noise` in `aesthetics` and `background`
- Minify when passing to the MCP (no extra whitespace)

---

## Style Inspiration

Use for: cloning or blending a visual style from reference images and applying it to a new subject.

1. **Collect references.** Accept file paths, attachments, or URLs. Hard cap: 10 images.

2. **Describe each reference** via `describe_image` (Ideogram MCP). If unavailable, caption each across: medium, palette, grain/texture, lighting, composition, mark-making, mood.

3. **Distill a style recipe:**
```json
{
  "medium": "...",
  "palette": "...",
  "grain_texture": "...",
  "lighting": "...",
  "composition": "...",
  "mark_making": "...",
  "mood": "...",
  "prompt_additions": "prose additions encoding this style — e.g. 'Heavy grain across the whole surface, most visible in shadow areas. Slight misregistration between the two ink colors at figure edges.'"
}
```

4. **Apply to the user's subject.** Build v4 JSON embedding the recipe's palette, medium, grain, lighting, and composition into `high_level_description` and `background`.

5. **Generate** with `aspect_ratio` matching references (or user preference), `model: "V_4"`.

6. **Offer to save the recipe** — output it in a code block so the user can paste it into future sessions.

---

## Few-Shot Examples

**Scene:**
Brief: "delorean at sunset"
Prompt: `A photograph — wide golden-hour light from just left of center, the sun barely above the horizon, warm bronze raking light catching the DeLorean's stainless-steel body along panel edges, deep shadow pooling in the door seams. Fine warm-toned grain, slight bloom around the brightest specular hits. The car sits centered in the lower half on dark desert tarmac, a vanishing-point highway stretching behind it to the horizon. Joshua trees line both shoulders, their silhouettes sharp against a pink-to-amber gradient sky filling the full upper third. The flux capacitor bleeds soft blue glow through the grill vents. A dust trail hangs in the air behind the car. The license plate reads exactly 'OUTATIME'. Heat shimmer rises off the asphalt ahead of the bumper.`
Ratio: 16:9

**Design artifact:**
Brief: "gig poster for punk band NERVE DAMAGE"
Prompt: `A screen-print gig poster — three-color risograph, registration slightly off between the neon pink and black layers, magenta fringe visible at letter edges where colors overlap. Vertical stack composition filling the canvas edge to edge: the headline 'NERVE DAMAGE' set in ultra-condensed stencil capitals, bone-white, two rows, letters touching — fills the full width with zero margin. A dominant front-facing skull occupies the central third: bone-white, hollow eye sockets, a neon pink jagged lightning bolt lodged behind the cranium. Below: 'WITH THE WIRE MOTHERS' in condensed grotesque caps, neon pink, a single tight row. At the foot: 'SAT 14 MAR / THE ECHO, LOS ANGELES / DOORS 8PM / $12 ADV' in monospaced typewriter face, all-caps, very small, stacked in a tight block. Background: flat inky black with coarse halftone dot pattern, dots coarsening into corners. No photographic texture — flat graphic throughout. Palette: black field, bone white, neon pink #FF2D6A.`
Ratio: 2:3

**Logo:**
Brief: "minimal logo for coffee shop called Dusk"
Prompt: `A flat vector illustration in two-tone black on cream — a single coffee cup silhouette centered with generous margin on all sides, a thin crescent moon nested within the steam wisp rising from the cup, clean geometric linework throughout. The mark occupies roughly half the square frame, cream field extending uniformly to all four edges. The logotype reading exactly 'DUSK' appears in lightweight geometric sans-serif capitals beneath the mark, evenly letter-spaced and centered. No other text, no background decoration, no drop shadow, no depth — just the mark on clean cream.`
Ratio: 1:1

---

## After Generation

Always:
- Show the image inline
- Offer to iterate: different ratio, more or less detail, re-run for variation
- Offer to switch modes if results aren't precise enough (verbose → JSON for text fidelity; JSON → verbose for style richness)
- Remind: swap `balanced` → `lossless` in the returned URL for full resolution
