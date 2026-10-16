# FLUXFIRE Data Provenance

FLUXFIRE separates source metadata, reviewed findings, raw numeric files, derived workflow metadata and AI-selected passages. The application must never invent, normalize or silently transform scientific values.

## Source inventory

| Layer | Location | Status |
|---|---|---|
| NASA PSI records | `src/data/psi-records.json` | Verified metadata source for PSI-25 BASS-II, PSI-98 SAFFIRE-I and PSI-69 FLEX. |
| Curated catalog | `src/data/catalog.ts` | Source-linked conditions and observations only. Unknowns stay explicit. |
| Experimental summary tables | `src/data/experimental-tables.json` | Downloaded CSV rows with original cells, headers, retrieval URLs and SHA-256 checksums. |
| Selected numeric raw files | `src/data/raw-numeric-data.ts` | BASS-II fan calibration excerpt, SAFFIRE-I Sample 2 telemetry, FLEX-007 droplet and LLUV flame data. |
| Publication reviews | `src/data/publication-reviews.ts` | Only retrieved sections and exact quotations are treated as reviewed content. |
| Access attempts | `src/data/publication-access.ts` | Failed or blocked retrieval is recorded without converting snippets into evidence. |

## Provenance rules

- Every displayed scientific value must carry a `SourceRef` or be marked unknown.
- Original units and source cell text are preserved. Ambiguous units remain visible but unplotted.
- Table availability is not equivalent to reviewed scientific interpretation.
- Publication metadata, NASA metadata, reviewed findings, raw measurements, derived summaries and AI interpretation remain separate.
- Checksums document retrieved files; they do not imply NASA endorsement or completeness.

## Currently accessible numeric data

- BASS-II: selected fan calibration workbook excerpt. Fan display values are calibration display readings, not test-wise airflow velocities.
- SAFFIRE-I: Sample 2 calibrated telemetry including O₂, CO₂, pressure, temperatures and fan speed columns.
- FLEX: FLEX-007 droplet diameter data and LLUV flame-diameter/standoff numeric data.

## Metadata-only or incomplete areas

- Most listed publications are not content-reviewed.
- Video/image archives and most raw-file formats are not ingested.
- BASS-II test matrix, SAFFIRE Sample 1 files and one Sample 2 workbook duplicate were not treated as confirmed raw numeric sources when retrieval failed.

## Dashboard derivations

The safety dashboard computes evidence-readiness from catalog coverage, raw-file presence, reviewed findings and known conditions. This is workflow metadata only. It is not a fire-risk score, spacecraft safety prediction or validated safety model.