---
name: homebrewery-local
description: Personal local-only workflow for editing GrimPhantom Homebrewery brews. Use for Homebrewery source extraction, local draft preparation, authenticated browser edits, page-break/layout tuning, and rendered verification. Never register or deploy this skill to m-skills.
---

# Homebrewery Local Skill

Use this personal skill when the user asks to create, inspect, edit, repair, or update a Homebrewery brew for their personal DND projects.

This is a local personal skill only. Do not register it with Scout, do not copy it into `~\.scout\m-skills` or `~\.copilot\m-skills`, and do not attempt to make it pass Skill Guard. Keep it under `C:\Personal stuff\Scoutstuffs\skills\homebrewery-local`.

## Boundaries

- Work only with personal DND / Homebrewery content, normally under `C:\Personal stuff\DND`.
- Do not use enterprise data, customer data, M365 work content, FastTrack tools, internal Microsoft systems, or shared enterprise skills.
- Do not write Homebrewery exports or drafts into `C:\Users\oducharme\OneDrive - Microsoft\Documents\Microsoft Scout`; that is governed enterprise space.
- Keep intermediate source files in the relevant personal project folder, usually `...\Homebrewery\`.
- Treat official DND adventure books and copyrighted non-SRD text carefully: use user-owned/user-provided sources, public summaries, transformed notes, and original drafting. Do not copy protected boxed text, maps, stat blocks, or room text into the brew unless the user has provided and requested transformation of that specific content.
- If this skill is used with a non-DND personal Homebrewery brew, confirm the project folder under `C:\Personal stuff` before reading or writing local files.

## Account and login

- Homebrewery/NaturalCrit username: `GrimPhantom`.
- Preferred Windows Credential Manager target: `homebrewery:GrimPhantom`.
- Never print, store, paste into chat, or write the Homebrewery password into a file.
- If editing requires authentication:
  1. Open the edit URL in the browser.
  2. If NaturalCrit shows "User is not logged in", navigate to `https://www.naturalcrit.com/login?redirect=<edit-url>`.
  3. Fill username `GrimPhantom`.
  4. Retrieve the password only from Windows Credential Manager and paste it into the focused password field without exposing it in chat or logs.
  5. Clear the clipboard after use.
- The password paste approach that worked:
  - Use Playwright to focus the password textbox.
  - Use a local PowerShell script to read `homebrewery:GrimPhantom` via `CredRead`, temporarily place only the password on the clipboard, send `Ctrl+V`, then restore or clear the clipboard.
- Avoid using Playwright `run_code_unsafe` to call `require('child_process')`; that failed because `require` was not available in the browser context.

## Safety invariants

- Draft locally before changing a live brew.
- Never paste a password, source blob, or credential into chat.
- Never leave the password or full brew source on the clipboard after the operation.
- Never update a live brew through direct API calls unless Homebrewery's expected diff/hash/version payload is fully reproduced and tested; prefer the editor/autosave path.
- Before a live write, identify the exact section or full source that will be replaced.
- After a live write, verify both source and rendered iframe with cache busting.

## Homebrewery URLs and API facts

For a brew with share id `<shareId>` and edit id `<editId>`:

- Share/render page: `https://homebrewery.naturalcrit.com/share/<shareId>`
- Source page: `https://homebrewery.naturalcrit.com/source/<shareId>`
- Edit page: `https://homebrewery.naturalcrit.com/edit/<editId>`
- Update endpoint seen in the client: `PUT https://homebrewery.naturalcrit.com/api/update/<editId>`

The source endpoint returns rendered HTML wrapping the source:

```html
<code><pre style="white-space: pre-wrap;">...</pre></code>
```

Always strip this wrapper and HTML-decode the body before treating it as brew source. If the decoded source begins with one or more metadata code fences, those fences are Homebrewery metadata and may render as visible text if duplicated or pasted incorrectly.

Use cache-busting query strings when verifying source or rendered pages:

- `...?cb=<timestamp>`
- Add request header `Cache-Control: no-cache` from PowerShell where possible.

## What worked well

### Reading source

PowerShell plus `Invoke-WebRequest` worked reliably:

```powershell
$raw = (Invoke-WebRequest -Uri "https://homebrewery.naturalcrit.com/source/<shareId>?cb=$((Get-Date).Ticks)" -UseBasicParsing -Headers @{"Cache-Control"="no-cache"}).Content
if ($raw -match '(?s)^<code><pre[^>]*>(.*)</pre></code>\s*$') {
  $source = [System.Net.WebUtility]::HtmlDecode($matches[1])
} else {
  $source = $raw
}
```

Then remove leading metadata fences only when preparing body text for the editor:

```powershell
$body = $source -replace '^(?:```metadata\r?\n[\s\S]*?\r?\n```\r?\n\s*)+',''
```

### Editing source in the browser

Homebrewery uses CodeMirror. The editor view was available through:

```javascript
document.querySelector('.cm-content')?.cmTile?.view
```

This worked for reliable full-document replacement:

```javascript
const view = document.querySelector('.cm-content')?.cmTile?.view;
const text = await navigator.clipboard.readText();
view.focus();
view.dispatch({ selection: { anchor: 0, head: view.state.doc.length } });
// Then use browser keyboard Ctrl+V so Homebrewery's own editor/autosave path runs.
```

Using the native paste path is safer than trying to POST the API directly because Homebrewery computes internal diff patches, hashes, and version checks.

### Render inspection

The rendered brew lives inside an iframe titled "Rendered Brew Content". Inspect it with:

```javascript
const doc = document.querySelector('iframe')?.contentDocument;
const pages = [...doc.querySelectorAll('.page')];
```

Useful render checks:

```javascript
const text = doc.body.innerText || '';
const report = {
  metadataVisible: text.trimStart().startsWith('title:'),
  pageCount: pages.length,
  pageStarts: pages.map((p, i) => ({
    page: i + 1,
    start: p.textContent.trim().slice(0, 100),
    end: p.textContent.trim().slice(-140)
  }))
};
```

Inspect page fit with `.columnWrapper` measurements. Treat screenshots as a supplement, not the sole verification.

## What did not work / avoid

- Do not paste the raw `/source/<shareId>` response directly into the editor. It contains an HTML wrapper and can make the metadata/code wrapper display in the rendered brew.
- Do not rely on PowerShell process substitution like `<(echo '')`; that is Unix shell syntax and fails in PowerShell.
- Do not use direct `PUT /api/update/<editId>` unless you fully reproduce Homebrewery's client payload. Direct API calls failed with version/hash conflicts when missing the expected patches/hash values.
- Do not use only `page.keyboard.press('Control+A')` against the visible editor and assume it selected the full document. It can select the viewport/cursor region only. Use the CodeMirror view selection first.
- Do not trust `/source/<shareId>` alone for final layout verification. The source endpoint may include metadata fences that Homebrewery consumes correctly. Verify the rendered iframe.
- Do not leave the Homebrewery password or full brew source on the clipboard after use.

## Optimized workflow

### 1. Identify brew ids

From user context or an existing project note, collect:

- Share URL / share id.
- Edit URL / edit id.
- Local project folder where drafts should be stored.

If only a share URL exists, read source from `/source/<shareId>` and ask for or locate the edit URL only when a write is needed.

### 2. Fetch and normalize source

Read `/source/<shareId>` with cache busting. Strip the `<code><pre>` wrapper and HTML-decode it.

Keep two local files when doing meaningful edits:

- `*-current-source.md` - fetched source/body used as the baseline.
- `*-updated-source.md` or a named replacement block - proposed updated source.

Store these under the project `Homebrewery\` folder.

Fallbacks:

- If `/source/<shareId>` is unavailable, use the rendered share page only for visual inspection and ask the user for the source/edit link before writing.
- If the source contains unexpected metadata or wrapper duplication, save a local backup before normalizing it.
- If source parsing fails, stop and inspect a small source excerpt rather than performing regex replacements blindly.

### 3. Draft locally first

Make all substantive text changes locally before touching Homebrewery.

For replacement tasks:

1. Locate exact section headings in the source.
2. Replace only the target block.
3. Preserve surrounding sections and exact heading levels.
4. Remove planning/meta language.
5. Use Homebrewery-compatible Markdown:
   - `##` for major keyed location headings.
   - `###` for subareas.
   - `***Access.***`, `***Treasure.***`, `***Development.***` for official-style callouts.
   - `\page` on its own line for page breaks.
   - `\column` on its own line for column breaks only when genuinely useful.

### 4. Login only when ready to write

Open the edit URL. If login is required, use the Windows Credential Manager workflow above.

### 5. Update through the editor, not raw API

Copy the final clean source body to clipboard.

In the edit page:

1. Get CodeMirror view from `document.querySelector('.cm-content')?.cmTile?.view`.
2. Select the full document through `view.dispatch({ selection: { anchor: 0, head: view.state.doc.length } })`.
3. Paste with browser keyboard `Ctrl+V`.
4. Wait for Homebrewery autosave.
5. Clear the clipboard.

Fallbacks:

- If `.cm-content?.cmTile?.view` is unavailable, do not use blind keyboard replacement. Inspect the editor DOM and ask before proceeding.
- If autosave does not persist, reload the edit page, confirm the current server version, and retry through the editor path.
- If a bad paste occurs, immediately restore from the saved local clean source using the same editor path, then verify the rendered page.

### 6. Verify source and render

Verify source:

- No old target block remains.
- New target heading exists.
- Intended `\page` count and placement exists.
- No accidental `<code><pre` wrapper exists in source body.

Verify render:

- Metadata is not visible as body text.
- Page count is expected.
- Page starts and ends make sense.
- New sections do not split awkwardly across page boundaries.
- Logical blocks are kept together when practical.
- If a page starts or ends badly, adjust `\page` markers and repeat.

### 7. Page-break strategy

Homebrewery does not automatically paginate the way a writer expects. Use manual `\page` breaks after rendered inspection.

Guidelines:

- Prefer starting major location sections on a new page only when the prior page is already full enough.
- Do not force every subsection onto its own page; that creates excessive blank space.
- Keep room blocks together where possible:
  - Description.
  - Access.
  - Treasure.
  - Development.
- For long locations, break at clean subarea boundaries.
- For the Cragmaw Castle C16 pattern that looked good:
  - Let C16 intro/general features begin on the same page as preceding C13/C14 continuation if it fits.
  - Start B1 on the next page.
  - Let B1-B4 flow together.
  - Start B5 on the next page.
  - Let B5-B8 flow together.
  - Start B9 on the final page with "Leaving the Basement" and "What's Next?" if it fits.

### 8. Done condition

A Homebrewery task is done only when:

- The live rendered page was inspected after cache-busting.
- The visible metadata/header issue is absent.
- The requested source block was changed and unrelated sections were not modified beyond formatting/page-flow needs.
- The final source/body is saved locally in the personal project folder if it may be useful later.
- The clipboard is cleared if it held a password or full source.
