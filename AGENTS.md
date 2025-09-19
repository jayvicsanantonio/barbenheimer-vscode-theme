# Repository Guidelines

## Project Structure & Module Organization
- `package.json` owns the extension manifest; update `version`, `contributes.themes`, and marketplace metadata together.
- `themes/` stores the three theme variants; keep filenames in the pattern `barbenheimer-<descriptor>-theme.json` and mirror labels in `package.json`.
- `images/` holds marketing assets referenced from the README and the Marketplace listing; export optimized `.webp` alongside any icon updates.
- `README.md` and `vsc-extension-quickstart.md` document usage; refresh them whenever color scopes or onboarding steps change.

## Build, Test, and Development Commands
- `npm install` prepares local tooling (e.g., `vsce`, linters) before packaging or publishing.
- `code --extensionDevelopmentPath=$(pwd)` launches VS Code with the extension loaded; equivalent to pressing `F5` inside VS Code for live preview.
- `npx vsce package` builds `barbenheimer-<version>.vsix` for local install and regression testing.
- `npx vsce publish` (with a Personal Access Token) pushes a Marketplace release; run only after tagging and updating screenshots.

## Coding Style & Naming Conventions
- Use 2-space indentation in JSON, uppercase hex color codes (including alpha suffixes), and trailing commas for stable diffs.
- Group keys by VS Code surface (`activityBar`, `editor`, `statusBar`, etc.) and keep related scopes clustered to aid reviews.
- New variants should reuse shared palette constants where possible and follow the existing `Barbenheimer <Title>` naming in `label` and `name` fields.
- Reference assets as `images/<variant>.webp` or `.png` to stay consistent with current marketing material.

## Testing Guidelines
- After edits, relaunch the extension host and cycle through all three variants to confirm contrast, syntax legibility, and terminal/readline colors.
- Use the Command Palette action `Developer: Inspect Editor Tokens and Scopes` to verify scope assignments for modified tokens.
- Validate JSON with `npx jsonlint themes/<file>.json` (or the VS Code built-in formatter) before committing.
- Capture before/after screenshots when altering prominent UI areas to simplify reviewer comparison.

## Commit & Pull Request Guidelines
- Write imperative, descriptive commit subjects under ~72 characters, matching the existing history (`Remove unused CHANGELOG.md`).
- Summaries should call out affected surfaces (e.g., editor, activity bar, syntax) and note any asset or documentation updates.
- Link issues with `Fixes #<id>` when applicable and attach preview screenshots or scope notes in the PR description.
- Ensure PRs list verification steps (`code --extensionDevelopmentPath`, token inspection, jsonlint) and request review before publishing.
