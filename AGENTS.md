# Repository Guidelines

## Project Structure & Module Organization
- `src/main.js`: Imports Flomo HTML into Memos.
- `src/weixin.js`: Imports WeRead notes from `weixin.txt`.
- `src/delete.js`: Deletes memos listed in `sendedIds.json`.
- `src/utils/api.js`: Memos API calls, throttling, and request headers.
- `src/utils/utils.js`: Argument parsing, path helpers, and shared utilities.
- `assets/`: README screenshots and static images.
- Runtime output files in repo root: `memo.json` and `sendedIds.json`.

## Build, Test, and Development Commands
- `pnpm install`: Install dependencies.
- `pnpm lint`: Run ESLint for the whole repository.
- `node ./src/main.js <api-host> <access-token> ./flomo/index.html`: Import Flomo export.
- `node ./src/weixin.js <api-host> <access-token> ./weixin.txt`: Import WeRead notes.
- `node ./src/delete.js <api-host> <access-token>`: Remove previously imported memos.

Use Node.js LTS and `pnpm` to match the lockfile workflow.

## Coding Style & Naming Conventions
- Follow `.editorconfig`: 2 spaces, LF, UTF-8.
- Follow `.prettierrc`: `printWidth: 120`, double quotes.
- Use CommonJS (`require`, `module.exports`) consistently.
- Naming: variables/functions `camelCase`, constants `UPPER_SNAKE_CASE`, utility files in lowercase (for example `api.js`, `utils.js`).
- Keep scripts deterministic and CLI-oriented; avoid hidden global state.

## Testing Guidelines
- No automated test suite is currently checked in.
- Before opening a PR:
  - Run `pnpm lint`.
  - Run the target import script with a small sample file.
  - Verify created memo order, tags, resources, and timestamps in Memos UI.
  - If import fails, confirm `sendedIds.json` content, then validate rollback with `node ./src/delete.js ...`.

## Commit & Pull Request Guidelines
- Follow Conventional Commit style seen in history: `fix: ...`, `feat: ...`, `build(deps): ...`.
- Keep commit scope narrow (one behavior change per commit).
- PRs should include:
  - What changed and why.
  - Target Memos API/version assumptions (for example `v1` vs `v2` paths).
  - Reproduction and verification commands.
  - Before/after evidence for import behavior when output format changes.

## Security & Configuration Tips
- Never commit real access tokens or host URLs containing secrets.
- Use placeholders in docs and examples (for example `<access-token>`).
- Tune request interval via `SLEEP` in `src/utils/api.js` carefully to avoid `429` rate limits.
