# GitHub Theme preview

This file exercises the surfaces the **GitHub Light**, **GitHub Dark**, and **GitHub Dark Green** themes color.
Switch themes in Settings > Appearance > Theme and compare against github.com.

## Text and links

Body text with *emphasis*, **strong**, ~~strikethrough~~, `inline code`, and a [link to GitHub](https://github.com).
Muted secondary text shows up in captions and metadata, and ==highlighted text== uses the yellow tint.

> Blockquotes use GitHub's gray left border and muted text color.

## Lists and tasks

- [x] Ported the Primer dark palette
- [x] Ported the Primer light palette
- [x] Added a green-accent dark variant
- [ ] Compare against github.com side by side

1. First
2. Second
3. Third

## Code

```typescript
// Syntax colors: comment, keyword, string, function, property, variable
import { readFile } from 'node:fs/promises';

export async function loadTheme(path: string): Promise<Theme> {
  const raw = await readFile(path, 'utf-8');
  const theme = JSON.parse(raw) as Theme;
  return { ...theme, isDark: theme.colors.bg === '#0d1117' };
}
```

```diff
- "primary": "#0e639c",
+ "primary": "#58a6ff",
```

## Table

| Token | Light | Dark | Dark Green |
| --- | --- | --- | --- |
| bg | `#ffffff` | `#0d1117` | `#0d1117` |
| text | `#24292f` | `#c9d1d9` | `#c9d1d9` |
| primary | `#0969da` | `#58a6ff` | `#258d32` |
| success | `#0cb54f` | `#7ee787` | `#7ee787` |
| error | `#cf222e` | `#f47067` | `#f47067` |

---

Horizontal rule above uses the border color.
