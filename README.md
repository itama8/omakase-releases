# Omakase Test Releases

Official preview binaries for **Omakase** — a local-first, cursor-first programmable Markdown scratchpad. Your current note is the primary surface: write normally, navigate local notes, use search and reference tools, and optionally bring an LLM into the writing flow through **Sushi**.

> **Super-early test build:** this is not a polished or stable release. Expect rough edges, incomplete workflows, platform quirks, and breaking changes between test versions. Back up important notes and report what you find.

## Download

Open [Releases](https://github.com/itama8/omakase-releases/releases), choose the newest prerelease, and download the artifact for your machine:

| Platform | Artifact | Notes |
| --- | --- | --- |
| Windows x64 | `Omakase-…-windows-x64.exe` | Portable executable; no installer. |
| macOS Apple Silicon | `Omakase-…-macos-arm64.dmg` or `.zip` | For M-series Macs only; no installer or signing. |
| Linux x64 | `Omakase-….AppImage` | Portable AppImage; no installer. |

These are **no-install binaries**, packaged ad hoc for testing rather than through a finished distribution channel. Startup—especially the first launch—can be slower than a normal installed app. Do not mistake a short delay for a hung app.

Download from this repository's **Releases** page. That is all most testers need to do.

You will also see files named `SHA256SUMS-…` and `BUILD-INFO-…`. They are optional technical records for people who want to check a download; you can safely ignore them while getting started.

## Unsigned-build warnings: how to open Omakase

These early test apps are **not signed yet**, so Windows and macOS will show a warning. That is expected. Only use the steps below for a file you downloaded from this repository's Releases page.

### Windows

1. Download the Windows `.exe`.
2. Open it. When Windows says **Windows protected your PC**, click **More info**.
3. Click **Run anyway**.
4. If Windows still blocks it: right-click the `.exe` → **Properties** → check **Unblock** (if shown) → **Apply** → open it again.

### macOS (Apple Silicon / M-series Macs)

1. Download the DMG or ZIP and move `Omakase.app` to **Applications**.
2. Control-click `Omakase.app` → **Open** → **Open** again.

If macOS says the app is “damaged” or cannot be opened, open **Terminal**, paste this, and press Return:

```bash
xattr -dr com.apple.quarantine "/Applications/Omakase.app"
codesign --force --deep --sign - "/Applications/Omakase.app"
open "/Applications/Omakase.app"
```

This tells your Mac to trust and locally sign that copy of Omakase. If you would rather not use Terminal, wait for a future signed build.

### Linux

1. Download the `.AppImage`.
2. Open a terminal in the download folder and run:

   ```bash
   chmod +x Omakase-*.AppImage
   ./Omakase-*.AppImage
   ```

The Linux build is x64 only. If your Linux distribution blocks AppImages, look up its AppImage/FUSE setup instructions.

## What it is / quick start

Omakase keeps plain Markdown notes local to a vault folder. It is useful without AI: create or open a note, type, rely on autosave, and use the command palette to discover actions.

1. Launch Omakase and choose or create a local notes folder when prompted.
2. Create/open a note and start typing. Markdown is the durable format.
3. Press **Ctrl+Shift+P** (on macOS, use **Cmd+Shift+P**) for the command palette.
4. Useful first shortcuts: **Ctrl/Cmd+F** searches the current note; **Ctrl/Cmd+Shift+F** searches the vault.
5. Keep independent backups of notes you care about. This build is for testing, not the only copy of important work.

Sushi is Omakase’s in-editor LLM workflow: it can work with your writing context and show responses as editor artifacts rather than functioning as a separate chat app. AI remains optional.

## Getting started with LLMs and provider registration

The simplest free starting point is usually a **Google AI Studio API key**. Create one at [Google AI Studio](https://aistudio.google.com/apikey), subject to Google’s current free-tier limits and terms; never share the key in a note, issue, screenshot, or chat.

1. In Omakase, open the **Provider** card in the HUD/sidebar (it may say **Configure providers**).
2. In **API Keys**, find **Google**, choose **Set key**, paste the AI Studio key, and select **Save**.
3. Open the **Model** card, choose an available Google model, then invoke Sushi from the command palette or its editor action.
4. If a model is unavailable, return to Provider settings to confirm the key saved, then choose another listed model.

Other supported providers can be configured in the same Provider dialog with their own API key or login flow. Provider requests leave your computer for the provider you select, so review that provider’s terms, pricing, and privacy policy. Use a key with an appropriate spending limit; Omakase does not provide model service or pay provider charges for you.

## Current state and near-term improvements

Omakase is actively being shaped around a dependable local editor core: typing, local Markdown notes, autosave, per-note Undo history, commands, note/vault search, and optional Sushi assistance. The immediate focus is on making test distribution less friction-filled: faster and more predictable startup, stronger packaged-app smoke testing, Windows/macOS signing and notarization, and resolving platform-specific rough edges before broader release.

Known rough edges include unsigned-platform warnings, slow first start, incomplete polish, evolving UI/shortcuts, uneven platform testing, and features that may change or disappear. The PDF viewer’s packaged Windows path and broader release ergonomics are still receiving real-device testing. Please treat this as an invitation to test and give focused feedback, not a promise of production readiness.

## Feedback and release policy

- Report reproducible issues through the project’s GitHub channels, including platform, artifact version, and steps to reproduce. **Never attach API keys or private notes.**
- This repository is a binary distribution surface only; it does not contain the Omakase source tree.
- Releases are immutable. A fixed binary is published under a new version rather than silently replacing an existing asset.
