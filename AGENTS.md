# Agent Instructions — vros-api (Horizon OS SDK Samples)

A collection of Android samples that demonstrate the Horizon OS SDK (JSDK, NSDK, and Support Library) on Meta Quest devices. Each sample is a self-contained Gradle project under one of the top-level category directories.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup, repository layout, and requirements
- The per-sample `README.md` inside each sample directory — sample-specific requirements (feature flags, permissions, device builds)
- `<sample>/app/build.gradle.kts` + `<sample>/gradle/libs.versions.toml` — Android Gradle / SDK versions for that sample
- `<sample>/app/src/main/AndroidManifest.xml` — package id, permissions, target API
- `LICENSE` — license terms

## Quest / Horizon-specific notes

- This repo is a **public mirror of an internal Meta source-of-truth repository** (per the README). Contributions only appear after the internal review lands — don't restructure aggressively or expect rapid back-and-forth on PRs.
- There is no top-level Gradle project. Each sample under `JavaDevelopmentKitSamples/`, `NativeDevelopmentKitSamples/`, `SupportLibrarySamples/`, and `MixedSdkSamples/` is opened independently in Android Studio.
- NSDK samples consume `horizon-os-nsdk` as a Prefab AAR (headers + `.so`s packaged via Android NDK Prefab). Do not move headers/libs out of the Prefab layout.
- Horizon OS API levels are deliberate per-sample pins. Bumping `compileSdk` / `minSdk` / `targetSdk` is a real SDK-availability decision, not a casual cleanup.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Android answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Android-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
