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

## Local use and privacy

The app is designed to work locally without an account or paid service. These builds disable cloud providers/chat, automatic model downloads, usage reporting, automatic updates, and automation listeners. Screen recording, microphone, camera, system audio, and Accessibility are separate OS-controlled choices. Importing a local video does not require screen-capture permission. Captioning needs separately supplied local model weights; the app does not fetch them automatically.

The first dependency install and native build require internet access to obtain pinned components. An offline build is possible only after dependencies and required native assets have been cached. App use does not depend on a hosted service. See [privacy and permissions](PRIVACY.md) and [local captions](LOCAL-CAPTIONS.md).

## Build

Historical shared-engine evidence: on 24 October, the clean remote Custom PR clone at `fc14d6a` passed install, the default suite (364 files; 4,953 passed, 2 skipped; 4,955 total), `docs:check`, `i18n:check`, TypeScript checking, and Vite builds for Neutral Plus, Pip Core, and Pip Plus. The suite ran on Node.js 22.22.1/npm 10.9.4. Two tests were skipped: the staged-FFmpeg real-file waveform suite because the clean export did not fetch native FFmpeg, and a Linux-only host-symbol test on macOS. System-FFmpeg integration tests did run. The clean remote Replica PR clone at `3774c04` separately passed install, docs/localization checks, TypeScript, and its Replica Core Vite build; a full Replica suite was not run. Those two historical exports share normalized engine hash `4ad3c4e…d399013`; the Custom suite covers shared-engine code but does not establish a full Replica-product suite.

The full-suite result above is historical and applies to Custom `fc14d6a`; it was not rerun for the RPATH fix. Replica `3774c04` passed the listed install, docs/localization, type, and Vite checks but had no full suite. At source revision `4a58359`, focused `before-pack.test.mjs` checks passed (27 passed, 1 skipped). A real temporary macOS Mach-O fixture verified rejection of an absolute space-containing `LC_RPATH` and acceptance after normalization, preserving relative paths and symlinks, remaining idempotent, and passing strict ad-hoc signature verification. The subsequent clean-export packages were built from Custom ref `4ad1a8c` and Replica ref `ceeba575`; their current normalized shared-engine hash is `f01935c94e3598165ef60dc4c492b8969a3915b85c8ed4993ca9a1fa9bc033f2`. The 16 headless CLI exports passed on those packages. No current-head full suite was run.

The shared app's source listener applies `openscreen-theme` changes, including a cleared key, to already-open Pip windows; the existing before-first-paint bootstrap handles a newly opened window. The listener is Pip-profile-only, leaving the neutral Replica profile unchanged. This source behavior has not been verified in the packaged native app. Package integrity and the four-profile headless media-export paths passed; GUI workflow and Paper-theme acceptance for the Custom variants remain pending. The Replica GUI steps recorded in its separate README do not qualify these variants. The CLI run did not invoke live capture, load speech models, or test ASR. Five declared-MIT notice gaps still block binary distribution.

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
