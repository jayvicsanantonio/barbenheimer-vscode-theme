# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.
``

Project type and scope
- This is a declarative Visual Studio Code theme extension. There is no build pipeline, source code, or automated tests; the extension contributes three color themes via JSON files.
- Key sources consulted: package.json (extension manifest), CLAUDE.md (project guidance), .vscode/launch.json (dev host), themes/*.json (actual theme definitions), README.md (user-facing notes).

Common commands
- Launch Extension Development Host (requires VS Code CLI available as `code`)
```bash path=null start=null
# Open a VS Code instance with this extension loaded in dev mode
code --new-window --extensionDevelopmentPath="$PWD"
```
- Validate theme JSON files (quick syntax check)
```bash path=null start=null
# Fails if any JSON is invalid; produces no output on success
python3 -m json.tool themes/*.json > /dev/null
```
- Package the extension (produces a VSIX)
```bash path=null start=null
# Uses vsce without a global install
npx @vscode/vsce package
# The output will look like: barbenheimer-1.0.0.vsix
```
- Install/uninstall a packaged VSIX locally
```bash path=null start=null
# Install the generated package into your VS Code
code --install-extension ./barbenheimer-*.vsix

# Uninstall by extension identifier (publisher.name)
code --uninstall-extension jayvicsanantonio.barbenheimer
```
- Inspect what would be published (file list in package)
```bash path=null start=null
npx @vscode/vsce ls
```
- Version bump (updates package.json version)
```bash path=null start=null
# Choose one of: patch | minor | major
npm version patch
```
- Publish to Marketplace (optional; requires vsce to be authenticated)
```bash path=null start=null
# One of: patch | minor | major | specific version
npx @vscode/vsce publish patch
```
Notes on build/lint/tests
- Build: Not applicable (pure JSON contribution).
- Lint: No repo-configured linter. Use the JSON validation command above and rely on VS Code’s JSON validation.
- Tests: No automated tests are configured in this repository.

High-level architecture and structure
- Extension manifest (package.json)
  - Defines metadata (name: "barbenheimer", publisher: "jayvicsanantonio", engines.vscode: ^1.80.0).
  - Contributes exactly three themes:
    - Barbenheimer Dreamhouse (uiTheme: vs, path: themes/barbenheimer-dreamhouse-theme.json)
    - Barbenheimer Bunker (uiTheme: vs-dark, path: themes/barbenheimer-bunker-theme.json)
    - Barbenheimer Nuclear Sunrise (uiTheme: vs-dark, path: themes/barbenheimer-nuclear-sunrise-theme.json)
  - Icon path points to images/barbenheimer-icon.png (used for marketplace/extension gallery).
- Theme definitions (themes/*.json)
  - Each file contains two main sections that matter:
    - colors: UI color tokens for VS Code (activity bar, editor, panels, sidebar, terminal, git decorations, etc.).
    - tokenColors: TextMate scope-based syntax highlighting rules.
  - The three variants share structure but differ in palettes and contrast:
    - Dreamhouse: Light theme with pink/warm palette.
    - Bunker: Dark theme with muted tones and pink accents.
    - Nuclear Sunrise: High-contrast dark theme with hot-pink accents.
- Development configuration (.vscode/launch.json)
  - Provides a single "Extension" launch config; pressing F5 in VS Code uses this to start an Extension Development Host with the repo loaded.
- Additional assets
  - README.md documents theme variants and basic installation for users.
  - LICENSE.md defines licensing.
  - Images (icon and previews) referenced by package.json and README.md.

Workflow tips specific to this repo
- Iterating on colors
  - Edit the relevant theme JSON in themes/ and reload the Extension Development Host window to see changes.
  - Keep token naming consistent across variants where possible; most differences should be palette values, not structure.
- Adding a new theme variant
  - Create a new JSON file in themes/ with the same structure (colors + tokenColors).
  - Add a new entry to contributes.themes in package.json with label, uiTheme (vs or vs-dark), and path to your JSON.
  - Update README.md and add preview imagery if desired; ensure package.json icon/preview references remain valid.
- Compatibility
  - engines.vscode is set to ^1.80.0; ensure you test on a matching or newer VS Code version.

Important guidance from CLAUDE.md (summarized)
- This extension is purely declarative (JSON only); no executable code.
- Themes are defined by colors (workbench/UI) and tokenColors (syntax scopes) and are ~hundreds of lines each.
- Use the standard VS Code extension packaging/publishing flow via vsce when needed.
