# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a VS Code theme extension called "Barbenheimer" that provides three color theme variants inspired by the cultural phenomenon combining Barbie and Oppenheimer aesthetics. The extension is published to the VS Code marketplace and contains no executable code - only JSON configuration files.

## Architecture

The project follows the standard VS Code theme extension structure:

- `package.json` - Extension manifest defining the three theme contributions
- `themes/` - Contains three JSON theme definition files (~300 lines each):
  - `barbenheimer-dreamhouse-theme.json` - Light theme with pink/warm tones
  - `barbenheimer-bunker-theme.json` - Dark theme with muted colors
  - `barbenheimer-nuclear-sunrise-theme.json` - High-contrast dark theme
- `images/` - Theme preview images and extension icon
- `.vscode/launch.json` - Extension development configuration

Each theme JSON file defines:
- `colors` object - VS Code UI element colors (activity bar, editor, panels, etc.)
- `tokenColors` array - Syntax highlighting rules with TextMate scope selectors

## Development Commands

### Testing the Extension
```bash
# Press F5 in VS Code to launch Extension Development Host
# Or use the launch configuration: "Extension"
```

### Publishing (if needed)
This extension uses the standard VS Code extension publishing workflow via `vsce` (Visual Studio Code Extension manager).

## Theme Development Notes

- Each theme file is approximately 300 lines of JSON
- Color definitions use hex codes with optional alpha channels
- UI colors are defined in the `colors` object using VS Code's theming API
- Syntax highlighting uses TextMate scopes in the `tokenColors` array
- The three themes maintain consistent structure but different color palettes
- Theme previews are included as WebP images in the `images/` directory

## Key Color Palettes

- **Dreamhouse (Light)**: Pink (#F672AC), off-white (#FFF8F0), browns
- **Bunker (Dark)**: Deep pink (#E44288), dark grays (#14140B), muted tones
- **Nuclear Sunrise (High-contrast)**: Hot pink (#FF69B4), white (#FFFFFF), dark gray (#0F0F0A)