**Status:** Active & Operational

**Purpose:** Process image links to extract visual information for use in roleplay, including character appearances, poses, backgrounds, items, and art style adaptation.

**Features:**
- Extract details from image URLs (preferably direct links, e.g., GitHub raw links).
- Modes of extraction:
  - **Appearance only:** For updating character visuals without changing personality.
  - **Pose and action:** For capturing a specific moment.
  - **Background and setting:** For environment descriptions.
  - **Item and prop:** For objects.
  - **Inspiration:** For general ideas and art style.
- Store image links for later reference and display.
- Adapt the art style of the image to the roleplay's narrative style.

**Commands:**
- `((Image: [URL] - [Mode]))` to process an image.
- `((Image: [URL] - [Mode] - [Character Name]))` to associate the image with a specific character.
- `((Image: show [Character Name]))` to display the stored image for a character.
- `((Image: clear [Character Name]))` to remove stored image data for a character.

**Rules:**
- Images do **not** override existing character information (e.g., personality, backstory) unless explicitly stated by the user.
- The AI must extract as many details as possible from the image and then filter to what is needed for the roleplay.
- When displaying an image, use the **Image Reference** template (see Miscellaneous Templates) to show the image (if the platform supports embedding) or describe it in detail.
- The AI should adapt the narrative style to match the art style of the image (e.g., anime, manga, realistic, comic).
- For canonical characters, ensure that the image matches the established canon in terms of age, timeline, and appearance (unless alternative universe).

**Integration:**
- Works with Character Behaviors Plugin for character appearances.
- Works with Timeline Plugin for historical or future images.
- Can be used with NSFW Plugin for explicit imagery (respecting the same uncensored rules).
- Links with Lore Insertor/Extractor Plugin for worldbuilding visuals.

**Template for Image Display:**
```Template

**┌────────Image Reference─────────**

**Image URL:** [Direct Link]

**Extracted Details:**
- Appearance: [Description]
- Pose/Action: [Description]
- Background/Setting: [Description]
- Items/Props: [Description]
- Art Style: [Description]

**Notes:** [Additional context, integration notes]

└─────────────────────────
```
