# SelfDev — Clarity Lab v2

An original, standalone, offline communication-skills studio. No accounts, payments, network APIs, analytics or external lesson copying.

## Files

- [Clarity_Lab_SelfDev_Offline.html](Clarity_Lab_SelfDev_Offline.html): fully self-contained HTML/CSS/JS application. Open directly in a browser.
- [src/SelfDev_ClarityLab_v2_Android_Source.zip](src/SelfDev_ClarityLab_v2_Android_Source.zip): complete Android Java source, identical HTML asset, builder scripts, tests and docs.
- [REVIEW.md](REVIEW.md): verified weaknesses, improvements and remaining Android tests.
- [APK build workflow](.github/workflows/build-selfdev-apk.yml): manually dispatched GitHub Actions build.

## Build APK

This public repository uses a **manual-only** Android build workflow. Open Actions → Build SelfDev Clarity Lab APK (manual only) → Run workflow. If successful, download the `selfdev-clarity-lab-debug-apk` artifact. The workflow verifies the source ZIP SHA-256, compiles the APK, verifies the signature and checks the package ID `com.msa.claritylab`.

The code **has passed 22 source tests and desktop/mobile Chromium interaction and boundary checks**. **The APK has not yet been compiled or installed**. No workflow, deployment or billing change was triggered when source files were added.
