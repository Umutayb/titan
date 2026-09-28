# Titan

**Unofficial fork** of [Pastiera](https://github.com/palsoftware/pastiera) by PalSoftware, a keyboard for Android phones with physical keyboards (GPLv3). This is not an official Pastiera release. For the full feature list, read the [upstream README](../README.md).

## What this fork changes

- **Hide status bar** (Settings → Customization → Status Bar): while you type on the hardware keyboard, nothing is drawn above the keys. SYM, emoji and clipboard pages still open when you call them up.
- Its own app ID, `io.github.umutayb.titan`, so it installs alongside Pastiera. Update checks use this repo.

To move your settings over, go to Pastiera → Advanced → **Backup now**, then Titan → Advanced → **Restore from file**.

## Staying in sync with upstream

- `main` mirrors `palsoftware/pastiera` and never receives fork commits.
- `titan` is `main` plus the fork changes. The **Sync upstream** workflow runs weekly (or trigger it by hand). It fast-forwards `main` and merges it into `titan`. If the merge conflicts, it opens an issue instead.
- To keep conflicts rare, fork changes stay out of upstream files where possible:
  - Branding: the appended overlay block at the end of `app/build.gradle.kts`, plus `app/src/titan/res/`
  - Fork strings: `app/src/main/res/values/titan_strings.xml`
  - This README: `.github/README.md`
  - Feature code: small, marked hunks in `StatusBarController`, `KeyboardVisibilityController`, `CandidatesBarController`, `PhysicalKeyboardInputMethodService`, `SettingsManager`, `StatusBarButtonsScreen`, `CustomizationSettingEntries` and `BackupContract`

To sync by hand:

```sh
git remote add upstream https://github.com/palsoftware/pastiera.git
git fetch upstream && git checkout titan && git merge upstream/main
```

## Building

```sh
./gradlew :app:assembleStableDebug :app:testStableDebugUnitTest
```

This needs JDK 21 and Android SDK 36.
