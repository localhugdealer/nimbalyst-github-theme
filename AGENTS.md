# AGENTS.md

This is a Nimbalyst extension project. Read [CLAUDE.md](./CLAUDE.md) before making changes.

## What This Project Is

- Extension ID: `com.localhugdealer.github-theme`
- Type: manifest-only theme extension (no `main`, no build output)
- All theme colors live in `manifest.json` under `contributions.themes`

## Documentation

Use these docs in this order:

1. Bundled SDK docs in packaged Nimbalyst:
  - Runtime path: `path.join(process.resourcesPath, 'extension-sdk-docs')`
  - macOS example: `/Applications/Nimbalyst.app/Contents/Resources/extension-sdk-docs`
  - Windows example: `<Nimbalyst install dir>\\resources\\extension-sdk-docs`
2. Monorepo source docs when available:
  - `packages/extension-sdk-docs/README.md`
  - `packages/extension-sdk-docs/getting-started.md`
  - `packages/extension-sdk-docs/custom-editors.md`
  - `packages/extension-sdk-docs/ai-tools.md`
  - `packages/extension-sdk-docs/manifest-reference.md`
  - `packages/extension-sdk-docs/api-reference.md`
  - `packages/extension-sdk-docs/examples/`
3. Hosted docs:
  - `https://docs.nimbalyst.com/extensions`

## Required Workflow

- Run `npm install` once before the first build
- Build with `mcp__nimbalyst-extension-dev__extension_build`
- Install with `mcp__nimbalyst-extension-dev__extension_install`
- Iterate with `mcp__nimbalyst-extension-dev__extension_reload`
- Check status with `mcp__nimbalyst-extension-dev__extension_get_status`
- Use main and renderer log MCP tools for debugging
- Do not restart Nimbalyst unless the user explicitly asks
- When possible, create a representative sample file and use it to verify the extension after install or reload
- After a successful install, tell the user the extension is installed and available across all of their Nimbalyst projects

## Validation Checklist

- `manifest.json > main` matches the file Vite emits in `dist/`
- Every `customEditors[].component` entry matches a key in the exported `components` object
- Every tool name listed in `contributions.aiTools` has a matching exported handler
- Custom editors use `host.loadContent()`, `host.onSaveRequested()`, `host.onFileChanged()`, and `host.setDirty()`
- Styling uses Nimbalyst CSS variables such as `--nim-bg`, `--nim-text`, and `--nim-border`

## When Unsure

- Follow [CLAUDE.md](./CLAUDE.md) as the authoritative project guide
- Prefer SDK docs and local examples over inventing patterns
