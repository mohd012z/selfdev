# SelfDev / Clarity Lab v2 — Verified Deep-Dive and Improvement Report

Date: 14 November 2026, MYT. Repository target: `mohd012z/selfdev`. All tests were executed locally; **no APK compilation success is claimed**.

## Original source audit

Previous Clarity Lab v1 was a multi-file React/Capacitor app (18 lessons, 12 exercises, 26 statements) with 21 passing local tests. The previously delivered `index.html` relied on separate scripts, CSS, vendor React files and a service worker. Thus it was **not a genuine single HTML file**. Browser file and local HTTP navigation are blocked by this environment's administrator policy; previous visual QA could not be completed that way.

## Implemented remedies

1. Built a **single 66 KB HTML** with embedded styles, JS, 6 domains, 18 lessons, 12 exercises and 26 original self-reflection prompts; no external assets or requests.
2. Redesigned desktop/mobile UI with dark/light themes, responsive fixed bottom navigation, progress overview, lesson search/filters, focus styles, reduced-motion support and large-text option.
3. Implemented working quiz, explicit skip (clears prior response), self-ratings, transparent rule-based practice reflection, timer, optional device text-to-speech and local journal.
4. Replaced implicit persistence assumptions with explicit `localStorage` failure notice, memory-mode fallback, 1 MB JSON backup/import, validation, whitelisted IDs, 100-note limit, and confirmation before overwrite/erase.
5. Fixed a real narrow-screen bug found in visual QA: a hidden notice remained visible because authored `display:flex` overrode the browser's `[hidden]` display rule. Added `.notice[hidden]{display:none}` and reran tests.
6. Built a minimal **no-network-permission native Android Java WebView wrapper** (package `com.msa.claritylab`) serving bundled HTML through an intercepted virtual HTTPS origin. Native SAF import/export dialogs avoid relying on Blob downloads in WebView.
7. Added manually dispatched public-repository GitHub Actions workflow with package/signature/ZIP/SHA-256 checks, plus source audit.

## Test evidence

| Test group | Result | Caveat |
|---|---|---|
| Python static/source audit | **22/22 PASS** | Does not compile Android Java |
| Chromium interactive smoke | **2/2 viewports PASS** | Uses `page.set_content` because browser navigation is administratively blocked; storage is a mock |
| Chromium edge cases | **9 checks PASS** | Tested 320/360/390/768/1024/1440 px, corrupt JSON, malicious HTML import, erase confirmation |
| JavaScript syntax | **PASS** using Node v22 `--check` | Does not test Android WebView JavaScript version |
| ZIP integrity | Performed on final archive | Archive not equal to signed APK |
| APK compilation | **NOT RUN** | Local Android SDK/Gradle unavailable; network DNS to Android SDK/Gradle repositories fails |
| Physical-device install, SAF backup/restore, offline boot | **UNVERIFIED** | Requires signed APK and Android device |

## Boundaries and risks

- This is an original free learning app, not RiseGuide or access to paid lessons. No objective charisma scoring is claimed.
- In a browser using a `file://` or other opaque origin, storage may be blocked. The warning tells users that session records might be lost; native Android uses a same-origin virtual HTTPS asset request to support DOM storage.
- Inline script/style CSP is required for a single-file app and is inherently weaker than script hashes/nonces in a multi-file distribution. User text and import values are HTML-escaped or whitelisted. Network connections are disabled in CSP and Android WebView.
- The Android Java backup bridge is restricted by WebView navigation/interception and no INTERNET permission. A physical-device permission/origin audit is still needed.
- Android source compiles in GitHub Actions **only when workflow is dispatched** and dependency repositories are reachable. The pipeline intentionally has no push/deploy trigger and blocks private repository runners to avoid unknown billed minutes.
- No automatic upload, billing, remote deployment or Telegram messages occurred during these local tests.

## Next release gate

In a public `mohd012z/selfdev` repository, import the complete source, then invoke Actions > SelfDev Clarity Lab APK (manual only) > Run workflow. Require green Python checks, `assembleDebug`, verified `apksigner`, package ID `com.msa.claritylab`, archive integrity, SHA-256, then install on an Android phone and validate actual backup import/export, offline relaunch and screen insets. Do not label a source ZIP as an installable APK.
## GitHub import verification — 14 November 2026

- Single HTML: Git blob `4327bc0a6fd1a1e58ff9ed868399ab2bf8b50e94`, exactly matching the local file and the bundled Android asset.
- Android source ZIP: Git blob `dfc0be855cb844a88f9192d85a12e59d429522ff`, SHA-256 `6ba59c605485fa6914d92480f2b7f5a41d4f150358ab9e1d8cf9558a1f487a85`.
- A one-byte trailing-newline mismatch during import was detected and corrected before the final file identity check.
- The GitHub manual-only APK workflow is committed, but has not been dispatched. GitHub Actions run count was 0 when inspected. No installable APK or physical-device verification is available.
