# FLUXFIRE · ORBITAL MIND

Independent microgravity-combustion evidence workspace. Not a NASA product, endorsement, fire-risk predictor or operational safety tool. Existing verified NASA records remain unchanged.

Copyright (c) 2026 Shomrat Mortaza.

## Overview

FLUXFIRE is an independent research workspace for NASA Physical Sciences Informatics (PSI) microgravity-combustion investigations: BASS-II (PSI-25), SAFFIRE-I (PSI-98) and FLEX (PSI-69). Every displayed value carries a source reference or is shown as an explicit unknown.

## Features

- Investigation explorer and detail pages (`/research`, `/research/$id`) with field-level provenance, original PSI experimental tables and selected raw numeric files (paged, CSV export).
- Field-matched search, condition-aware comparison (`/compare`) that discloses matching, differing and missing conditions.
- Workspace charts (`/app`) plotting only exact reported values with shared units.
- Evidence-readiness safety dashboard (`/safety`) — no fire-risk scores or spacecraft predictions.
- Cited AI research questions (`/assistant`) through the Lovable AI Gateway with a server-side exact-quotation citation gate.
- Source inventory (`/sources`), methodology, and staged CSV/JSON evidence import (`/import`) that never marks imports as verified.

## Architecture and technology stack

- TanStack Start v1 (React 19, SSR, server functions) built with Vite; deploys to an edge runtime (Cloudflare Workers compatible).
- Tailwind CSS v4 with semantic tokens in `src/styles.css`; shadcn/Radix UI primitives.
- TanStack Router (file routes in `src/routes`) and TanStack Query.
- Scientific data in `src/data/`; pure search/compare/stats logic in `src/lib/`; full raw rows load server-side only (`*.server.ts`) and reach the browser through paged server functions (`src/lib/raw-data.functions.ts`).
- Backend: Lovable Cloud (Postgres + auth via Supabase client libraries). AI: Lovable AI Gateway called from `src/lib/research-answer.server.ts`.
- Tests: Vitest (`src/test/`).

## Prerequisites

- Bun 1.1+ (or Node.js 20+ with npm).
- Optional: a Supabase-compatible Postgres project and a Lovable AI Gateway key for the cited-answer feature.

## Installation

```sh
unzip FLUXFIRE-source.zip && cd FLUXFIRE
bun install
cp .env.example .env   # fill in your own values
bun run dev            # http://localhost:8080
```

## Environment variables

See `.env.example`. `VITE_*` values are public browser configuration. `SUPABASE_SERVICE_ROLE_KEY`, `LOVABLE_API_KEY` and `LOVABLE_DB_MIGRATION_URL` are server-only secrets. No secrets are included in this repository. Without `LOVABLE_API_KEY` the cited-answer feature returns an explicit "insufficient evidence" response; all other pages work from bundled data.

## Database setup

The only table (`research_ai_access_state`) stores provider-denial state for the AI feature. Apply `drizzle/migrations/0000_research_ai_access_state.sql` to your Postgres database, or run `bunx drizzle-kit migrate` with `LOVABLE_DB_MIGRATION_URL` set. Scientific data is not stored in the database.

## Testing

```sh
bun run test   # Vitest suite in src/test
bun run build  # production build
```

## Deployment

Built for Lovable hosting (publish from the Lovable editor). The `vite build` output targets an edge/Worker runtime; to self-host, deploy the build with a Cloudflare Workers-compatible adapter and configure the environment variables above as runtime secrets.

## Usage

Start at `/` and open the workspace. Pick an investigation, inspect cited fields, page through raw tables, compare investigations, or ask a cited question. Check each source chip before reusing a value.

## Scientific limitations

FLUXFIRE does not produce fire-risk scores, safety predictions or new scientific results, and is not NASA-endorsed. Only some publications and raw files were accessible and reviewed; the rest are labelled unreviewed or listed-not-ingested. See `SCIENTIFIC_INTEGRITY.md` and `DATA_PROVENANCE.md`.

## Contributing and citation

See `CONTRIBUTING.md` and `CITATION.cff`.

## License

This project is released under the MIT License. See `LICENSE` for details.

## Security and scientific documentation

- `SECURITY.md`: vulnerability reporting, secret-handling expectations and dependency-check guidance.
- `.env.example`: non-secret local configuration template. Real secrets must stay in Lovable's secure runtime settings, never in committed files.
- `DATA_PROVENANCE.md`: source inventory, retrieval status, checksums, data-layer boundaries and known gaps.
- `SCIENTIFIC_INTEGRITY.md`: evidence rules, citation requirements, comparison limits and AI-answer guardrails.

## Reproduce

```sh
bun install
bun run dev
bun run test
```

TanStack Start / React / TypeScript / Tailwind. Tests include the original 13 checks plus evidence, search, comparison, storage and import checks. Development browser checks are described below; no live source verification runs automatically.

## Data and provenance

- `src/data/psi-records.json`: PSI-25 BASS-II, PSI-98 SAFFIRE-I, PSI-69 FLEX record metadata, 74 listed publication references (17/6/51).
- `catalog.ts`: source-supported conditions and experimental table parameters. `experimental-tables.json` retains all original CSV cells, headers, encodings, retrieval URLs and SHA-256 checksums; `raw-numeric-data.json` retains selected accessible NASA PSI numeric raw files with source IDs and SHA-256 checksums. Column mappings add per-cell citations. `Sourced<T>` is either a value with `SourceRef` or an explicit unknown; unknown is never zero. Scientific values live only in `src/data/`.
- `publication-reviews.ts`: separately retrieved publication content, exact quotations, named reviewed sections, URLs, methods, conditions and limitations. Publication-specific `SourceRef` adds `sourceId`, `url`, `locator`; it never redirects a paper citation to the PSI record.
- `/sources`: source-to-field table and all 74 publication entries with title-based priority, access/review labels. Priority is workflow triage, not evidence of findings. DOI presence does not establish access or review.

Evidence layers remain separate: primary experimental data; investigation metadata (objective/design/hypothesis/stated impact); publication metadata; reviewed publication statements; abstracts/summaries; derived analysis; AI interpretation; unavailable/unverified. No newly derived scientific result is claimed. Search excerpts are retrieval aids, not findings.

## Reviewed content (2026-10-16)

1. PSI-listed **Fire safety in space – beyond flammability testing of small samples**, DOI `10.1016/j.actaastro.2014.11.025`: author preprint retrieved from DTU Orbit; Introduction, Background, Saffire-1 Experimental Description, Conclusion reviewed. Pre-flight design and historical gaps only, no flight results. Printed pages differ from PDF page numbers; both are cited.
2. Supplemental **Results of Large-Scale Spacecraft Flammability Tests**, [NASA NTRS 20170008805](https://ntrs.nasa.gov/citations/20170008805): public full-text presentation transcript retrieved; named introductory, Saffire-1, conclusion sections and Table I reviewed. Reported 1.8 mm/s concurrent and 1.3 mm/s opposed spread rates are quoted from slide 21, not inserted into the PSI raw-measurement catalog. This is **not one of the 74 listed references**, and does not count as review of the 2018 journal paper.

3. PSI-listed **Microgravity Flammability of PMMA Rods in Concurrent Flow**, [NASA NTRS 20150008961](https://ntrs.nasa.gov/citations/20150008961): original conference manuscript retrieved; abstract, introduction, setup, quenching section and conclusions reviewed. Quench burns up to 28 minutes are cited to p. 4; approximate oxygen endpoints remain approximate. Radiometer uncalibrated. This does not review the related journal article.
4. PSI-listed **Concurrent flame growth, spread and extinction over composite fabric samples in low speed purely forced flow in microgravity**, [NASA NTRS 20150008962](https://ntrs.nasa.gov/citations/20150008962): original conference manuscript retrieved; abstract, introduction, experimental section, quenching discussion, conclusions and appendix reviewed. Conditions and 1–5 cm/s quenching range retain original units and section citations; limited tests and unreliable appendix oxygen readings are flagged.

Six original-content retrieval attempts are recorded in `publication-access.ts`; blocked publisher pages and uncorroborated search snippets do not establish review. **71 of the 74 listed references remain not content-reviewed**, including all 51 FLEX entries. Only named sections were reviewed; no full-library completion is claimed.

## Known gaps and attribution

- NASA PSI JSON and file-index metadata checked 2026-10-16. Records attribute CC0-1.0; that license is **not transferred to journal papers or author preprints**. Source authors and DOIs remain visible.
- Raw file listings are not downloaded datasets; unrestricted flags do not establish that download succeeded. Selected numeric raw files were retrieved and labelled separately: BASS-II fan calibration workbook, SAFFIRE-I Sample 2 calibrated telemetry, FLEX-007 droplet data and FLEX-007 LLUV flame data. Video/image archives and most raw files remain un-ingested.
- Original CSVs retrieved through `/geode-py/ws/studies/{accession}/download?file={bare-filename}&version=1&redirect=false`: parse its HTML redirect and fetch the temporary signed download. BASS-II has 129 data rows, SAFFIRE-I 4, FLEX 274 (header excluded). These are summary/test tables, not raw sensor files. All original rows are visible/exportable; chartable columns require explicit units. SAFFIRE chart selection remains the two specimen burns, not flow-visualization rows.
- FLEX original burning-rate header is `Burning rate; mm`; dimension is ambiguous. Values retained but not plotted. Original species headers O, N, CO are not chemically relabelled. BASS-II negative CO and anomalous final oxygen values remain unchanged; fan/air display values have no reported unit and are not treated as velocities.
- Pre-flight design thickness 0.3175 mm differs from PSI table 0.37 cm. Kept separately and flagged, never silently reconciled.
- Pressure, temperature and measurement methods are missing in parts of the catalog. No cross-record numerical comparison is enabled. BASS-II source-specific manuscript findings are now available; FLEX still has insufficient reviewed findings. PSI summaries remain metadata only.
- Topic insights remain design-level; reviewed presentation statements are not a validated topic-wide synthesis. No smoke toxicity dataset or cabin-level safety inference.

## Judge-priority fixes (2026-10-16)

Official awards text was read on spaceappschallenge.org/2025/awards: Science = best and most valid use of science/scientific method; Data = makes space data accessible or leverages it uniquely; Technology = most innovative use of technology. The Flame in Freefall challenge page did not render its statement in this environment, so challenge-specific requirements were not re-verified from its full text.

Five highest-impact weaknesses: (1) the assistant ignored reviewed findings and table values; (2) no observation-backed chart; (3) publication review states were not searchable or count-backed; (4) research results could not be exported with citations; (5) BASS-II/FLEX raw-table access remains blocked. Fixed 1–4. Real AI synthesis was deliberately not enabled: citation-ID validation alone cannot prove claim support, and the request also lacks rate limiting. Cloud is connected for future protected synthesis and reviewed intake.

This describes the earlier judging-audit milestone; subsequent extractive model answers are documented below. Free-form scientific synthesis remains withheld.

## Cited AI research questions

`/assistant` now offers independent, session-only AI questions through Lovable AI Gateway. The server retrieves indexed passages, streams model reasoning summaries separately (not verified evidence), and validates structured selections before displaying the answer. Only complete, exact indexed passages with original citations may appear; altered quotes, unknown IDs and publication-title-only claims are withheld. This deliberately provides **extractive evidence selection**, not free-form scientific synthesis. It cannot prove that a question is exhaustively answered or independently validate the cited science. Reviewed publication content is limited to the named sections above; the remaining listed papers remain metadata-only.

The server uses Responses with `openai/gpt-6-astra`, no automatic retries, explicit Stop, bounded question input (3–2,000 characters), original unit strings and safe failure messages. Provider denials are persisted in the server-only `research_ai_access_state` table and checked before a new model request; restoring access requires owner repair and explicit clearing of that paused state. There are no automatic/background jobs. There is no infrastructure rate limiter; one browser request at a time and input validation are not server rate limiting. Workspace AI credits apply. Scientific catalogs and review records are never mutated by the assistant.

## Safety dashboard

`/safety` summarizes selected BASS-II, SAFFIRE-I and FLEX evidence into source-linked fire-safety insight cards, raw-data mini charts, domain coverage and evidence-readiness rankings. The ranking is a documentation/readiness index based on available measurements, raw files, reviewed findings and known conditions; it is **not** a fire-risk score, spacecraft safety prediction or NASA endorsement. The dashboard's AI panel uses the same extractive citation gate as `/assistant`: if the model or evidence is unavailable, the app shows an insufficient-evidence state instead of unverified analysis.

Shared mobile navigation uses a focus-trapped dialog with Escape and focus return. Focus-visible outlines and skip links apply across the site. Apparatus silhouettes are decorative schematics, not experimental images or measurements; the FLUXFIRE logo and browser icon use the same flame/trajectory symbol.

Verification on 2026-10-16: 42 automated tests passed, including home link rendering and citation rejection regressions. Browser checks visited all 11 content screens at 1280×1800 and 390×844; verified one main/H1, no horizontal page overflow, visible keyboard focus, mobile menu Tab containment, Escape and return focus, and home link destinations without page errors. Real model requests returned cited BASS-II metadata and a reviewed publication quotation with its original preprint locator. Stop and no-evidence states were exercised; simulated 402/403/429 responses preserved their messages. Whole-project lint was executed but remains failing on existing formatting and one existing prefer-const issue; targeted functional lint of the new assistant and shared UI passed with formatting enforcement excluded. Provider-denial persistence was inspected in code, not induced against the live provider.

Coverage chart counts PSI-listed references only. Observation charts support all three investigations with exact same-unit values and source cells; approximate values, ranges and ambiguous units are excluded. Raw-file charts plot selected downloaded numeric streams. Negative values plot left of zero on a shared scale. CSV exports preserve reported value, unit, conditions, unknown method and source. Markdown briefs retain evidence class, ID, locator and limitations.

The older `/datamanager/file/...` links returned 404; the study resolver succeeded for all three experimental CSVs on 2026-10-16. Latest verification: 48 automated tests passed; browser sweep visited 13 screens at 1280×1800, 390×844 and 824×674 without page errors or horizontal page overflow. This does not verify raw instrument downloads or the remaining publication contents.

## Search, comparison, recent research

Pure functions in `src/lib/`. Search ranks exact identifier/title matches, metadata matches, then publication-title-only matches, with field/excerpt citations. The current PMMA query matches BASS-II metadata only; publication-only ranking is additionally tested with a clearly synthetic test fixture.

Comparison shows match/differs/missing. “Match” means identical indexed wording, not independently validated physical equivalence. Fuel-phase disagreement is non-comparable; missing phase/flow/oxygen is insufficient; known common phase/flow/oxygen can support qualified metadata reading. Direct/numerical comparison also requires matching material, geometry, oxygen, pressure, temperature, flow/direction, gravity, platform and known methods plus a shared variable and reported units. Table availability alone is insufficient.

Continue research is browser-local convenience history, not scientific storage: known IDs only, deduplicated, newest first; handles malformed or denied storage and updates on storage/change events. It is not account-synced.

## Safe import staging

`/import` validates CSV with Papa Parse and JSON with Zod. Required fields:

| Field | Requirement |
|---|---|
| id | Lowercase letters, digits, hyphens; unique in file and against NASA catalog |
| title | Source title |
| source | HTTPS URL or DOI `10.…/…` |
| evidenceType | experimental-metadata, publication, summary, primary-data |
| excerpt | Source-specific quotation |
| locator | Page, section, table row or source field |
| variable, value, unit, conditions | Additional requirements for primary-data; strings preserved verbatim |

Unknown fields/claimed verification are rejected. Maximum 2 MB / 500 rows. File-level and row-level errors shown in preview. Export enabled only when every row is valid; exported package has `verificationStatus: pending-review` and `candidates[]`. This review package is intentionally distinct from the input array. Preview is temporary, with no persistent record ingestion, automatic source verification, NASA verification status or catalog mutation. Human scientific review and persistent intake remain future work.

## Manual audit reproduction

Open BASS-II, then FLEX, return to `/app`, reload and follow Continue research: FLEX must open `/research/flex`. Search PMMA and inspect field excerpts. Open SAFFIRE-I reviewed content and follow paper-specific citations. Compare solids, add FLEX and inspect missing methods. Retrieve “gaseous fire suppressants” and “quantum banana” for positive/insufficient states. Upload a valid JSON/quoted CSV, export pending-review package, then upload duplicate/missing-field records and confirm export disabled. Check every content page at desktop and 390 px phone width; confirm mobile citations, scrolling tables, menu navigation and no page overflow.
