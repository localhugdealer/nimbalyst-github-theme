# GitHub Theme -- Nimbalyst Extension

This is a **Nimbalyst extension** project. Nimbalyst is an extensible, AI-native workspace and code editor. Extensions add custom editors, AI tools, panels, themes, and more.

- **Extension ID**: `com.localhugdealer.github-theme`
- **Type**: manifest-only theme extension (no JS entry point, nothing to build)
- **Contributes**: three color themes (GitHub Light, GitHub Dark, GitHub Dark Green) via `contributions.themes`; no custom editors or file patterns

## Documentation

Use these docs in this order:

1. **Bundled SDK docs in packaged Nimbalyst**
   - Cross-platform runtime path: `path.join(process.resourcesPath, 'extension-sdk-docs')`
   - macOS example: `/Applications/Nimbalyst.app/Contents/Resources/extension-sdk-docs`
   - Windows example: `<Nimbalyst install dir>\\resources\\extension-sdk-docs`
2. **Monorepo source docs** (when developing inside the Nimbalyst repo)
   - `packages/extension-sdk-docs/README.md`
   - `packages/extension-sdk-docs/getting-started.md`
   - `packages/extension-sdk-docs/custom-editors.md`
   - `packages/extension-sdk-docs/ai-tools.md`
   - `packages/extension-sdk-docs/manifest-reference.md`
   - `packages/extension-sdk-docs/api-reference.md`
   - `packages/extension-sdk-docs/examples/`
3. **Hosted docs**
   - `https://docs.nimbalyst.com/extensions`

When examples are more helpful than prose, prefer the example projects in `packages/extension-sdk-docs/examples/` and the built-in extensions in `packages/extensions/`.

## Build and Development Workflow

This extension is **manifest-only**: `manifest.json` has no `main` field, so there is
no build step, no `dist/`, and no npm dependencies. Editing colors means editing
`manifest.json` and reloading.

| Action | How |
| --- | --- |
| Edit colors | Edit `contributions.themes[].colors` in `manifest.json` |
| Apply changes | `mcp__nimbalyst-extension-dev__extension_reload` (needs Extension Dev Tools enabled in Settings > Advanced), otherwise restart Nimbalyst |
| Check status | `mcp__nimbalyst-extension-dev__extension_get_status` with `extensionId: "com.localhugdealer.github-theme"` |
| Switch theme | `mcp__nimbalyst-host__appearance_set_theme` with `com.localhugdealer.github-theme:github-light`, `:github-dark`, or `:github-dark-green` |

The full list of supported color keys is not in the SDK docs. Grep the app bundle for
`"bg": "--nim-bg"` in `<Nimbalyst install dir>/resources/app.asar` to see the key-to-CSS-variable
map, and `deriveColorsFromTheme` nearby for which keys are auto-derived when omitted.

### Local development install

The extension is linked into Nimbalyst via a junction:
`%APPDATA%\@nimbalyst\electron\extensions\github-theme` -> this project root.
It breaks silently if this folder is renamed or moved.

## Project Structure

```
manifest.json           # The entire extension -- all three themes under contributions.themes
README.md               # Install instructions and palette table
LICENSE                 # MIT, with attribution to the upstream Obsidian theme
samples/
  theme-preview.md      # Sample file exercising every themed surface
```

## Manifest (`manifest.json`)

The manifest declares what the extension contributes to Nimbalyst. Key fields:

- **`contributions.customEditors`** -- Register editors for file patterns
- **`contributions.aiTools`** -- List AI tool names (must match the `name` field in your tool definitions)
- **`contributions.newFileMenu`** -- Add entries to File > New menu
- **`contributions.fileIcons`** -- Custom icons for file types
- **`contributions.panels`** -- Sidebar or bottom panels
- **`contributions.commands`** -- Commands with optional keybindings
- **`contributions.themes`** -- Color themes (see [EXTENSION_THEMING.md](../../docs/EXTENSION_THEMING.md); manifest-only theme extensions are supported)
- **`contributions.claudePlugin`** -- Claude Code agent skills and slash commands (see below)
- **`permissions`** -- Request `filesystem`, `ai`, or `network` access

## Claude Agent Skills (`claudePlugin`)

Extensions can bundle **Claude Code skills** -- slash commands and agent context that enhance the AI agent's capabilities within Nimbalyst.

### Directory structure

```
claude-plugin/
  .claude-plugin/
    plugin.json          # Plugin metadata
  commands/
    my-command.md        # Slash command (user types /my-command)
  skills/
    my-skill/
      SKILL.md           # Skill definition (auto-triggered by agent)
```

### Register in manifest.json

```json
{
  "contributions": {
    "claudePlugin": {
      "path": "claude-plugin",
      "displayName": "GitHub Theme",
      "description": "What the plugin provides to the agent",
      "enabledByDefault": true,
      "commands": [
        { "name": "my-command", "description": "What /my-command does" }
      ]
    }
  }
}
```

### plugin.json

```json
{
  "name": "com-localhugdealer-github-theme",
  "version": "1.0.0",
  "description": "Claude Code plugin for GitHub Theme",
  "keywords": []
}
```

### Slash command (`commands/my-command.md`)

```markdown
---
description: Short description shown in command palette
---

# /my-command

Detailed instructions for Claude when the user invokes /my-command.

The user said: $ARGUMENTS
```

### Skill (`skills/my-skill/SKILL.md`)

Skills are automatically loaded when their description matches the task. They provide domain context and tool usage instructions.

```markdown
---
name: my-skill
description: When and why the agent should use this skill (be specific so it triggers correctly)
---

# Skill Name

Instructions for the agent, including which MCP tools to use and in what order.
```

## SDK Reference

The `@nimbalyst/extension-sdk` package provides types and the Vite build helper.
The `@nimbalyst/extension-sdk` package also re-exports the `useEditorLifecycle` hook (provided by the host at runtime -- do not add `@nimbalyst/runtime` to package.json).

Key imports:
```typescript
// Types from SDK
import type {
  EditorHostProps,      // Props for custom editor components
  ExtensionAITool,      // AI tool definition
  AIToolContext,         // Context passed to tool handlers
  ExtensionToolResult,  // Return type for tool handlers
  ExtensionContext,      // Passed to activate()
  PanelHostProps,        // Props for panel components
  ExtensionStorage,      // Workspace and global key-value storage
} from '@nimbalyst/extension-sdk';

import { createExtensionConfig } from '@nimbalyst/extension-sdk/vite';

// Hook (provided by host at runtime -- do NOT add @nimbalyst/runtime to dependencies)
import { useEditorLifecycle } from '@nimbalyst/extension-sdk';
```