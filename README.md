# GitHub Theme for Nimbalyst

Two color themes that bring GitHub's look to [Nimbalyst](https://nimbalyst.com),
adapted from the [Obsidian GitHub Theme](https://github.com/krios2146/obsidian-theme-github)
by [@krios2146](https://github.com/krios2146).

- **GitHub Dark** — GitHub's dark palette on a `#0d1117` background
- **GitHub Light** — GitHub's light palette on a white background

Both cover the full editor UI, code syntax colors, diff tints, blockquotes, tables,
and the built-in terminal's 16-color ANSI palette.

## Install

In Nimbalyst, open **Settings > Extensions**, find **Install from GitHub**, and paste:

```
https://github.com/localhugdealer/nimbalyst-github-theme
```

Then pick **GitHub Dark** or **GitHub Light** in **Settings > Appearance > Theme**.

Nimbalyst installs the latest release asset, or clones this repository if no release
exists. There is nothing to build — this is a manifest-only extension.

<details>
<summary>Manual install</summary>

1. Download or clone this repository
2. Copy the folder into your Nimbalyst extensions directory:
   - Windows: `%APPDATA%\@nimbalyst\electron\extensions\`
   - macOS: `~/Library/Application Support/@nimbalyst/electron/extensions/`
   - Linux: `~/.config/@nimbalyst/electron/extensions/`
3. Restart Nimbalyst and choose the theme in Settings > Appearance

</details>

## Palette

The accent is a custom green rather than GitHub's blue. Everything else follows Primer.

| Role | GitHub Dark | GitHub Light |
| --- | --- | --- |
| Background | `#0d1117` | `#ffffff` |
| Secondary background | `#161b22` | `#f6f8fa` |
| Text | `#c9d1d9` | `#24292f` |
| Muted text | `#8b949e` | `#57606a` |
| Border | `#30363d` | `#d0d7de` |
| Accent / links | `#258d32` | `#258d32` |
| Success | `#7ee787` | `#0cb54f` |
| Warning | `#d29922` | `#bd8e37` |
| Error | `#f47067` | `#cf222e` |

Open [`samples/theme-preview.md`](samples/theme-preview.md) in Nimbalyst to see
headings, code, diffs, tables, and blockquotes under either theme.

## Customizing

Everything lives in [`manifest.json`](manifest.json) under `contributions.themes`.
Edit a color, restart Nimbalyst, and the change is live. The full set of supported
color keys is broader than the SDK docs suggest and includes `code-*` syntax colors,
`diff-*`, `table-*`, `toolbar-*`, and `terminal-*` entries; keys you omit are derived
from the core palette.

## Credits

- Palette and original design: [Vladimir Kidyaev (@krios2146)](https://github.com/krios2146),
  [Obsidian GitHub Theme](https://github.com/krios2146/obsidian-theme-github) (MIT)
- Underlying color system: [GitHub Primer](https://primer.style)

## License

[MIT](LICENSE)
