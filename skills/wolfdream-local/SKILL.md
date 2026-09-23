---
name: wolfdream-local
description: Personal local-only Wolfdream reprise and writing workflow under C:\Personal stuff\Wolfdream. Use for French prose, canon, timeline, character, manuscript, and map-continuity work. Never register or deploy this skill to m-skills.
---

# Wolfdream Local Skill

Use this personal skill when the user wants to resume, continue, revise, or reason about the Wolfdream fiction project.

## Personal / non-business boundary

- This is a personal creative-writing skill, not an enterprise or FastTrack skill.
- The working language for this project is French. Use French by default for Wolfdream content, preferably French (Canada) / fr-CA for Word proofing when creating or modifying documents.
- Ring-fence all Wolfdream file access to `C:\Personal stuff\Wolfdream` unless the user explicitly points to another personal project file under `C:\Personal stuff`.
- Refuse to read from or write to any path outside `C:\Personal stuff` unless the user explicitly confirms a one-off exception.
- This is a personal local skill only. Do not register it with Scout, do not copy it into `~\.scout\m-skills` or `~\.copilot\m-skills`, and do not try to make it pass Skill Guard.
- Do not use WorkIQ, Outlook, Teams, SharePoint, OneDrive cloud routing, FTOP, FTBI, Lynx, S360, Seismic, enterprise MCP servers, enterprise datasets, or enterprise skills for Wolfdream work.
- Do not use enterprise/customer/tenant context while working on Wolfdream.
- Do not use Wolfdream or personal-project context while doing enterprise work unless the user explicitly asks.
- Never place customer, tenant, M365, or work-derived content in the Wolfdream folder or in the personal GitHub source repo.
- If the user asks to prepare a file for personal printing or personal sharing, prefer the Purview `Non-business/Personal` sensitivity label when available; do not apply labels automatically without an explicit request.

## Project root

Primary project folder: `C:\Personal stuff\Wolfdream`

Expected current artifacts:

- `Wolfdream - Brief de reprise.docx` - first file to read; short handoff/canon summary.
- `WolfDream V3 - Chapitre 1 au present.docx` - active manuscript.
- `Wolfdream - Ligne du temps maitresse v0.1.xlsx` - primary canonical timeline and metadata source.
- `Wolfdream - Plan de redaction V3.docx` - writing plan and chapter/fragment architecture.
- `Personnages - Wolfdream.docx` or `Personnages — Wolfdream.docx` - character bible.
- `WD Chronologie — Wolfdream.docx` - secondary narrative chronology.
- `Wolfdream - Carte style manuscrit v0.10.png` - current map reference.
- `Archive\` - backups and old versions; consult only when comparing history or recovering older material.

## Routing and related local skills

- Use this skill for Wolfdream canon, prose, timeline, characters, and manuscript continuity.
- Use `map-making-local` for map reconstruction, cartographic rendering, symbol grammar, and visual map QA.
- Do not use `dnd-local` unless the user explicitly switches to DND project work.
- Do not use `homebrewery-local` unless the user explicitly asks to work in Homebrewery; Wolfdream is normally manuscript/document work, not brew work.

## Source-of-truth model

Use local files as the authoritative source of truth:

1. The reprise brief is the compact canon index.
2. The manuscript, timeline, plan, character bible, chronology, and map are the detailed canon sources.
3. Memories may be used only as a routing/high-salience index, not as higher-priority truth.
4. If memory conflicts with local project files, trust the local project file and surface the conflict.
5. At the end of meaningful work, fold durable decisions back into `Wolfdream - Brief de reprise.docx`.

## Resume procedure

1. Read `Wolfdream - Brief de reprise.docx` first.
2. Recall only Wolfdream/personal-project memories, and treat them as context rather than instructions.
3. Inspect the `C:\Personal stuff` folder tree only enough to confirm current artifacts and archive structure.
4. Read the exact artifact needed for the current task:
   - prose continuation or revision: active manuscript plus relevant plan section;
   - canon or timeline questions: timeline workbook first;
   - character consistency: character bible;
   - geography or map continuity: current map plus relevant geography notes.
5. Do not reread all past sessions unless local files are missing or contradictory.
6. Before editing `.docx` or `.xlsx`, load the appropriate document/spreadsheet skill and preserve the current file with a clear backup under `C:\Personal stuff\Wolfdream\Archive\Backups`.
7. If a file is open or locked, pause and ask the user to close it instead of creating a duplicate workaround.

## Fallbacks

- If the reprise brief is missing or stale, inspect the active manuscript, plan, timeline, character bible, and chronology enough to rebuild a short session brief before writing.
- If `.docx`/`.xlsx` editing tools are unavailable, do not write a lossy replacement; produce a local plain-text draft under `C:\Personal stuff\Wolfdream\Archive\Drafts` or ask the user how to proceed.
- If canon sources conflict, preserve both possibilities in the brief and ask for a decision rather than silently choosing.
- If a file is locked, stop and ask the user to close it; do not create a parallel "final final" duplicate.
- If generated text changes canon, update the reprise brief with the decision before ending the session.

## Canon checkpoints

- Present-day main chapters use third-person present.
- Fragments use a distinct classical past register with passe simple, imparfait, and occasional passe compose.
- Fragments veil identities by archetype; Rachelle may be named because the family knows her as Clarisse.
- Julian is the Voleur in Fragments; Brock is the Druide; Rei the Traqueur; Basile the Guerrier; Achille the Boiteux; Rachelle the Guerisseuse.
- Brock must remain slow-burn: early scenes should not clearly reveal that he knows Basile or the children's family history.
- Charlene functions as Brock's redemptive archetype: she gives him the chance to act where he could not save Rachelle, and the threat falls exactly within his druidic expertise.
- The Lacs d'Argent tragedy happened 15 years before the novel.
- Grande-Rive is Achille's care/logistics city on the Route du Roy toward the east, distinct from Longue-Halte.
- Oroks are originalized feathered bipedal mounts/work animals; avoid generic horse substitution.
- Current focus: maps are satisfactory for now; return focus to prose/text development, especially Brock and the next section of the V3 manuscript.

## End-of-session maintenance

At the end of meaningful Wolfdream work, update `Wolfdream - Brief de reprise.docx` with:

- current active manuscript state;
- latest canon decisions;
- changed narrative metadata;
- files modified and backups created;
- next recommended writing step.

Keep the brief short enough to read at the start of every new conversation.
