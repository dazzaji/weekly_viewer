# Weekly Viewer Project - Initial Analysis Report

**Agent:** Claude Code
**Branch:** `agent/claude-viewer`
**Date:** 2026-01-04

---

## Executive Summary

You have a substantial personal knowledge management challenge: **56 weekly markdown files** totaling ~67,500 lines of notes from 2025, containing actionable items, content snippets, personal metrics, meeting notes, research links, and "gems" that are effectively invisible to you after a few days.

The existing viewer (`2026_viewer.html`) is a solid foundation—a self-contained HTML/JS app that parses markdown, provides collapsible sections, and supports `@@tag` filtering. However, it's underutilized and needs enhancements to address your "surface the buried treasure" problem.

---

## Data Shape Analysis

### File Inventory

| Metric | Value |
|--------|-------|
| Total weekly files | 56 markdown files |
| Coverage | 2025W01 through 2025W52 (mostly complete) |
| Total lines | ~67,500 |
| Largest files | W08 (2824 lines), W43 (2623 lines), W11 (2606 lines) |
| Special files | Some weeks have auxiliary files (e.g., `2025W34-BenNotes.md`, `2025W33-Demo_Synthi.md`) |
| Non-markdown | 1 PDF (`2025W35-GoDaddySeriousJunkFee.pdf`) |

### Standard Weekly Structure

Most files follow this semi-consistent pattern:

```
2025WXX Month DD - Month DD
Goals: [weekly goals/themes]
LinkedIn: [follower counts]

[Top-of-week punch lists - day-by-day often]

@METRIX
* Monday: [weight/metrics]
* Tuesday: ...
...

# WEEKLY
## MONDAY - [meeting/topic]
## TUESDAY - ...

# ITEMS
[various @ACTION items and notes]

# CONTENT
[longer-form content, articles, research, tutorials]
```

### Tag/Marker Conventions

| Tag | Count | Purpose |
|-----|-------|---------|
| `@ACTION` | 487 | Tasks/to-dos to complete |
| `@ACTION_DONE` | 79 | Completed tasks |
| `@METRIX` | 52 | Weekly metrics section marker |
| `@ACTION-2`, `@ACTION-3` | ~few | Numbered/prioritized actions |

**Key insight:** Your tagging is prefix-based (`@ACTION`) not the `@@tag` format the viewer expects. The viewer looks for `@@tag` while your actual convention is `@ACTION`.

### Major Content Themes (from sampling)

1. **AI Agents & Frameworks** - MCP, Pydantic, A2A, AutoGen, LangGraph, Claude Code
2. **Legal/Tech Intersection** - UETA, AI liability, error handling, SB53/SB813
3. **Events/Networking** - Davos prep, MIT/Stanford events, Shack15
4. **Health Tracking** - Weight, glucose (Oura/Stelo), eye exams, diabetes management
5. **Business Development** - Twilio, Procore, BML, Sogeti, ContractPod
6. **Technical Content** - Tutorials, research papers, implementation guides
7. **Personal/Spiritual** - Menachem meetings, dating, music

### Recurring Sections

- **Goals** - Top of file, weekly intentions
- **Day_PunchList** - Monday/Tuesday/etc daily task lists
- **@METRIX** - Weight and other daily measurements
- **# WEEKLY** - Meeting notes by day
- **# ITEMS** - Action items and links
- **# CONTENT** - Longer articles, tutorials, how-tos
- **# DONE_ITEMS** or `@ACTION_DONE` - Completed tasks

---

## Current Viewer Analysis

**Location:** `viewer_project/view/2026_viewer.html`

### What It Does Well
- Self-contained single-file app (easy to deploy/share)
- Clean dark-mode UI
- Collapsible H1 sections
- Tag filtering (for `@@tag` format)
- Full-text search with highlighting
- Multiple view modes (H1, H1+H2, All)
- Inline link rendering

### Current Limitations
1. **Tag mismatch** - Viewer expects `@@tag`, your files use `@ACTION`
2. **Single-file only** - Can't view across multiple weeks
3. **No persistence** - Must reload each time
4. **No index/summary** - Can't see "all @ACTION items across all weeks"
5. **No date awareness** - Doesn't parse the week date ranges
6. **No AI assistance** - No way to query or summarize content

---

## Identified "Gems" Hiding in Your Notes

From sampling, here's the kind of valuable content that's effectively lost:

1. **One-liner ideas** - Quick thoughts buried mid-file
2. **Links to resources** - Papers, repos, demos, tutorials
3. **Contact/followup items** - Names + context that fade from memory
4. **Meeting insights** - Key takeaways from Menachem, Sandy, Roland, etc.
5. **Completed work** - Things you've done but forgot about
6. **Research content** - Multi-paragraph summaries of papers/tools
7. **Personal metrics patterns** - Weight trends, health observations

---

## Questions Before We Proceed

1. **Viewer deployment**: Where do you typically open the viewer? Local file? Simple local server? Do you need it to work offline?

2. **Multi-file priority**: Is the main pain point "I need to see across ALL weeks at once" or "I need to see ONE week better"? (Sounds like the former.)

3. **Tag standardization**: Would you prefer to:
   - Adapt the viewer to your existing `@ACTION` convention?
   - Adopt a new convention going forward?
   - Support both?

4. **AI CLI integration**: When you say you want to "pose questions to the AI CLI of your choice," are you thinking:
   - The AI reads the files and answers questions conversationally (like we're doing now)?
   - The viewer provides a "send to clipboard for AI" function?
   - Some kind of pre-computed summaries/indices that AIs can quickly parse?

5. **Read-only focus**: You emphasized this is a "viewer" job—no downstream actions. Is that still accurate? (No task management, no editing, just surfacing and navigating?)

6. **"Good enough" threshold**: You mentioned not sweating the last 5-10%. What's the minimum viable improvement? Examples:
   - "See all @ACTION items from all weeks on one screen"
   - "Quick search that actually finds what I'm looking for"
   - "AI-generated weekly summaries"

---

## Preliminary Enhancement Ideas

These are brainstorming seeds for `dev_plan.md`—we can refine based on your answers:

### Quick Wins (Low Effort, High Impact)

1. **Fix tag regex** - Update viewer to match `@ACTION`, `@METRIX`, etc.
2. **Multi-file loader** - Load all 56 files at once, concatenated or switchable
3. **Cross-file search** - Search across all weeks, results grouped by week
4. **Pre-generated index** - A JSON/HTML file listing all `@ACTION` items with links

### Medium Effort

5. **Timeline view** - Calendar/timeline showing weeks with content previews
6. **Topic extraction** - Automatic categorization (AI/Legal/Health/Personal/etc.)
7. **Link harvester** - Extract and list all URLs across all files
8. **Done vs. Pending tracker** - Show `@ACTION` vs `@ACTION_DONE` status

### AI-Assisted Features

9. **Weekly summaries** - Pre-generated AI summaries for each week
10. **"What did I do about X?"** - Query interface that pulls relevant sections
11. **Pattern detection** - "You mentioned [person] 12 times across weeks W20-W35"
12. **Clipboard exporter** - Format selection for pasting into AI CLI conversations

### For Multi-Agent Coordination

13. **comms.md protocol** - How agents should report findings to each other
14. **Standardized output format** - JSON schema for extracted data

---

## Next Steps

1. **Your input**: Answer the questions above (or tell me to proceed with assumptions)
2. **dev_plan.md**: I'll contribute to the shared development plan
3. **Prototype**: Start with the quickest wins that deliver the most value
4. **Iterate**: Test, get feedback, refine

---

## Appendix: Sample Content Types Found

### @ACTION Example
```
@ACTION BERKELEY AGENTS 2025 see about modular fun - register:
https://llmagents-learning.org/sp25 and resources https://llmagents-learning.org/f24
```

### @METRIX Example
```
@METRIX
* Monday: 219.3.
* Tuesday: 221.3.
* Wednesday: 222.5.
...
```

### Content Block Example
```
# CHAIN OF CONTINUOUS THOUGHT

- **The overall main point is**: Meta AI introduces the "Chain of Continuous
Thought" (Coconut) method to enhance reasoning in large language models...
```

### Goals Example
```
2025W40 September 29 - October 05
Goals: prep 12:21/25 to 3/20/26 for 6/21/26
* **Leverage law.MIT.edu** all the way :-)
* Sophie; Lori; Kai; Heidi; Katalina
```

---

*Report generated by Claude Code in branch `agent/claude-viewer`*
