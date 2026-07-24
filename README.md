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

Each release includes SHA-256 checksum files and build metadata identifying the exact source commit. Verify a checksum before bypassing an operating-system warning:

- **Windows (PowerShell):** `Get-FileHash .\Omakase-…-windows-x64.exe -Algorithm SHA256`
- **macOS/Linux:** `shasum -a 256 <downloaded-file>`

Compare the output with the matching `SHA256SUMS-*.txt` file in that release.

## Unsigned-build warnings and how to run

These early binaries are **unsigned**. Windows SmartScreen and macOS Gatekeeper warnings are expected. Only bypass a warning after downloading from this repository and verifying its checksum.

### Windows

1. Download the portable `.exe` and verify its SHA-256 checksum.
2. In the **Windows protected your PC** SmartScreen dialog, select **More info**.
3. Confirm the file name is the Omakase release you verified, then select **Run anyway**.
4. If Windows flags it again from Explorer, right-click the file, choose **Properties**, select **Unblock** if present, then choose **Apply** and open it.

### macOS (Apple Silicon)

1. Download the DMG or ZIP, verify its SHA-256 checksum, and copy `Omakase.app` to **Applications** (or another folder you control).
2. Control-click `Omakase.app`, choose **Open**, then choose **Open** again in the warning dialog. This is the normal one-time Gatekeeper override for an unsigned app.
3. If macOS instead says the app is “damaged” or cannot be opened, open Terminal and run the following **only after checksum verification** (adjust the path if needed):

   ```bash
   xattr -dr com.apple.quarantine "/Applications/Omakase.app"
   codesign --force --deep --sign - "/Applications/Omakase.app"
   open "/Applications/Omakase.app"
   ```

The second command locally ad-hoc-signs the copy on your Mac. It does not make the download developer-signed or notarized. Proper Developer ID signing and notarization are planned improvements.

### Linux

1. Verify the AppImage checksum.
2. Mark it executable and run it:

   ```bash
   chmod +x Omakase-*.AppImage
   ./Omakase-*.AppImage
   ```

If your distribution blocks AppImages, consult its AppImage/FUSE guidance. The test build is x64 only.

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
