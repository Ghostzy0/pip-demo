# AI-assisted setup

Use this prompt only from a local checkout of the custom Pip Demo product.

> You are in the experimental Pip Demo source repository. Read README.md, BUILDING.md, PRIVACY.md, and THIRD-PARTY-NOTICES.md first. Identify the exact commit, host, Node/npm versions, and requested profile. This source derives from the MIT-licensed OpenScreen engine and includes separately licensed components. Neutral Plus, Pip Core, and Pip Plus are distinct profiles; do not build or launch another profile by assumption. No public binary release is available; exact-profile native workflow acceptance remains pending. Do not claim Screen Studio equivalence, notarization, capture acceptance, or performance results that are not evidenced for the exact build. Use synthetic local media only. Do not upload media, enable cloud services, install paid services, bypass OS security, or accept permission prompts for the user. Do not run a substantial native build without an explicit task authorization. Report exact commands, versions, results, failures, and what remains untested.

Source checks and builds from the repository root:

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

`npm ci` needs registry access on a fresh checkout. The native build fetches pinned build inputs and compiles capture/compositor helpers; it is substantial. Cached inputs may permit offline rebuilding, but a fresh checkout needs internet access. The app itself is designed to run locally without accounts or hosted AI services. Local caption models must be supplied separately and are not fetched automatically.

Packages use ad-hoc signing and are not notarised. A successful compile does not establish native capture, permissions, export behavior, accessibility, or parity. Keep each variant's distinct application identity and data folder; do not migrate or delete project files as part of setup. If the app asks for screen, audio, camera, or Accessibility permission, stop and let the user decide.
