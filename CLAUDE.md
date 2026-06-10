# CLAUDE.md — keithnelson.cv (visual CV site)

Context briefing for Claude Code (or any AI assistant) working on this repo.
Read this fully before changing anything.

## What this is

Keith Nelson's personal CV website, live at **https://keithnelson.cv**.
Keith is a climate & energy transition consultant in Barcelona (owner of
New Day Climate) pivoting into renewable energy roles. This site is the
"visual CV" — a designed one-page A4 layout. A separate traditional .docx CV
exists outside this repo (Keith has it locally) and is the source of truth
for facts.

## Files

- `index.html` — the entire site. Single self-contained page: A4 print layout
  + `@media screen` wrapper (dark sage backdrop, centered page, floating
  Download PDF button hidden in print). Fonts: Lora (serif display) + Lato
  (body), loaded from Google Fonts for browsers; WeasyPrint uses locally
  installed versions when generating the PDF.
- `Keith_Nelson_CV.pdf` — the downloadable PDF, **generated from index.html**
  via WeasyPrint. Regenerate after any content change:
  `pip install weasyprint && python -m weasyprint index.html Keith_Nelson_CV.pdf`
  NOTE for Windows (Claude Code on Keith's PC): WeasyPrint needs GTK and often
  fails to install. Use headless Chrome/Edge instead — renders the same
  @media print CSS:
  `"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --headless --print-to-pdf="Keith_Nelson_CV.pdf" --no-pdf-header-footer "index.html"`
  (or `chrome.exe` with the same flags). If neither works, ask Keith to request
  the regeneration in his Claude Cowork session, which has WeasyPrint.
  Then verify it is still exactly 1 page (`pdfinfo`) and visually check a
  render (`pdftoppm -jpeg -r 100 Keith_Nelson_CV.pdf check`).

## Hosting & DNS

- Host: Netlify, site name `jade-tarsier-7ae169` (Keith's account).
- Deploy method: as of 2026-06-10, manual zip drag onto Netlify Deploys tab.
  PLANNED: link this GitHub repo in Netlify (Site configuration → Build &
  deploy → Link repository; no build command, publish directory = root).
  Once linked, every push to `main` auto-deploys and zip-dragging stops working.
- DNS at Namecheap: `A @ 75.2.60.5`, `CNAME www → jade-tarsier-7ae169.netlify.app`.
  HTTPS via Netlify-managed Let's Encrypt. Don't touch DNS unless asked.

## Hard-won rendering gotchas (do not regress these)

1. **No borders on rounded pill chips.** WeasyPrint draws border + fill as
   slightly offset arcs → "double bubble" artifact in the PDF. Chips are
   borderless white pills. If an outline is ever needed, test the PDF at
   300dpi zoom first.
2. **Pixel borders, not mm.** Sub-pixel mm borders (0.25mm) render broken in
   Edge/Chromium on screen. All hairlines are ≥1px.
3. **One page is a hard constraint.** `.cols` has fixed height 249mm with
   overflow hidden; total = header 34mm + statband 14mm + cols 249mm = 297mm.
   If content grows, cut oldest bullets first; never go below ~8pt body.
4. The HTML must stay self-contained (inline CSS, no JS, no build step).

## Content rules (honesty constraints from Keith — do not violate)

- Keith was Director of **Operations** of the USAID ACE program, NOT the
  program director (there was a Chief of Party above him). The $77M loans /
  32,000 farmers / 31 provinces outcomes belong to the program, phrased as such.
- Kabul team size: 50 staff (confirmed by Keith over LinkedIn's "30+").
- El Salvador: remote work only — Keith never worked there on the ground.
  It was removed from the CV entirely; don't re-add.
- Chile & Peru on-the-ground work happened under Deloitte (2015–19).
- Deloitte: he developed the sustainable operations offering for Deloitte
  **Spain** (not global) and delivered it for Canon. Don't say he "designed
  Deloitte's sustainability offering."
- No Rio Tinto in the client list (was a client; Keith chose to omit).
- University of Salamanca 2018 = "Postgraduate Degree" (título propio, not an
  official Spanish government master) — never "MA" or "Master".
- Keith dislikes the term "ESG" — avoid it. Use climate transition strategy,
  sustainability strategy, etc.
- Company name: **New Day Climate**. Email: keith@newdayclimate.com.
- Every factual claim must trace to Keith's traditional CV or his explicit
  statements. Never invent metrics, clients, or dates.

## Design system

- Colors: green `#1B6B4A`, deep `#14523A`, tint `#EDF4F0`, line `#BFD8CC`,
  ink `#2B2F2D`, grey `#6A736E`. Screen backdrop `#39463F`.
- Layout: full-width header → green stat band (5 stats) → 64mm tinted sidebar
  (skills as grouped chips — NEVER skill bars/percentages, languages,
  education, global footprint) + main column (career timeline with dots,
  "Beyond work" box at the end).
- Tone: senior, credible, restrained. One accent color. No headshot, no icons
  beyond what exists, no decorative clutter.

## History

- 2026-06-10: CV content overhauled in Claude Cowork session (repositioned for
  renewables/energy-transition roles), visual CV designed, domain bought at
  Namecheap, Netlify deploy, this repo created. v1 design archives live in
  Keith's local Cowork outputs folder (`archive_v1/`).
