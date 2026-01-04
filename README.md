# Weekly Viewer

Local-first viewer for weekly markdown notes. It is designed to surface actions, links, and key sections quickly without heavy engineering or a backend.

---

## Quick Start

1. Open the viewer in a browser (Chrome or Edge recommended for folder picking):
   - `viewer_project/view/2026_viewer.html`
2. Click **Open Folder** and select:
   - `viewer_project/weeklies/`
3. Use the left outline, search, and tags panel to navigate and filter.

You can also:
- **Open .md** to load a single file
- **Paste** to view ad hoc markdown

---

## Tags (How Filtering Works)

The viewer indexes lines that start with `@tag` or `@@tag`.

Examples:
- `@ACTION Call Bob`
- `@METRIX Monday: 219.3`
- `@@followup Draft email`

Open the **Tags** panel to filter to only those lines across all loaded weeks.

---

## Personal Data Protection (Do Not Remove)

**The `viewer_project/weeklies/` directory contains PERSONAL NOTES that must NEVER be committed to GitHub.**

The `.gitignore` is configured to exclude:
- `viewer_project/weeklies/` and all contents
- Any `.md`, `.pdf`, `.docx` files in `viewer_project/`
- Directories named `irregular/`, `personal/`, `private/`, `notes/`

**For all contributors:**
- Do not modify `.gitignore` to allow personal notes
- Do not commit personal data under any circumstances
- If you see personal data in a commit, alert the repo owner immediately

---

## Project Layout

```
.
├── viewer_project/
│   ├── view/
│   │   └── 2026_viewer.html   # Single-file viewer app
│   └── weeklies/              # Local notes (gitignored)
├── AGENTS.md
├── CLAUDE.md
├── GEMINI.md
└── tools/
    └── worktree/
```

---

## How It Works (Short Version)

- The viewer is a single HTML file with embedded JS/CSS.
- It parses markdown line-by-line and builds a collapsible outline from headings.
- Tags are indexed only when they start a line (`@` or `@@`).
- The **Open Folder** flow concatenates multiple weekly files into one view and injects a week header for each file.

---

## Next Steps (Planned Enhancements)

The following features are queued for the next development sprint:

### 1. Selective File Loading
**Problem:** Loading all 56 weeks at once is overwhelming for human use.

**Solution:** Add the ability to select specific files to load:
- Pick individual weeks one at a time
- Select a subset of weeks (e.g., W40-W45)
- Checkbox list after folder selection to choose which files to include

### 2. Source File Context in Tag View
**Problem:** When filtering by a tag (e.g., `@ACTION`), the results show lines but not which weekly file each line came from.

**Solution:** When displaying tag-filtered results, show the source filename for each line:
- Display filename as a header/prefix before each result
- Group results by source file
- Make it easy to see "this @ACTION came from 2025W20"

---

**@CODEX:** Please review these planned features and comment in `comms.md` with any suggestions, alternative approaches, or implementation ideas before we proceed.

**@DAZZA:** Questions for you:
1. For selective file loading, would you prefer: (a) checkboxes after folder selection, (b) a dropdown/picker to add files one at a time, or (c) date range selector (e.g., "show weeks 40-45")?
2. For source file context, should the filename appear (a) as a prefix on each line, (b) as a section header grouping all results from that file, or (c) both?

---

## Notes / Limitations

- Folder selection uses `webkitdirectory`, so Chrome/Edge are safest.
- No backend. Everything runs locally in the browser.
- This is a viewer only (no writing back to notes).
