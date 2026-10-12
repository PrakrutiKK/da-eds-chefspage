# Chef Page Figma → EDS Design Migration Plan

**Goal:** Analyze the chef page design from Figma and migrate its visual design into the AEM Edge Delivery Services (EDS) project.

**Mode:** Plan only — execution requires Execute mode.

## Answer: Will a Figma PAT unlock this file?

**No — a Personal Access Token won't help here.** The blocker is the **file type**, not authentication. The API rejected the request with:

`Figma API error (400): "File type not supported by this endpoint"`

That is a *type* error, not a *401/403 permissions* error. The link you shared is a **Figma Make** app (`figma.com/make/...`) — Figma's AI app-builder product. The design-extraction tools (`get_metadata`, `get_design_context`, `get_screenshot`, `get_variable_defs`) operate only on standard **Figma design files** (`figma.com/design/...` or `figma.com/file/...`). A PAT only changes *whether you're allowed in*; it can't make a Make file readable by an endpoint that doesn't support that format.

### What actually unlocks it
1. **Best:** In the Figma Make project, export/open the result as a regular Figma **design file**, then share that `figma.com/design/...` URL **with a `node-id`** for the chef page frame.
2. **Alternative:** Provide **screenshots** of the Make design and I'll migrate visuals from those (less precise — no exact tokens/measurements).

## Current Repo State (already inspected)

- **Project:** `eds-chefspage` (xwalk boilerplate), source site `unileverfoodsolutions.co.uk` / `.nl`.
- **Chef page content:** `content/chefpage.plain.html` — currently one section using `cards-theme` plus page metadata.
- **Existing chef block:** `blocks/columns-chef/` (avatar + name rows) with minimal, non-design-matched CSS.
- **Existing blocks available for reuse:** `cards-theme`, `cards-article`, `cards-recipe`, `carousel-hero`, `carousel-product`, `carousel-recipe`, `columns-*`, `hero`, `hero-newsletter`, `tabs-brand`, etc.
- **Global tokens:** `styles/styles.css`.

## Checklist

- [ ] **1. Get a supported Figma source** — either a `figma.com/design/...` / `figma.com/file/...` URL **with a `node-id`**, or screenshots of the Make design (a PAT alone does not resolve the Make-file limitation).
- [ ] **2. Extract Figma structure** — run `get_metadata` on the chef page node to map the frame/layer hierarchy and section layout.
- [ ] **3. Capture Figma visual reference** — run `get_screenshot` on the chef page node and key sub-frames for pixel-level comparison.
- [ ] **4. Extract design tokens** — run `get_variable_defs` to pull colors, typography, spacing, and radii; compare against current `styles/styles.css` global tokens.
- [ ] **5. Pull per-section design context** — run `get_design_context` on each major section node for exact computed styles and asset download URLs.
- [ ] **6. Map Figma sections → EDS blocks** — match each design section to an existing block (`cards-theme`, `columns-chef`, etc.) or flag where a new block/variant is required.
- [ ] **7. Gap analysis** — for each mapped block, document deltas between current EDS CSS and the Figma design (color, type, spacing, layout, imagery).
- [ ] **8. Migrate block design (CSS)** — update block CSS to match Figma exactly: mobile-first, 600/900/1200px breakpoints, selectors scoped per project conventions; download/optimize any required assets.
- [ ] **9. Update content/model if needed** — adjust `chefpage.plain.html` and any `_{block}.json` models; run `npm run build:json` if models change.
- [ ] **10. Visual verification** — render the chef page in the local preview, compare against the Figma screenshots, and iterate (snapshot/evaluate first, screenshot only for final QA).
- [ ] **11. Lint** — run `npm run lint` and fix any issues.
- [ ] **12. Report** — summarize matched sections, intentional deviations, new assets, and remaining follow-ups.

To proceed: provide a Figma **design-file** link (with `node-id`) or screenshots, then switch to Execute mode. A PAT by itself will not make the Make file accessible.
