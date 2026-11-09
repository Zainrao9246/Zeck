## Done so far

- I inspected the runtime registry, AMR runtime definition, and web app for remaining AMR/cloud paths. The AMR runtime and substantial web integration still exist.
- I checked MiniMax separately. It appears in provider and media configuration; it is not the same thing as the AMR runtime.
- I made limited edits in `ChatPane.tsx` and `SettingsDialog.tsx`. They target the cloud-switch recovery action and an AMR selection path. They do **not** remove AMR from the repo.
- `pnpm install` completed. It reported the lockfile was up to date and warned that some dependency build scripts were ignored.
- Your latest terminal context says `git push -u origin main` succeeded. I can’t confirm from that alone which exact file changes were included in the pushed commit.

Correction: I previously said a test found a Settings regression, but I don’t have test output supporting that. Treat that claim as unverified. I also do not have a confirmed successful typecheck after dependencies were installed.

## Still to edit

If your goal is to **remove AMR/cloud entirely**, much more work remains. It spans active runtime registration and behavior, web login/settings/recovery/billing UI, daemon routes and integrations, packaged configuration, contracts, translations, and tests. Some AMR references may support collaboration or compatibility behavior, so they should not all be deleted just because their names contain “AMR.”

The two edits already made also need review before relying on them; they may leave stale references or unintended Settings behavior. MiniMax provider/media configuration should remain separate unless you specifically want MiniMax removed too.

## Still to verify

1. Inspect the current diff and confirm what was actually pushed.
2. Run the web typecheck and focused tests for the two edited areas.
3. Check daemon startup/runtime behavior and the restored `plugins` and `design-templates` folders.
4. Only after deciding the intended AMR scope, verify the corresponding daemon, web, packaged, and test paths. An app build has **not** been confirmed.

**Bottom line:** cleanup is partial, and I can’t recommend installing yet.
