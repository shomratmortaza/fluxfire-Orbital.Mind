# Contributing to FLUXFIRE

Thanks for helping improve FLUXFIRE.

## Setup

```sh
bun install
bun run dev
bun run test
```

## Rules

1. Scientific values live only in `src/data/` and must carry a source reference (`SourceRef`) or be an explicit unknown. Never guess, round or convert reported values.
2. Do not add fire-risk scores, safety predictions or claims of NASA endorsement.
3. Imported evidence stays pending review; it is never added to the verified catalog automatically.
4. Keep search, comparison and stats logic as pure functions in `src/lib/` with tests in `src/test/`.
5. Never commit `.env` files, API keys or tokens. See `SECURITY.md`.

## Pull requests

- Describe what changed and which sources support any data change (URL, file, checksum, locator).
- Run `bun run test` and `bun run build` before opening a PR.
- Keep UI changes within the existing design tokens in `src/styles.css`.
