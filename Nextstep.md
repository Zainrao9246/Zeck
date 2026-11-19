# Zeck project handoff

Updated 2026-11-19.

## Current status

- The web document title is `Zeck` (`apps/web/app/layout.tsx`). Packaged app
  identity is still `Open Design`; the release-channel identity rules in
  `AGENTS.md` were intentionally not changed.
- The current `main` branch was at `8894e58` and matched `origin/main` before
  this work. The model-label changes described below are still uncommitted and
  have **not** been sent to GitHub.
- The model-label changes passed focused tests, `pnpm guard`, and
  `pnpm typecheck`. This is enough for code review and focused testing, but a
  Windows installer has not been produced, so do not call the app installer
  ready yet.
- Windows packaging was attempted with `pnpm tools-pack win build --to nsis
  --json` and stopped because the repository is missing the required
  `assets/community-pets` directory. `tools/pack/src/resources/index.ts`
  bundles it and `tools/pack/src/win/resources.ts` hashes it.
- Upstream `nexu-io/open-design` has the directory at
  <https://github.com/nexu-io/open-design/tree/main/assets/community-pets>.
  It contains `clippit`, `dario`, `dentist`, `nyako-shigure`, `slavik`, `tux`,
  `yelling-dario`, and `yorha-sit-2b`; each folder has `pet.json` and
  `spritesheet.webp`. Manifests identify the content as community/local assets;
  at least Clippy and YoRHa 2B are recognizable third-party characters. Do not
  copy these spritesheets without confirming their asset-specific reuse rights.

## Completed in the current work

- Added distinct `Free` and `Free tier (limited)` model cost labels to the
  chat-model picker, with strings in all 19 web locales.
- OpenRouter model discovery now reads its reported input/output prices and
  labels a model `Free` only for an explicit `:free` route or zero prices for
  both input and output. Unknown prices remain untagged.
- Focused tests passed:
  - `pnpm --filter @open-design/web exec vitest run -c vitest.config.ts tests/components/modelOptions.test.tsx`
  - `pnpm --filter @open-design/daemon exec vitest run -c vitest.config.ts tests/connection-test.test.ts -t "OpenRouter zero-priced models|OpenAI-compatible models from /models"`
- `pnpm guard` passed.
- `pnpm typecheck` passed.
- `git diff --check` passed.
- Workspace setup needed `pnpm install --frozen-lockfile --ignore-scripts` after
  the regular install hit an unrelated ONNX Runtime CUDA binary 404. The native
  `better-sqlite3` binding was built separately with
  `pnpm --filter @open-design/daemon rebuild better-sqlite3`.

## Uncommitted files

- `apps/daemon/src/integrations/provider-models.ts`
- `apps/daemon/tests/connection-test.test.ts`
- `apps/web/src/components/modelCapabilityTags.ts`
- `apps/web/src/i18n/types.ts`
- `apps/web/src/i18n/locales/*.ts` (all 19 locales)
- `apps/web/src/types.ts`
- `apps/web/tests/components/modelOptions.test.tsx`
- `packages/contracts/src/api/registry.ts`

## Still not implemented

- Cloudflare Workers AI chat/image integration (Cloudflare credentials have not
  been requested or pasted into chat; do not ask for secrets in chat).
- Cost/free labels for image-generation models.
- Reliable reasoning-capability labels for provider models.
- Any changes to AI-credit usage/routing.
- Packaged installer/app identity change from `Open Design` to `Zeck`.
- A Windows `.exe` build or install smoke test.

## Next steps

1. Resolve the missing `assets/community-pets` packaging input. Obtain assets
   whose reuse rights are clear, or get an explicit decision to make the bundle
   optional (bundled pets would not ship, but remain downloadable in-app).
2. Re-run `pnpm tools-pack win build --to nsis --json`; verify the resulting
   installer's exact output path and app identity before sharing it.
3. If the Windows installer is available, install and smoke-test it on Windows
   (this current Linux environment has no Windows desktop runtime).
4. Review the uncommitted diff, then send it to GitHub on an appropriate
   feature branch/PR; do not push directly to `main`.
5. Continue the separate Cloudflare, image-cost, reasoning-label, and credit
   work as explicitly scoped phases.

## Earlier AMR cleanup context

- The repository still has substantial AMR runtime and web integration.
- MiniMax provider/media configuration is separate from AMR and should remain
  unless its removal is explicitly requested.
- Earlier `ChatPane.tsx` / `SettingsDialog.tsx` AMR recovery edits were reported
  as limited and unverified at that time. The existing main history has moved
  since then; inspect current Git history/diffs before acting on that older
  claim.
- Do not remove every AMR-named path mechanically: some references may support
  collaboration or compatibility behavior.
