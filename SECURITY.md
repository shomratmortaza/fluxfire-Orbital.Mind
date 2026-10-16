# Security Policy

## Reporting vulnerabilities

Report suspected vulnerabilities privately to the project owner before public disclosure. Include the affected page or workflow, reproduction steps, expected impact and whether any secret or user data may have been exposed.

## Secret handling

- Never commit real secrets, tokens, private keys, service credentials or downloaded session files.
- Use Lovable project secrets/runtime settings for server-only values such as AI Gateway access.
- Keep `.env.example` as a template only; local `.env` files are ignored.
- Public browser configuration may appear in local setup files, but private credentials must stay server-side.

## Application boundaries

- FLUXFIRE is an independent research workspace, not a NASA service or operational safety system.
- Server-side AI requests must not expose provider credentials to the browser.
- Imported evidence packages remain pending review and must not be promoted to verified catalog data automatically.
- Any future persistent intake or account feature must preserve row-level access controls and audited provenance.

## Dependency checks

Run dependency and application-security checks before release, and review findings manually for actual exploitability in this codebase. Do not suppress findings without a written reason.

```sh
bun run test
```

## Scientific-security overlap

Data integrity is part of the security model. Treat unsupported findings, altered citations, fabricated units and uncited AI prose as integrity failures, not cosmetic issues.