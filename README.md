# Pip Demo

Pip Demo is an experimental, local macOS screen recorder and demo-video editor. This clean-export product line contains **Pip Core**, **Neutral Plus**, and **Pip Plus**, all built from one shared engine. The neutral Plus edition uses the neutral Replica-style presentation; the Pip editions use the original Paper/Pebble theme. Core releases are version `0.1.0-alpha.1`; Plus releases are version `0.2.0-alpha.1`.

The project derives substantially from the MIT-licensed OpenScreen Electron/React, Swift capture, and Rust compositor code. It is independent of Screen Studio. Screen Studio's public guide informed workflow research; this product is not a verified equivalent and makes no compatibility claim. The separate `pip-demo-replica` product is intended for a partial functional/layout recreation based on undated guide material.

## Availability and qualification

Experimental source alpha for local developers. No binary downloads are offered. Binary distribution is held by five MIT notice-provenance gaps for `dlv` 1.1.3, `lazy-val` 1.0.5, `react-remove-scroll-bar` 2.3.8, `block` 0.1.6, and `malloc_buf` 0.0.6. The four clean-export macOS packages (Neutral Plus, Pip Core, Pip Plus, and Neutral Replica) passed package-integrity checks after the RPATH fix: 40 whole-app Mach-O paths were checked per package, with zero absolute `LC_RPATH` entries and successful deep strict ad-hoc signature verification. A headless CLI regression produced control, zoom, voiceover, and GIF exports from each package (16 exports total). These checks do not establish GUI workflow acceptance, live capture, model/ASR execution, or reference fidelity. Capture permissions, Screen Studio fidelity, notarization, accessibility technology testing, and performance measurements remain unverified.

Variant identities and data directories are separate:

| Variant | Version | Application ID | Data directory | Build command |
| --- | --- | --- | --- | --- |
| Neutral Plus | `0.2.0-alpha.1` | `uk.pip.demo.plus` | `Demo-Plus` | `npm run build:neutral-plus` |
| Pip Core | `0.1.0-alpha.1` | `uk.pip.demo` | `Pip-Demo` | `npm run build:pip` |
| Pip Plus | `0.2.0-alpha.1` | `uk.pip.demo.pip.plus` | `Pip-Demo-Plus` | `npm run build:pip-plus` |

No project/settings migration between those data directories is qualified. Keep independent backups of project files and their media.


### Cmd-W native close evidence — 25 October 2026

At this native verification checkpoint, the Cmd-W patch had no hosted CI result. The linked CI runs cover earlier source; use the pull request checks for later results on an exact patch head.

The current source adds the standard macOS File > Close / Cmd-W route. The published source-alpha tags remain unchanged; `EXPORT-MANIFEST.json` in the clean export identifies the source used for this package. Three focused test files passed (23 tests), and TypeScript passed on Node.js 22.22.1. A fresh Pip Plus package was built with Node.js 22.22.1/npm 10.9.4. In a 178.5-second native slice, Cmd-W quit the empty editor with app-process absence checked before the next accessibility query; after relaunching a synthetic project, a renamed title and 0–345 ms zoom range persisted in project data and Cmd-W closed normally. A separate 105.18-second scenario on the same package exercised an unsaved text annotation: while its textarea had focus and showed Unsaved, Cmd-W opened the Save Changes modal; Cancel retained the editor and text. After replacing the text with a second label, Cmd-W followed by Save & Continue closed the app, with processes absent before the next accessibility query. The saved project data contained the exact second label, and after relaunch/reopen it was visible in the rendered project. Cmd-Q also exited normally. This verifies Cancel and Save/reopen for this synthetic text-annotation scenario only; Discard and other unsaved-state flows were not exercised. The Pip Plus test bundle also contained a private camera-asset cache-provenance receipt absent from the source export. It remains a local test input, not a redistribution candidate; a future binary must omit that receipt, be resealed, and pass package-integrity and signature checks again. Advisory: when the textarea lost focus as the modal opened, the background status changed from Unsaved to Saved while the modal remained visible, and generic modal copy said the project was not yet saved despite existing saved-project data. This did not block the tested flow. The native checkpoint did not rerun the full suite; hosted results for later exact refs are tracked in [GitHub Actions](https://github.com/Ghostzy0/pip-demo/actions). No other-profile package, capture, reference-fidelity, or accessibility acceptance is claimed. The package is ad-hoc signed and not notarised. The public tags and releases were not changed. Five MIT notice-provenance holds still block binary distribution.

## Local use and privacy

The app is designed to work locally without an account or paid service. These builds disable cloud providers/chat, automatic model downloads, usage reporting, automatic updates, and automation listeners. Screen recording, microphone, camera, system audio, and Accessibility are separate OS-controlled choices. Importing a local video does not require screen-capture permission. Captioning needs separately supplied local model weights; the app does not fetch them automatically.

The first dependency install and native build require internet access to obtain pinned components. An offline build is possible only after dependencies and required native assets have been cached. App use does not depend on a hosted service. See [privacy and permissions](PRIVACY.md) and [local captions](LOCAL-CAPTIONS.md).

## Build

Historical shared-engine evidence: on 24 October, a clean Custom PR export passed install, the default suite (364 files; 4,953 passed, 2 skipped; 4,955 total), `docs:check`, `i18n:check`, TypeScript checking, and Vite builds for Neutral Plus, Pip Core, and Pip Plus. The suite ran on Node.js 22.22.1/npm 10.9.4. Two tests were skipped: the staged-FFmpeg real-file waveform suite because the clean export did not fetch native FFmpeg, and a Linux-only host-symbol test on macOS. System-FFmpeg integration tests did run. A separate clean Replica PR export passed install, docs/localization checks, TypeScript, and its Replica Core Vite build; a full Replica suite was not run. The Custom suite covers shared-engine code but does not establish a full Replica-product suite.

Historical hosted source CI passed at Custom `369753868c4b443ab42b992f7a0aabb879e5fa0e` ([run 40173721426](https://github.com/Ghostzy0/pip-demo/actions/runs/40173721426)) and Replica `d44bc0f3d8c289e3afe2220fcb42fc733d6a2530` ([run 40173723275](https://github.com/Ghostzy0/pip-demo-replica/actions/runs/40173723275)) on Linux with Node.js 22.22.1/npm 10.9.4. Each run passed 363 test files and skipped 1 file; 4,948 tests passed and 7 FFmpeg-dependent tests skipped (4 audio-peak, 3 audio-extraction) out of 4,955, in 184.80s Custom and 144.33s Replica. Type, docs, and i18n checks passed. The corrected workflow built Custom Neutral Plus (`uk.pip.demo.plus`), Pip Core (`uk.pip.demo`), Pip Plus (`uk.pip.demo.pip.plus`), and Replica Core (`uk.pip.demo.replica`); Vite compiled renderer, main, and preload bundles. CI did not launch an app or build a native package. The immutable public source-alpha tag manifests share engine SHA-256 `3447fde8c6d0dbf40d26ab341f5a181abd835309f5297714641c2d1fb6009b43`; they predate the unreleased menu change above. For those immutable tags, compared with the f019 package-tested exports, only `.github/workflows/checks.yml`, `README.md`, and `BUILDING.md` differ; the other 1,433 of 1,436 payload files, including all runtime files, are byte-identical. The earlier workflow run built only the foundation profile; these runs verify the corrected declared-profile workflow.

The 24 October full-suite result applies to the historical Custom export only; the separate Replica export passed the listed install, docs/localization, type, and Vite checks but had no full suite. The RPATH correction had focused `before-pack.test.mjs` checks (27 passed, 1 skipped) and a real temporary macOS Mach-O fixture: the package gate rejected an absolute space-containing `LC_RPATH`, then accepted the normalized binary while preserving relative paths and symlinks, remaining idempotent, and passing strict ad-hoc signature verification. The subsequent pre-menu-fix clean-export packages passed package-integrity checks and 16 headless CLI media exports. The packaged-app media checks are separate from hosted source suites.

Earlier native observations on pre-Cmd-W packages include synthetic Notes persistence and a light/dark route on Pip Plus, compact HUD keyboard focus transfer on Neutral Plus, and the permission-status/Get Started route without Allow plus a full HUD without Plus collapse controls on Pip Core. These are narrow observations, not full Paper, capture, accessibility, or overall GUI acceptance. They predate the current Cmd-W fix. See [build details](BUILDING.md). The CLI run did not invoke live capture, load speech models, or test ASR. Five declared-MIT notice gaps still block binary distribution.

The source checks and package/CLI checks above are separate evidence: they do not establish GUI workflow acceptance. Capture permissions, Screen Studio fidelity, model/ASR execution, notarization, accessibility technology testing, and performance measurements remain unverified. The source alpha has incomplete native acceptance; the five notice-provenance gaps listed above hold binary distribution. Other operating systems have no qualified package. Full Xcode, Rust, CMake, pkg-config, and network access for a fresh dependency/native-asset setup are required. Example commands:

```sh
npm ci
npm test -- --maxWorkers=2
npm run build:native:demo
npm run build:neutral-plus
npm run build:pip
npm run build:pip-plus
```

Packages are ad-hoc signed and not notarised. Never disable macOS security globally. Build commands do not grant OS permissions or establish a working recording/export flow. See [build details](BUILDING.md) and the [AI-assisted setup prompt](docs/AI-SETUP.md).

## Questions

**Can I download a public build?** No binary downloads are offered. Do not treat an internal package as a published download.

**Does the app upload recordings or require an AI account?** The described editions disable cloud providers and usage reporting. Projects and media are saved locally. Dependency downloads during setup are separate from app use.

**Do I need Screen Recording permission?** Only to capture a screen or window. Microphone, camera, system audio, and Accessibility permissions are separate. Local video import needs no screen-capture grant.

**Is this equivalent to Screen Studio?** No. This custom product uses OpenScreen-derived code and original theme work. Research and a similar interface do not establish parity with Screen Studio.

**Are files shared across editions?** No. Each variant has its own application ID and data directory. Migration has not been qualified.

## References and attribution

- [OpenScreen source pin](https://github.com/getopenscreen/openscreen/tree/d8bf2d8138cc2ce2c6542549853260f716cb8fb6), MIT copyright Siddharth Vaddem and contributors. Other bundled components retain their own licenses; see [third-party notices](THIRD-PARTY-NOTICES.md) and the generated license inventory.
- [Screen Studio public guide](https://screen.studio/guide), a workflow research reference. No reference media or vendor assets are included.
- [Notices](THIRD-PARTY-NOTICES.md), [license](LICENSE), [asset provenance](ASSETS.md), [changes](CHANGELOG.md), [contributing](CONTRIBUTING.md), and [security](SECURITY.md).

No personal recordings, Screen Studio reference recordings, or vendor guide images are included. Bundled OpenScreen-derived and other third-party components retain their licenses and notices. No affiliation or compatibility guarantee is claimed.
