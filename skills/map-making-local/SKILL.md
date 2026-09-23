---
name: map-making-local
description: Personal local-only cartography workflow for fictional, fantasy, TTRPG, Wolfdream, and DND maps under C:\Personal stuff. Use for readable map design, reconstruction, iteration, and validation. Never register or deploy this skill to m-skills.
---

# Map-making Local Skill

Use this personal skill when the user asks to create, revise, reconstruct, or continue a fictional/fantasy/TTRPG map, especially for Wolfdream or another personal creative project. The goal is not just to draw a pretty image: build a readable, geographically coherent, narrative-useful map through explicit cartographic reasoning and iterative validation.

## Personal / non-business boundary

- Treat this as a personal creative lane.
- Do not use work/M365 data, WorkIQ, Outlook, Teams, SharePoint, FTOP, Lynx, FTBI, S360, Seismic, enterprise MCP servers, customer systems, or enterprise skills.
- For Wolfdream artifacts, ring-fence all file access to `C:\Personal stuff` and its subfolders.
- Refuse to read from or write to any path outside `C:\Personal stuff` unless the user explicitly confirms a one-off exception.
- This is a personal local skill only. Do not register it with Scout, do not copy it into `~\.scout\m-skills` or `~\.copilot\m-skills`, and do not try to make it pass Skill Guard.
- Do not mix map artifacts with FastTrack/work skill folders, work datasets, customer data, tenant data, or M365-derived content.
- If the user asks to prepare a file for personal printing or personal sharing, prefer the Purview `Non-business/Personal` sensitivity label when available; do not apply labels automatically without an explicit request.

## Routing and related local skills

- Use `wolfdream-local` when the map task depends on Wolfdream prose canon, timeline, character canon, or French-language manuscript decisions.
- Use `dnd-local` when the map belongs to a DND campaign project and needs quest/location/faction continuity.
- Use `homebrewery-local` only if the final map/source needs to be referenced or embedded in a Homebrewery brew.
- Stay local: no enterprise skills, no m-skills deployment, and no shared-skill runtime edits.

## Core philosophy

Readable geography comes before decoration. Start with a usable regional map, then add narrative layers, then add manuscript/fantasy styling. Avoid dense relationship diagrams and overloaded lore overlays. A good result should answer: where can characters go, by which route, through what terrain, with what obstacle, and what landmarks guide them?

For Wolfdream specifically, preserve the learned design direction unless the user changes canon:

- Regional, zoomed-out map around roughly a 50 km scale.
- Post-apocalyptic fantasy Quebec/Montreal inspiration, transformed into original worldbuilding.
- Ile du Royal has no active settlement and no active roads; it should feel ruined, isolated, and dangerous.
- The fleuve must visibly wrap around the island, including north, west, and south channels when relevant.
- Route du Roy / main Rive-Sud route is the key travel artery.
- Tarenn is a port town reached logically by south-shore travel plus ferry, not by an active road across Royal.
- Port-aux-Cendres is the ferry/service village facing Tarenn.
- Lacs d'Argent works better as a direct label when space permits, not necessarily as a numbered legend item.
- Ponts morts are ruins/sites, represented by paired markers on opposite banks.

## Intake checklist

Before drawing, extract or ask for:

1. Map purpose: novel frontispiece, TTRPG play aid, route planning, political map, regional overview, encounter map, or narrative overlay.
2. Scope and scale: region size, zoom level, rough travel distances, expected page/image size.
3. Geographic anchors: water, mountains, settlements, roads, forests, marshes, ruins, borders, landmarks.
4. Travel logic: main roads, secondary routes, trails, ferry crossings, blocked routes, seasonal passages, hazards.
5. Narrative priorities: which places need labels, which can be numbered, which should be implied only.
6. Style target: utilitarian topographic, clean TTRPG, parchment/manuscript, Tolkien-like fantasy, or hybrid.
7. Existing artifacts: inspect prior versions before changing direction; prefer continuing from editable source when present.

## Workflow

1. Inspect existing artifacts first.
2. Prefer rebuilding from editable source over pixel-editing a rendered PNG.
3. If only PNG exists, say so and either retouch carefully or reconstruct an editable source.
4. Separate base geography, human layer, narrative layer, and presentation layer conceptually.
5. Build a symbol grammar before rendering.
6. Control label density: use either a direct label or a number, not both, unless there is a strong readability reason.
7. Iterate in named versions and preserve prior versions.
8. Add manuscript/fantasy finish only after geographic validation.

## Fallbacks

- If editable source exists, use it as the base and preserve the previous version before changing it.
- If only a rendered image exists, create a new editable reconstruction source when the requested change is structural; use pixel retouching only for small cosmetic fixes.
- If the prompt is under-specified, produce a low-risk draft map plan or ask for the missing anchor rather than inventing key canon.
- If image generation or rendering produces illegible labels, simplify labels/legend and regenerate rather than layering corrections on a bad base.
- If a generated artifact lands outside `C:\Personal stuff`, move it into the active personal project folder or delete it.
- If map work touches Homebrewery, keep the rendered map and source in the local project first, then hand off to `homebrewery-local` for live brew updates.

## Recommended symbol grammar

- Large city: solid black circle.
- Village / hamlet / camp: black circle with white center.
- Mountain / summit: triangle.
- Point of interest / ruin / mill / monastery / cabin: black square.
- Dead bridge / crossing site: paired black squares on both banks.
- River: blue line.
- Fleuve / lake / marsh: blue area at scale.
- Main paved/royal road: thick or double black line.
- Dirt road: simpler black line.
- Secondary maintained route: spaced dashes.
- Small trail / animal path: dots.
- Biomes: pale textures or light fills, never heavy labels.

## Validation checklist

Before presenting a version as done, check:

1. Readability at normal viewing size.
2. No overloaded text or lore crowding.
3. Geography coherence.
4. Travel coherence.
5. Symbol consistency.
6. Label/number discipline.
7. Short, useful legend.
8. Scale/compass placement.
9. Canon consistency for Wolfdream.
10. Artifact hygiene: keep previous versions, include editable source when possible, and identify the recommended current version.

## Recovered Wolfdream progression

- v0.1 was too much like a relationship/narrative diagram and had too much overlaid information.
- v0.2 improved by separating geography and legend.
- v0.3 became the first usable map: readable geography, numbered places, separate key, routes/obstacles visible, lore removed from the image.
- v0.4 split physical/topographic map from narrative overlay.
- v0.5 established the symbol grammar.
- v0.6 used Montreal/OpenStreetMap only as broad geographic reference, zoomed out, showed fleuve channels around Ile du Royal, removed number bubbles, and used label-or-number discipline.
- v0.7 fixed travel logic: no roads on Royal, no direct road to Tarenn, south-shore route plus Port-aux-Cendres ferry, clearer channels, compass top-left, scale moved away from terrain text.
- v0.8 added hand-drawn/parchment/manuscript finish while preserving v0.7 geography.
- v0.9 simplified the legend, removed notes/subtext, extended the main road, and added Route du Roy.
- v0.10 removed marker number 3 while keeping the Lacs d'Argent text label.

## Response style

- Respond in French by default for Wolfdream map work unless the user uses English or asks otherwise.
- Lead with the created/updated artifact and the meaningful cartographic change.
- When a version is imperfect, say so plainly and fix it rather than pretending it is final.
- Prefer concrete design language: lisibilite, grammaire cartographique, logique de voyage, relief, hydrographie, routes, obstacles, legend/key, densite visuelle.

## Done condition

A map task is done only when the current version is saved, visually inspected, and the response identifies the recommended artifact path plus any limitation, such as `source editable missing; this is a PNG retouch`.
