# Build the custom Pip Demo variants on macOS

This is build guidance for an experimental source alpha for local developers. No binary downloads are offered. Five named MIT notice-provenance gaps hold binary distribution; see [README](README.md). This repository has three package profiles on one engine: Neutral Plus, Pip Core, and Pip Plus. They use distinct app IDs, versions, and user-data directories. The baseline foundation and Replica build commands are not exposed by this product package manifest. Historical shared-engine evidence from 24 October: the clean remote Custom PR clone at `fc14d6a` passed `npm ci`, its default suite (364 files; 4,953 passed, 2 skipped; 4,955 total), `docs:check`, `i18n:check`, `npx tsc --noEmit`, and Vite builds for Neutral Plus, Pip Core, and Pip Plus using Node.js 22.22.1/npm 10.9.4. The skipped tests were the staged-FFmpeg waveform suite (native FFmpeg is not fetched during clean `npm ci`) and a Linux-only host-symbol test on macOS. The clean remote Replica PR clone at `3774c04` separately passed install, docs/localization checks, TypeScript, and the Replica baseline/core Vite build; a full Replica suite was not run. Those historical exports share normalized engine hash `4ad3c4e…d399013`, so the Custom suite covers shared-engine code but is not a full Replica-product suite.

Hosted source CI on 25 October passed at Custom `fd2a6fd` and Replica `b982753` on Linux with Node.js 22.22.1/npm 10.9.4: 363 test files, 4,948 passed, 7 skipped (4,955 total), taking 110.22s and 122.25s respectively; type, docs, and i18n checks passed ([Custom run](https://github.com/Ghostzy0/pip-demo/actions/runs/40172497618), [Replica run](https://github.com/Ghostzy0/pip-demo-replica/actions/runs/40172502073)). All seven skips required FFmpeg (four audio-peak checks and three audio-extraction checks); native FFmpeg was not fetched. The initial hosted renderer step built only the foundation profile. A corrected workflow that builds each declared product profile is present in source but has not yet run on hosted CI.

The 24 October full-suite result applies only to `fc14d6a`; the initial RPATH correction used focused checks before the subsequent hosted source suites. At source revision `4a58359`, focused `before-pack.test.mjs` checks passed (27 passed, 1 skipped). A real temporary macOS Mach-O fixture verified that the package gate rejects an absolute space-containing `LC_RPATH`, then accepts the normalized binary while preserving relative paths and symlinks, remaining idempotent, and passing strict ad-hoc signature verification.

The current Pip-profile source listener synchronizes `openscreen-theme` changes, including key clearing, to already-open Pip windows. First-load initialization remains provided by the existing page bootstrap. The listener is gated to the Pip profile. This source check does not establish packaged native multi-window behavior. At refs Custom `4ad1a8c` and Replica `ceeba575`, the current normalized shared-engine hash is `f01935c94e3598165ef60dc4c492b8969a3915b85c8ed4993ca9a1fa9bc033f2`. All four clean-export packages passed RPATH and deep strict signature checks: 40 whole-app Mach-O paths checked per app, zero absolute `LC_RPATH` entries, and ad-hoc runtime signatures. The four packages also passed 16 headless CLI media exports (control, zoom, voiceover MP4, and small GIF per profile); input fixtures, ASARs, and native inventories remained unchanged. The CLI path does not run live capture or load speech models. GUI workflow and Paper-theme acceptance for the Custom variants remain pending; the separate Replica GUI result does not qualify them. Five declared-MIT source-notice gaps block binary distribution. Windows and Linux package builds have no qualification.

Use Apple Silicon macOS, full Xcode with command-line tools selected, Rust, CMake, and pkg-config. Windows and Linux package builds have no qualification. Fresh setup requires network access for npm dependencies and pinned native assets.

```sh
npm ci
npm test -- --maxWorkers=2
npm run docs:check
npm run i18n:check
npm run build:native:demo
npm run build:neutral-plus
npm run build:pip
npm run build:pip-plus
```

`build:native:demo` prepares the ScreenCaptureKit helper, checksum-pinned LGPL FFmpeg, Apache-licensed camera assets, ONNX Runtime, Rust Metal compositor, and optional local caption helper. It is a substantial native build. Once dependencies and native assets are already cached, some build steps can run offline; a fresh checkout cannot. Speech model weights are not downloaded automatically. Do not distribute Homebrew/GPL FFmpeg in place of the packaged LGPL libraries.

Outputs are created under `release/neutral-plus`, `release/pip`, and `release/pip-plus`. Bundle IDs, data directories, versions, and selected variant are defined by the build profile. `npm run dev` starts the Pip Core app; `npm run dev:neutral-plus` and `npm run dev:pip-plus` select the other profiles. A development launch is not package acceptance.

Packages use ad-hoc signing and are not notarised. Building does not grant macOS permissions or prove capture/export behavior. Screen recording permission remains under macOS control; microphone, camera, system audio, and Accessibility are separate choices. Never bypass prompts or disable macOS security. Source recordings and projects stay in local paths. The app does not require accounts or cloud services. See [README](README.md) and [privacy and permissions](PRIVACY.md) before use.
