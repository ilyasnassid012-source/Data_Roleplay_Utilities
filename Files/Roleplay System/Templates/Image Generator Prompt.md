# AI Image Generator Prompt Database & Rule System

**Purpose:** Create detailed, tag-based prompts for AI image generators (CharacterSnap, NovelAI Diffusion, Pony Diffusion, etc.) by structuring visual information hierarchically so that generators understand every element without ambiguity.

**Core Philosophy:** Treat the image generator as if it has zero prior knowledge. Every detail—no matter how small—must be explicitly stated and ordered by generation priority.

---

## 1 FOUNDATIONAL RULES

### 1.1 Universal Tagging Requirements

- **TAG SYSTEM MANDATORY** — Use comma-separated, Danbooru-style tags (e.g., `1girl, long hair, blue eyes`)
- **NO FULL SENTENCES** unless specifying rare dialogue or text elements in images
- **ASSUME ZERO CONTEXT** — The generator knows nothing about any character, location, or style by name alone
- **EXTREME LITERAL INTERPRETATION** — The AI processes every word exactly as written; avoid vague descriptors
  - ❌ "busty" → ✅ "large breasts, D cup"
  - ❌ "gorgeous" → ✅ "beautiful detailed face, symmetrical features"
  - ❌ "fancy clothes" → ✅ "silk white blouse, gold embroidered collar, pearl buttons"

### 1.2 Information Priority & Ordering

**The generator should be told information in this exact sequence** (what comes first gets strongest generation focus):

1. **Quality & Technical Foundation** (masterpiece, best quality, high resolution)
2. **Art Style & Medium** (anime, manga style, watercolor)
3. **Subject Count & Type** (1girl, 1boy, solo, group)
4. **Core Character Appearance** (face, body build, skin, hair color)
5. **Clothing & Accessories** (detailed outfit specifications)
6. **Pose, Action & Expression** (what the character is doing, how they look)
7. **Environment & Location** (detailed setting, architecture, weather)
8. **Lighting, Camera, Composition** (how the scene is lit and framed)
9. **Style Enhancers & Mood** (cinematic, atmospheric, mood descriptors)
10. **Negative Elements** (in separate negative prompt section)

**Why this order matters:** The generator allocates generation weight/attention to early tags. If you place environment first, characters may become blurry or poorly defined. Keep priority-critical elements at the start.

### 1.3 The Generator Knows Nothing Rule

- **Never assume the generator recognizes character names, franchises, or implied details**
- Example: Writing "Sailor Moon uniform" assumes generator knowledge → Instead: "white sailor collar, navy pleated skirt, red ribbon bow, tiara, long hair"
- Describe visual reality, not narrative context
- Exception: Only use character names if the user explicitly requests the name visible as text/watermark (extremely rare)

### 1.4 Assumption of Broken Physics

- **The generator has no default understanding of gravity, anatomy, or realistic joint movement**
- If you want realistic proportions → explicitly state: "realistic anatomy, correct joint placement, anatomically correct"
- If you want gravity-defying hair → explicitly state: "hair defying gravity, floating upward, no physics"
- If unsure, assume the generator will create broken anatomy unless told otherwise

---

## 2 HIERARCHICAL CHAIN TAGGING SYSTEM (Core Structure)

### 2.1 What Are Chains?

A **Chain** is a hierarchical sequence of increasingly detailed tags that builds one element from broad to microscopic detail. Chains prevent vagueness and ensure layered information reaches the generator in logical progression.

**Chain Structure:**

```
[Main Section]: Base category (CHARACTER, CLOTHING, ENVIRONMENT, LIGHTING)
  └─ [Sub Section]: Specific element within the main (Hair, Upper Body, Facial Features)
      └─ [Sub Sub Section]: Micro-details within that element (Texture, Color, Pattern, Adornments)
```

**How Chains Are Written:**

Chains are NOT written as nested bullets in the final prompt. Instead, they flow naturally as comma-separated tags **ordered from broad to specific**, grouped logically with commas and occasional periods for readability.

**Example Chain Breakdown:**

```
CHARACTER
├─ Gender & Age: 1girl, 18 years old, young adult
├─ Body Build: tall, athletic build, slim waist, wide hips
├─ Skin Tone: fair skin, unblemished
└─ Face Detail:
    ├─ beautiful detailed face, symmetrical features
    ├─ amber eyes, large pupils, intense gaze
    └─ small nose, pale lips, high cheekbones

HAIR (Separate Chain)
├─ Length & Style: very long hair, waist-length, straight hair
├─ Color & Texture: jet black, glossy, healthy shine
└─ Details: side bangs, no highlights, flowing naturally
```

**In Final Prompt Format:**
```
1girl, 18 years old, young adult, tall, athletic build, slim waist, wide hips, fair skin, unblemished.
beautiful detailed face, symmetrical features, amber eyes, large pupils, intense gaze, small nose, pale lips, high cheekbones.
very long hair, waist-length, straight hair, jet black, glossy, healthy shine, side bangs, no highlights, flowing naturally.
```

Notice: Each sentence/period groups a related chain, then the next chain begins.

### 2.2 Chain Expansion Rules

**Single Detail Chain** (minimal):
```
[Main Section]: [Base Tag]
```
Example: `background, white`

**Standard Detail Chain** (most common):
```
[Main Section]: [Base Tag], [Sub-Detail], [Sub-Detail]
```
Example: `hair, very long, platinum blonde, wavy texture`

**Complex Detail Chain** (maximum depth):
```
[Main Section]: [Base Tag], [Sub-Detail], [Sub-Detail], [Sub-Detail].
  [Sub Section]: [Micro-Detail], [Micro-Detail], [Micro-Detail].
    [Additional Layer]: [Hyper-Detail], [Hyper-Detail]
```

Example:
```
upper body clothing, white button-up blouse, silk fabric, form-fitting.
collar detail, navy blue trim, gold embroidered edge, shell buttons.
sleeve detail, long sleeves, rolled up to elbow, visible stitching.
```

**Expansion Principle:** 
- Simple elements = 2-3 tags
- Important elements = 4-6 tags
- Complex/focal elements = 7+ tags distributed across sub-chains

The more important something is to the final image, the more detail it deserves.

---

## 3 TAG SYSTEM REFERENCE & BEST PRACTICES

### 3.1 Weighted Emphasis (Critical for Priority)

Use emphasis syntax to force generator focus on key elements:

**Strong Emphasis (Double Braces):**
```
{{very important detail}}
```
Use for: Character's most defining feature, plot-critical element

**Moderate Emphasis (Single Parentheses with Weight):**
```
(important detail:1.3)
(important detail:1.5)
(important detail:1.2)
```
Weight range: 1.1–2.0 (start at 1.2, increase only if critical)

**De-Emphasis (Brackets):**
```
[unwanted element:0.6]
[unwanted element:0.4]
```
Use for: Things the user doesn't want but might accidentally appear

**When to Use Emphasis:**
- Character's signature feature (colored eyes, unique hairstyle)
- Rare or complex visual element
- Element that might be misinterpreted or forgotten
- Critical focal point of composition

**Example with Emphasis:**
```
{{long silver hair}}, {{amber eyes}}, 1girl, solo.
(detailed face:1.3), (high cheekbones:1.2), small nose, pale lips.
```

### 3.2 Essential Quality Tags (Always Start Here)

**Absolute Foundation** (begin every positive prompt with these):
```
masterpiece, best quality, absurdres, ultra-detailed, sharp focus, very aesthetic, high resolution
```

**Why:** These tell the generator to prioritize quality and detail across all elements.

**Conditional Quality Additions:**
- For extreme detail: `extremely detailed, intricate details, finely detailed`
- For artistic quality: `studio quality, professional art, polished`
- For specific style: `concept art quality, illustration, digital art`
- For photorealism (if applicable): `photorealistic, hyperrealistic` (but often conflicts with anime style)

### 3.3 Art Style Tags

**Primary Style (choose ONE or TWO):**
```
anime
detailed anime
vibrant anime
manga style
detailed manga style
manga panel
watercolor
digital art
painted
sketch
cel shaded
chibi
3D rendered (rarely recommended)
realistic anime
studio ghibli
retro 80s anime
cyberpunk neon
steampunk
```

**Style Modifiers (can combine):**
```
highly stylized
soft colors
vibrant colors
saturated colors
pastel colors
dark colors
neon colors
gradient colors
cinematic color grading
color splash
```

**Art Medium Specifiers:**
```
oil painting
acrylic
watercolor
pencil sketch
ink drawing
digital illustration
gouache
```

### 3.4 Character Appearance Chains (Most Complex)

#### Gender & Age Chain
```
1girl (or 1boy, solo, etc.)
[age descriptor: teenage, young adult, adult, mature adult, elderly]
[age appearance: appears 18, appears 25, youthful, mature features]
```

#### Body Build Chain
```
[overall build: petite, slim, athletic, curvy, chubby, muscular, tall and lean]
[height relative: short, average, tall, very tall]
[build specifics: slim waist, wide hips, broad shoulders, flat chest, large breasts, thin legs, thick thighs]
[proportions: hourglass figure, pear-shaped, athletic frame, delicate frame]
[cup size if breasts relevant: flat chest, small breasts (A cup), medium breasts (C cup), large breasts (D cup), very large breasts (F+ cup)]
```

#### Skin Chain
```
[skin tone: pale skin, fair skin, light skin, medium skin, tanned skin, dark skin, olive skin]
[skin condition: smooth skin, unblemished, clear skin, soft skin, porcelain skin]
[skin marks: freckles, moles, beauty marks, scars, tattoos, birthmarks]
[skin features: shiny skin (if appropriate), skin texture emphasis]
```

#### Face Chain (Critical for Recognition)
```
[face quality: beautiful detailed face, gorgeous face, delicate face, sharp features, soft features, symmetrical face, asymmetrical features]
[face shape: oval face, round face, heart-shaped face, square face]
[facial structure: high cheekbones, defined jawline, soft jaw, small nose, pointed nose, button nose, plump lips, thin lips, full lips]
```

#### Eyes Chain (Extremely Important)
```
[eye basics: detailed eyes, large eyes, wide eyes, upturned eyes, downturned eyes]
[eye color: [specific color], heterochromia, gradient eyes, glowing eyes]
[eye detail: long eyelashes, thick eyelashes, eyeshadow, eye highlight, pupil detail, iris detail]
[eye expression: soft eyes, sharp eyes, kind eyes, seductive eyes, innocent eyes]
```

#### Hair Chain (One of the Most Important Visual Elements)

**Hair Style Sub-Chain:**
```
[length: very short hair, shoulder-length hair, waist-length hair, hip-length hair, extremely long hair]
[cut style: straight hair, wavy hair, curly hair, curled, layered cut, shag cut, asymmetrical cut]
[specific hairstyle: twintails, pigtails, ponytail, high ponytail, bun, braided hair, half-up half-down, side-swept bangs, blunt bangs, wispy bangs]
[hair volume: volumetric hair, fluffy hair, flat hair]
```

**Hair Color & Texture Sub-Chain:**
```
[primary color: [specific color], gradient hair, ombre hair, pastel color]
[secondary colors/highlights: with [color] highlights, streaks of [color], tips dyed [color]]
[texture & shine: glossy, matte, silky, shiny, healthy shine, wet look]
[hair details: no highlights (if de-emphasizing color variation), natural color, vibrant color]
```

**Hair Embellishments Sub-Chain:**
```
[accessories: hairband, ribbon in hair, hair clip, flower in hair, crown, tiara, hair ornament]
[adornments within hair: strings in hair, beads, gold accessories, pearls]
[hair behavior: flowing hair, windswept hair, hair defying gravity, floating hair]
```

**Complete Hair Example:**
```
very long hair, waist-length, straight hair, platinum blonde, silky texture, glossy shine, side-swept bangs, no highlights, flowing naturally, red ribbon woven through hair, hair ornament.
```

#### Additional Face & Head Details
```
[makeup: makeup, detailed makeup, eyeshadow, blush, lip gloss, smoky eyes, cat eye liner]
[other details: freckles, beauty marks, moles, scars on face, face paint, nose piercing, lip piercing, facial tattoo]
```

### 3.5 Clothing & Accessory Chains

**Clothing Structure** (for each garment):
```
[garment type: shirt, blouse, dress, skirt, pants, jacket, coat, etc.]
[fit & silhouette: form-fitting, loose, oversized, tight, flowing, short, long, knee-length, above-knee, floor-length]
[material: silk, cotton, leather, lace, velvet, satin, fabric type]
[color: [specific color], gradient, ombre, multicolor]
[pattern: solid, striped, polka dot, plaid, floral, geometric, checkered]
[details: buttons, zippers, buckles, seams, visible stitching, embroidery, lace trim, embellishments, ruffles, frills]
[wear & condition: pristine, worn, torn, dirty, weathered]
```

**Full Clothing Example:**
```
white button-up blouse, silk fabric, form-fitting, long sleeves, rolled up to elbows, navy blue trim on collar, gold embroidered edge, pearl buttons, visible stitching, pristine condition.
navy blue skirt, pleated, knee-length, silk material, white waistband, red ribbon bow at center.
black loafers, polished leather, dark socks with red stripe.
```

**Accessory Chain:**
```
[accessory type: earrings, necklace, bracelet, ring, watch, bag, belt, hat]
[material: gold, silver, pearl, crystal, leather, metal]
[style: simple, ornate, elegant, delicate, chunky, minimalist]
[details: chain link type, gemstone color, pendant shape, engraving]
```

### 3.6 Pose, Action & Expression Chain

**Pose Chain:**
```
[basic position: standing, sitting, lying down, kneeling, crouching, bending]
[pose type: static pose, dynamic pose, action pose, relaxed pose, tense pose]
[limb placement: hand on hip, crossed arms, arms at sides, hands behind head, one leg raised, splayed legs]
[body angle: facing viewer, facing away, profile, three-quarter view, turned over shoulder]
[hand detail: hands visible, hands detailed, hand position specific]
```

**Expression & Emotion Chain:**
```
[basic expression: smile, smirk, frown, blank expression, angry, sad, happy, neutral]
[expression intensity: subtle smile, big grin, seductive smile, gentle smile, smug expression]
[emotion: confident, shy, innocent, seductive, playful, serious, surprised, shocked]
[gaze direction: looking at viewer, looking away, looking down, looking over shoulder, staring, direct eye contact]
[mouth detail: open mouth, closed mouth, tongue visible, teeth showing]
```

**Complete Pose Example:**
```
standing, facing viewer, hand on hip, confident pose.
gentle smile, soft gaze looking directly at viewer, blushing slightly.
```

### 3.7 Environment & Location Chain

**Location Type:**
```
[setting type: indoor, outdoor, classroom, bedroom, kitchen, forest, beach, city street, fantasy world, abstract background]
[specific location: school hallway, modern apartment, medieval castle, underwater, space station]
```

**Architectural & Object Chain:**
```
[furniture/objects: desk, chair, bed, table, bookshelf, door, window]
[decorative elements: plants, flowers, artwork, posters, curtains, carpets]
[architectural style: modern, minimalist, vintage, rustic, futuristic, gothic, cozy]
[structural details: wooden beams, stone walls, tiled floor, brick wall, hardwood floor]
```

**Natural Environment Chain:**
```
[landscape: mountains, hills, forest, ocean, river, desert, meadow, garden]
[vegetation: trees, grass, flowers, moss, vines, wildflowers]
[weather: clear sky, cloudy, rainy, stormy, snowing, foggy, misty]
[time of day effects: morning light, afternoon light, golden hour, sunset, dusk, night, moonlight, starlight]
[atmospheric elements: mist, fog, dust, rain, snow, wind effects]
```

**Complete Environment Example:**
```
school hallway, lockers lining walls, wooden floor, window with afternoon sunlight streaming through, soft golden light, slightly blurred background, depth of field effect.
```

### 3.8 Camera, Composition & Framing Chain

**Shot Type:**
```
[framing: full body, upper body, close-up, headshot, extreme close-up, wide shot, establishing shot]
[composition: centered composition, rule of thirds, off-center, symmetrical, asymmetrical]
```

**Camera Angle:**
```
[angle: from below, from above, eye level, dutch angle, side profile, rear view, overhead]
[perspective: fish-eye, wide angle, normal lens, telephoto, depth of field, shallow depth of field, bokeh]
```

**Depth & Focus:**
```
[focus: sharp focus, soft focus, selective focus on [element], blurred background]
[depth: bokeh background, blurred background, detailed background, simple background (if contrast wanted)]
[layering: foreground element, middle ground, background, multiple layers]
```

**Complete Camera Example:**
```
full body portrait, centered composition, eye level camera, sharp focus on character, shallow depth of field, blurred background, soft bokeh effect.
```

### 3.9 Lighting & Mood Chain

**Light Quality:**
```
[brightness: bright lighting, soft lighting, dim lighting, dramatic lighting, low light]
[light type: natural light, sunlight, moonlight, artificial light, neon light, candlelight, firelight]
[light direction: front lighting, side lighting, backlighting, rim lighting, side-lit, top-lit]
```

**Light Effects:**
```
[effects: volumetric lighting, god rays, lens flare, light rays, light scattering, glow, bloom effect]
[shadows: soft shadows, sharp shadows, no shadow, shadow detail]
[reflections: reflective surface, mirror reflection, water reflection]
```

**Color Temperature:**
```
[temperature: warm lighting, cool lighting, neutral lighting, golden lighting, blue lighting]
[mood-specific: cinematic lighting, dramatic lighting, romantic lighting, eerie lighting, melancholic lighting]
```

**Complete Lighting Example:**
```
afternoon sunlight, golden hour lighting, warm color temperature, soft shadows, volumetric light rays through window, cinematic lighting, slightly backlit character with rim lighting.
```

---

## 4 GENERATION MODES

### 4.1 Pure Location / Environment
**Usage:** Background/scenery only, no characters
**Key Focus:** Architectural detail, atmosphere, environmental storytelling

**Emphasis Order:**
1. Quality tags
2. Art style
3. Location specifics
4. Architectural detail
5. Environmental elements (flora, weather, objects)
6. Lighting & mood
7. Camera framing

### 4.2 Character Portrait
**Usage:** Character-focused, minimal or clean background

**Variations:**
- **Standard Portrait:** Head + shoulders + upper torso, background can be blurred or simple
- **Full Body Portrait:** Entire character visible, usually centered, background secondary
- **T-Pose Front View:** Character facing directly forward, arms at sides or slightly away, neutral expression, no pose dynamics
- **T-Pose Back View:** Character facing away, full body visible, clean silhouette
- **Turnaround Sheet:** Multiple views (front, side, back) in one image, character in same pose across views

**Key Focus:** Character appearance, consistency, recognition

**Emphasis Order:**
1. Quality tags
2. Art style
3. Character count (1girl, solo, etc.)
4. Core appearance (face, body, hair)
5. Clothing
6. Pose (usually neutral for portraits)
7. Expression
8. Background (often blurred or simple)
9. Lighting

### 4.3 Scene / Full Composition
**Usage:** Character(s) interacting with environment, full narrative composition

**Key Focus:** Character + environment balance, spatial relationships, action

**Emphasis Order:**
1. Quality tags
2. Art style
3. Subject count
4. Character appearance
5. Clothing
6. Pose & action
7. Environment detail (SAME WEIGHT as character)
8. Camera framing
9. Lighting & mood

### 4.4 Manga Panel
**Usage:** Comic-style illustration with potential text/dialogue

**Panel Structure Options:**
- **Single Panel:** One rectangular frame with manga-style framing
- **2-Koma:** Two vertical panels stacked
- **3-Koma:** Three vertical panels stacked
- **4-Panel Strip:** Horizontal 4-panel comic
- **Irregular Grid:** Non-standard panel layout

**Special Tags for Manga:**
```
manga panel, comic panel, speed lines, action lines, screentone, halftone pattern, speech bubble, thought bubble, onomatopoeia, comic book style, bold outlines
```

**Text/Dialogue Rules:**
- Dialogue MUST be readable, grammatically correct English
- Specify placement: "speech bubble above character", "thought bubble upper left"
- Keep text simple and scannable
- Example: `speech bubble with text "Hello!", white speech bubble with black text, bold font`

**Emphasis Order:**
1. Quality tags
2. Manga style tags
3. Panel layout (single panel, 2-koma, etc.)
4. Subject count
5. Character appearance
6. Action/pose
7. Environment
8. Dialogue/text (if present)
9. Comic effects (speed lines, screentones)
10. Lighting & mood

---

## 5 NEGATIVE PROMPT CONSTRUCTION

### 5.1 Universal Base (Copy This for Every Prompt)

```
worst quality, low quality, normal quality, lowres, bad anatomy, bad hands, bad feet, bad proportions, bad perspective, text, error, missing fingers, extra digit, fewer digits, cropped, jpeg artifacts, signature, watermark, username, blurry, out of focus, deformed, mutated hands, mutation, ugly, disfigured, poorly drawn face, poorly drawn hands, extra arms, extra legs, fused fingers, too many fingers, long neck, malformed limbs, missing arms, missing legs, extra limbs, cloned face, gross proportions, malformed hands, missing ears
```

### 5.2 Contextual Additions (Add Based on What You DON'T Want)

**If Solo Character (no other people):**
```
1boy, 1other, multiple people, crowd, background character, extra characters
```

**If Anime Style (avoid realistic):**
```
realistic, photorealistic, photo, 3d, cgi, 3d rendering, realistic texture, realistic shading, western comic, cartoon
```

**If NOT Child/Loli/Shota (always add if any ambiguity):**
```
child, loli, shota, young girl, young boy, toddler, baby, infant, chibi (if not intentional)
```

**If Detailed Background Wanted (avoid simple):**
```
low detail background, simple background, plain background, monochrome background, solid color background
```

**If Specific Quality Issues to Avoid:**
```
bad shadow, bad lighting, overexposed, underexposed, washed out, oversaturated, undersaturated, color bleeding
```

**If NOT Censored/Blurred:**
```
mosaic censoring, bar censor, censored, blur censor, pixelated censor, blurred genitals
```

**If NO Text/Watermarks:**
```
text, watermark, signature, username, logo, subtitles, caption, label, watermark in corner
```

**If Manga Panel with Readable Text (NOT gibberish):**
```
gibberish, distorted text, unreadable text, scrambled text, illegible dialogue, corrupted text
```

**If Specific Anatomical Issues:**
```
asymmetrical eyes, cross-eyed, lazy eye, droopy eye, missing eye, extra eye, extra fingers, missing fingers, webbed fingers, clawed hands, malformed jaw, missing teeth
```

**If No Excessive Detail in Unwanted Areas:**
```
overly detailed, hyper detail in background, too much detail
```

### 5.3 How to Structure Final Negative Prompt

```
Negative Prompt:
[UNIVERSAL BASE TAGS], [CONTEXTUAL ADDITIONS], [SPECIFIC EXCLUSIONS FOR THIS IMAGE]
```

Example:
```
worst quality, low quality, lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer digits, cropped, jpeg artifacts, watermark, username, blurry, deformed, mutated, ugly, disfigured, poorly drawn face, extra limbs, bad proportions.
1boy, 1other, multiple people, crowd.
realistic, photo, 3d, cgi, western comic.
bad shadow, bad lighting, overexposed.
```

---

## 6 PROMPT TEMPLATE & STRUCTURE

### 6.1 File Organization

```
# [CHARACTER/GROUP/LOCATION NAME]

## [VARIATION NAME - Descriptive Title]

\`\`\`Positive Prompt
[Complete positive prompt tags]
\`\`\`

\`\`\`Negative Prompt
[Complete negative prompt tags]
\`\`\`


### AI Settings:
- **Canvas Size:** [dimensions, e.g., 768x1024]
- **Sampler:** [if applicable]
- **Steps:** [if applicable]
- **CFG Scale:** [if applicable]

---

## [NEXT VARIATION]

(repeat structure)

---

## [ANOTHER VARIATION]

(repeat structure)
```

### 6.2 Variation Title Naming Convention

**Format:** [Setting/Context], [Pose/Action], [Key Visual Feature], [Mood/Time]

**Examples:**
- "School Uniform, Seductive Lean Against Locker, Indoor Hallway, Afternoon"
- "Beach Swimsuit, Playful Pose in Shallow Water, Sunset, Golden Hour"
- "Formal Gown, Standing Elegantly, Grand Ballroom, Candlelit Evening"
- "Battle Armor, Dynamic Combat Pose, Ancient Ruins, Dramatic Lighting"
- "Pajamas, Lying in Bed, Cozy Bedroom, Early Morning Light"

**Why:** This naming immediately tells anyone reading the database what they'll get without opening the full prompt.

---

## 7 WORKING EXAMPLES

### 7.1 Example 1: Character Portrait (Detailed)

```
# Lyra

## Full-Body Portrait, Elegant Stance, Formal Ball Gown, Candlelit Palace

\`\`\`Positive Prompt
masterpiece, best quality, absurdres, ultra-detailed, sharp focus, very aesthetic, high resolution, detailed anime.

1girl, solo, young adult, appears 23 years old, tall and graceful, slim waist, gentle curves, fair skin, unblemished, porcelain complexion.
beautiful detailed face, symmetrical features, soft facial structure, high cheekbones, delicate jawline, small nose, full pale lips, subtle blush.
(detailed eyes:1.3), large eyes, upturned eyes, emerald green color, long thick eyelashes, sharp iris detail, luminous gaze, looking at viewer.
very long hair, hip-length, wavy texture, platinum blonde, silky shine, gradient into pale silver tips, voluminous, side-swept bangs, flowing elegantly, pearl hair pin.

formal ball gown, gold silk material, floor-length, form-fitting bodice, sweeping skirt with layered tulle, intricate gold embroidery throughout, off-shoulder neckline, long sleeves with delicate lace, elaborate detail, pristine condition.
jewelry, gold necklace with emerald pendant, matching gold earrings, diamond bracelet on left wrist.

standing, facing viewer, elegant posture, one hand at side, other hand resting on hip, confident yet graceful pose, relaxed shoulders.
gentle smile, soft gaze, serene expression, refined demeanor.

palace interior, grand ballroom, vaulted ceiling, marble floor with geometric pattern, ornate columns, candlelit ambiance, warm golden light, multiple candlebras, soft shadows, luxurious setting, depth of field effect, subtle bokeh.

candlelit lighting, warm golden tones, soft illumination on face and dress, gentle rim lighting on hair, romantic atmosphere, cinematic color grading.
\`\`\`

\`\`\`Negative Prompt
worst quality, low quality, lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, cropped, jpeg artifacts, watermark, username, blurry, deformed, mutated, ugly, disfigured, poorly drawn face, extra limbs, bad proportions.
1boy, 1other, multiple people, crowd.
realistic, photo, photorealistic, 3d, cgi, western comic.
child, loli, shota.
bad shadow, bad lighting, overexposed, underexposed, washed out.
mosaic censor, censored.
low detail background, simple background.
\`\`\`

### AI Settings:
- **Canvas Size:** 768 x 1024
- **Steps:** 28-32
- **CFG Scale:** 7-9


```

---

### 7.2 Example 2: Scene (Character + Environment)

```
# Akane

## School Hallway, Casual Lunchtime Pose, Beside Lockers, Warm Afternoon Glow

\`\`\`Positive Prompt
masterpiece, best quality, absurdres, ultra-detailed, sharp focus, very aesthetic, high resolution, anime, detailed background.

1girl, solo, teenage, appears 16 years old, petite build, fair skin, cute features, youthful appearance, large expressive eyes.
beautiful detailed face, round face, soft features, small nose, rosy cheeks, natural blush, delicate jawline.
big bright eyes, blue eyes, detailed pupils, long eyelashes, sparkling eyes, innocent expression.
long black hair, waist-length, straight with subtle waves, shiny texture, side bangs, no highlights, flowing naturally, simple hair clip.

school uniform, white short-sleeved shirt, blue sailor collar, navy pleated skirt, knee-length, white ankle socks, brown loafers, polished leather, school bag on shoulder.

standing casually, facing slightly toward viewer, relaxed posture, one hand holding lunchbox, other hand near chest, playful smile, natural pose.
cheerful expression, bright smile, happy eyes, looking at viewer, excited demeanor.

school hallway interior, rows of blue metal lockers, wooden floor, bright overhead lighting mixed with natural light from windows, posters on walls (club recruitment posters, notice board), drinking fountain visible, clean and well-maintained, other students blurred in background (depth of field).

warm afternoon sunlight streaming through hallway windows, golden hour quality light, soft natural shadows, bright and cheerful atmosphere, sharp focus on character, blurred warm-toned background.
\`\`\`

\`\`\`Negative Prompt
worst quality, low quality, lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, cropped, jpeg artifacts, watermark, blurry, deformed, mutated, ugly, disfigured, poorly drawn face, extra limbs, bad proportions.
1boy, 1other, multiple adult characters, excessive crowd.
realistic, photo, photorealistic, 3d, cgi.
child (if age ambiguity), loli.
bad shadow, bad lighting, overexposed, underexposed.
low detail background, simple background, plain background.
censored, mosaic.
school uniform poorly drawn, torn clothes, dirty uniform.
\`\`\`

### AI Settings:
- **Canvas Size:** 768 x 768
- **Steps:** 24-28
- **CFG Scale:** 6-8

```
---

### 7.3 Example 3: Environment Only (Location)

```
# Mystic Forest Temple

## Ancient Shrine Deep in Forest, Misty Morning, Overgrown Architecture

\`\`\`Positive Prompt
masterpiece, best quality, absurdres, ultra-detailed, sharp focus, very aesthetic, high resolution, detailed environment, painting style, atmospheric.

no characters.

ancient temple, stone structure, Japanese-inspired architecture, weathered wooden torii gate, moss-covered stone stairs, wooden prayer plaques hanging (ema), ornate roof tiles (some broken), intricate carvings on pillars.

surrounding forest, tall ancient trees, dense foliage, thick moss covering rocks and fallen logs, overgrown vines climbing temple structure, wild grass, ferns, scattered wildflowers (white and purple), natural forest chaos slowly reclaiming the shrine.

misty morning atmosphere, fog rolling through forest, volumetric mist between trees, soft diffused light filtering through canopy, dappled light on stone surfaces, cold color temperature with slight blue-tint, ethereal quality.

lighting, natural soft morning light, god rays piercing through mist and trees, shadows from leaves creating intricate patterns on temple, cool color grading, atmospheric depth through mist.

wide establishing shot, centered composition, depth of field focusing on temple entrance, layered: foreground moss-covered rocks, middle ground temple structure, background trees fading into mist.

cinematic atmosphere, mysterious mood, serene but slightly eerie, peaceful solitude, contemplative feeling.
\`\`\`

\`\`\`Negative Prompt
worst quality, low quality, lowres, bad anatomy, text, error, cropped, jpeg artifacts, watermark, blurry, deformed, ugly, disfigured.
1girl, 1boy, people, characters, human, figure.
modern building, signs, electric poles, urban elements, cars, contemporary objects.
bright daylight, sunset, noon lighting.
rain, storm, heavy fog that obscures everything.
poorly drawn architecture, unrealistic proportions, gravity-defying trees.
\`\`\`

### AI Settings:
- **Canvas Size:** 1024 x 768
- **Steps:** 28-32
- **CFG Scale:** 7-9

```
---

### 7.4 Example 4: Manga Panel (Single with Dialogue)

```
# Takeshi & Hana

## Single Manga Panel, Dramatic Confession Scene, Rooftop Sunset, Emotional Moment

\`\`\`Positive Prompt
masterpiece, best quality, absurdres, ultra-detailed, sharp focus, manga panel, manga style, comic book style, bold outlines.

1boy 1girl, teenager, standing on rooftop, facing each other, close proximity.

boy: sharp features, dark hair, serious expression, school uniform, hand reaching forward, nervous tension.
girl: long light hair, tearful eyes, school uniform, hand near chest, emotional vulnerability, blushing deeply.

rooftop setting, metal railing, cityscape background (skyscrapers blurred), sunset sky (orange and pink gradient), dramatic clouds.

dramatic lighting, golden hour sunset backlighting, warm tones, shadows on faces creating emotional tension, cinematically lit.

speech bubble with text "I like you.", upper right, bold font, white bubble with black outline, clean readable text.
thought bubble with text "This is...", upper left, traditional manga style, dashed line bubble.

speed lines behind dramatic gesture, emphasizing emotional impact, screentone effect for atmosphere, manga screentone shading, high contrast art style.
\`\`\`

\`\`\`Negative Prompt
worst quality, low quality, lowres, bad anatomy, bad hands, error, cropped, jpeg artifacts, watermark, blurry, deformed.
realistic, photo, photorealistic, 3d.
gibberish text, distorted text, unreadable dialogue, corrupted text.
censored, mosaic.
multiple panels (if single panel specified), simple lines (if detailed wanted).
low detail background.
\`\`\`

### AI Settings:
- **Canvas Size:** 768 x 1024 (portrait panel)
- **Steps:** 28-32
- **CFG Scale:** 7-9

```
---

## 8 CRITICAL DO'S AND DON'Ts

### DO ✓

- **DO** assume the AI generator has NO context or prior knowledge
- **DO** order tags by importance: quality → style → subject → appearance → clothing → pose → environment → lighting
- **DO** be extremely specific with colors, measurements, and physical attributes
- **DO** use comma separation for all tags
- **DO** group related chains with periods or line breaks for readability
- **DO** use weighted emphasis sparingly on 3-5 most critical elements
- **DO** describe pose with explicit limb placement and body angle
- **DO** include lighting details (direction, color temperature, special effects)
- **DO** prioritize user-provided details over assumptions
- **DO** test prompts and iterate with refinements
- **DO** keep a consistent character database with exact appearance tags for reuse
- **DO** specify "no highlights" if character has solid hair color
- **DO** describe fabric types and material when relevant to clothing
- **DO** include environmental details (furniture, objects, architecture) even if secondary to character
- **DO** specify gaze direction (looking at viewer, looking away, etc.)

### DON'T ✗

- **DON'T** assume the AI knows character names or franchises
- **DON'T** use vague words like "beautiful," "gorgeous," "fancy"—always be specific
- **DON'T** write full sentences or narrative context in prompts
- **DON'T** rely on implied details (the AI won't infer anything)
- **DON'T** place low-priority information before high-priority
- **DON'T** use overwhelming emphasis tags on every detail (dilutes effect)
- **DON'T** forget negative prompts (they're as important as positive)
- **DON'T** assume correct anatomy or gravity without explicit statement
- **DON'T** forget to specify skin condition, freckles, marks if character-defining
- **DON'T** omit lighting details (AI needs explicit direction and mood)
- **DON'T** use ambiguous pose descriptions ("standing cute"—use "standing, hand on hip")
- **DON'T** mix art styles without clear intention (anime + photorealistic usually conflict)
- **DON'T** skip environment detail if composition includes setting
- **DON'T** assume the AI will generate readable dialogue without explicit instruction
- **DON'T** ignore context-specific negatives (manga panels need different negatives than portraits)

---

## 9 TROUBLESHOOTING & REFINEMENT

### Common Issues & Fixes

| Issue | Cause | Solution |
|-------|-------|----------|
| Character looks nothing like intended | Appearance tags too vague or conflicting | Specify every detail: exact hair color, eye color, body measurements, skin tone. Use weighted emphasis on critical features. |
| Hands/Feet deformed | Not explicitly tagged or unknown to model | Add to negative prompt: "bad hands, bad feet, malformed hands" and positively emphasize: "beautiful hands, detailed hands, proper proportions" |
| Wrong pose/action | Vague pose description | Use explicit limb placement: "hand on hip, other hand at side, standing, facing viewer, slight turn to left" |
| Background too blurry/simple | Not prioritized in prompt | Move environment tags higher in prompt order, use "detailed background, rich environment, intricate details" |
| Face doesn't look right | Face tags too minimal | Expand face chain: add cheekbone detail, jawline, nose shape, lips, skin texture, eye shape, facial balance |
| Lighting feels wrong | Lighting tags missing or vague | Explicitly state: light direction (rim lighting, backlighting, side-lit), color temperature (warm, cool, golden), special effects (volumetric, god rays, bloom) |
| Character looks too young/old | Age tags ambiguous | Use both age number ("18 years old") AND age appearance ("young adult", "mature features") |
| Hair doesn't match vision | Color/texture/style insufficient | Expand hair chain completely: length, cut type, primary color, highlights/secondary colors, texture (silky, matte, glossy), style (twintails, straight, wavy) |
| Multiple characters fighting for attention | Emphasis/weighting unclear | Use {{weighted brackets}} ONLY on the character or element meant to be focal point. Reduce other details. |
| Art style wrong or mixed | Style tags conflicting or insufficient | Choose ONE primary style. Don't mix realistic + anime. Be explicit: "anime, detailed anime" not just "anime". Add art medium if needed: "digital art, watercolor, oil painting" |

### Iteration Strategy

1. **Generate** with baseline prompt
2. **Evaluate** what's wrong or missing using the issue table above
3. **Modify** only 1-2 problem areas per new generation (too many changes = unreliable feedback)
4. **Document** successful tag combinations for reuse
5. **Build** character templates with verified appearance tags
6. **Test** variations (outfit, pose, setting) using same core appearance tags

---

## 10 QUICK REFERENCE CHECKLISTS

### Pre-Generation Checklist

- [ ] Quality tags included at start? (masterpiece, best quality, absurdres, etc.)
- [ ] Art style specified? (anime, manga, watercolor, etc.)
- [ ] Subject count tagged? (1girl, solo, 1boy, etc.)
- [ ] Character appearance complete?
  - [ ] Face description (detailed, symmetrical, specific features)
  - [ ] Eyes (color, size, expression, eyelashes)
  - [ ] Hair (length, color, texture, style, accessories)
  - [ ] Body build (height, proportions, measurements)
  - [ ] Skin (tone, condition, marks)
- [ ] Clothing detailed? (type, fit, material, color, pattern, details)
- [ ] Pose specified? (position, limb placement, body angle, facing)
- [ ] Expression tagged? (smile, emotion, gaze direction)
- [ ] Environment described if needed? (location, objects, architecture)
- [ ] Lighting included? (direction, temperature, special effects)
- [ ] Camera specified? (shot type, angle, depth of field)
- [ ] Negative prompt complete?
  - [ ] Universal base included
  - [ ] Contextual exclusions added (gender, style, quality issues)
  - [ ] Specific unwanted elements for THIS image
- [ ] Tags ordered by priority? (quality → style → subject → appearance → clothing → pose → environment → lighting)
- [ ] Emphasis tags (<3) used strategically on 3-5 most critical elements?
- [ ] No ambiguous wording? (checked for vague words like "beautiful," "nice," "fancy")

### Quality Checklist (After Generation)

- [ ] Character recognizable from intended description?
- [ ] Face matches specification (eyes, hair, features)?
- [ ] Clothing accurate to prompt?
- [ ] Pose matches intention?
- [ ] Environment appropriate and detailed?
- [ ] Lighting creates intended mood?
- [ ] No obvious deformities or errors?
- [ ] Composition balanced and visually appealing?
- [ ] Any improvements needed for next iteration?

---

## 11 APPENDIX: COMMON TAG REFERENCE

### Quick Color List
```
black, white, gray, silver, gold, red, pink, magenta, purple, blue, cyan, teal, green, lime, yellow, orange, brown, tan, beige, cream
pastel [color], neon [color], metallic [color], matte [color]
```

### Quick Texture List
```
silky, smooth, glossy, matte, rough, velvet, satin, lace, leather, fabric, cotton, silk, wool, metal, shiny, dull, polished, weathered, worn, pristine
```

### Quick Fabric List
```
silk, cotton, linen, wool, polyester, satin, velvet, leather, suede, denim, lace, tulle, chiffon, rubber, latex, metallic fabric
```

### Quick Expression List
```
smile, smirk, frown, neutral, angry, sad, happy, shy, confident, seductive, playful, serious, surprised, shocked, confused, content, relaxed, tense, nervous, excited, blushing
```

### Quick Pose Verbs
```
standing, sitting, lying, kneeling, crouching, bending, leaning, stretching, jumping, running, walking, dancing, posing, reaching, gesturing, embracing, holding
```

### Quick Lighting Setup
```
front lighting, side lighting, backlighting, rim lighting, top lighting, under lighting, silhouette
natural light, sunlight, moonlight, candlelight, firelight, neon light, LED light, streetlight
soft lighting, hard lighting, dramatic lighting, cinematic lighting, volumetric light
warm lighting, cool lighting, golden hour, blue hour, neon colors, monochromatic light
```

---

**END OF PROMPT DATABASE GUIDE**

---

## Notes for Users:

This system prioritizes:
1. **Clarity for image generators** (treating them as having zero prior knowledge)
2. **Consistency for character databases** (reusing exact tag combinations)
3. **Hierarchy of importance** (telling the AI what matters first)
4. **Specificity over vagueness** (always choosing explicit descriptors)
5. **Scalability** (works for simple or extremely complex generations)

Use this as a reference when creating prompts. The goal is successful, consistent, repeatable image generation across any AI image generator platform.
