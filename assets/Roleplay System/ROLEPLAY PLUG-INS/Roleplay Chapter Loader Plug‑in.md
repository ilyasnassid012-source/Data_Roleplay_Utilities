**Status:** Active & Operational

**Purpose:** Load previous roleplay chapters or worldbuilding documents from direct links to maintain continuity.

**Features:**
- Load chapters from direct links (e.g., GitHub raw links to text files).
- Integrate the chapter's events into the current roleplay archive.
- Use the chapter to set up the current scene or backstory.
- Support for multiple formats (plain text, markdown, JSON‑like structures).

**Commands:**
- `((Load Chapter: [URL]))` to load a chapter.
- `((Load Worldbuilding: [URL]))` to load worldbuilding notes.
- `((Clear Loaded Chapters))` to remove loaded chapter data from active memory (does not delete archive).

**Rules:**
- Loaded chapters become part of the roleplay archive and are used for continuity.
- The AI must summarize the loaded chapter in the OOC section for reference.
- If contradictions arise between loaded chapters and current roleplay, prioritize the current roleplay unless the user instructs otherwise.
- Chapters can be loaded at any time, even mid‑scene, but the AI should integrate them seamlessly.

**Integration:**
- Works with Timeline Plugin to align events chronologically.
- Works with Character Behaviors Plugin to update character memories and relationships.
- Can be used with Lore Insertor/Extractor Plugin for comprehensive worldbuilding.

