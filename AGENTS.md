<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.
<!-- LOVABLE:END -->

# FLUXFIRE agent rules

- Scientific data lives only in `src/data/` (`psi-records.json` from NASA PSI JSON + `catalog.ts`); every displayed value must carry a `SourceRef` or be an explicit unknown — UI never invents or transforms science values.
- Search, comparison, retrieval and stats are pure functions in `src/lib/` covered by `src/test/science.test.ts` — keeps ranking and readiness rules auditable.
- No fire-risk scores or AI-generated answers unless a real model and citation validation are wired server-side.
- App routes wrap content in `components/ff/AppShell`; landing (`/`) has its own layout.
- Evidence imports are validated with Zod and Papa Parse in an isolated browser preview and exported as pending-review packages, never added to the verified catalog; this prevents unreviewed claims entering scientific workflows.
- Publication review data belongs in `src/data/` with section-specific quotes and access scope; inventory prioritization is workflow metadata, never evidence of findings.
- Continue research uses validated browser-local history and storage/change notifications; storage denial must not interrupt record access.
- Charts and exports derive only from catalog observations with exact reported values and shared units; approximate values, ranges and unknowns stay visible but unplotted to avoid fabricated precision.

- Shared mission-control typography and motion live in global tokens and ff primitives; all decorative movement honors reduced-motion and never represents live scientific telemetry.
- Cover composition and workspace hierarchy use dedicated shared CSS hooks; navigation stays neutral while scientific content and evidence states retain semantic accents, avoiding decorative telemetry or per-page restyling.
- Investigation apparatus silhouettes are shared decorative schematics identified as such; they never stand in for source imagery or scientific observations.
- Research questions are independent, non-persistent requests; AI selects complete indexed source passages, and a server-side exact-text citation gate withholds altered, unknown and title-only claims to avoid invented scientific prose.
- Research AI uses server-only Responses streaming with explicit Stop and no automatic replay; durable provider-denial state is application-owned and checked before calls to prevent repeated terminal failures.
- Shared navigation uses a Radix dialog for the mobile menu and semantic focus tokens, preserving keyboard trapping, Escape and trigger-focus restoration.
- Source, independence and visualization disclosures share one data-backed disclosure component across landing and workspace pages so their wording remains consistent.
- Downloaded PSI experimental tables and selected raw numeric files retain original cells, units, source IDs and checksums in src/data; column-specific mappings provide citations and withhold ambiguous units from plots so summary tables are never reclassified as raw sensor data.
- Full raw numeric rows load only server-side (`raw-numeric-rows.server.ts`) and reach the browser as paged server-function results; the client bundle carries metadata only, keeping pages fast.
