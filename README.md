# Anthropic

A complete Obsidian theme reverse-engineered from [claude.ai](https://claude.ai) and the [Anthropic Design System](https://www.anthropic.com/brand).

## Why this exists

Every day, thousands of people use Claude to think, write, and build. They spend hours inside claude.ai's interface — warm Ivory backgrounds, that distinctive Clay accent, the way Anthropic Serif makes long-form text feel settled and readable. Then they switch to their notes app, and the spell breaks.

This theme closes that gap. It doesn't borrow a color or two from Anthropic's palette — it *is* the Anthropic design system, faithfully adapted to Obsidian's CSS architecture. Same fonts. Same color logic. Same attention to typographic detail that makes reading on claude.ai feel effortless.

If you think in Claude, your notes should look the part.

---

## Design Language

### Typography

Three Anthropic custom typefaces, bundled as variable-weight woff2 files (300–800), configured in a beautiful CJK-friendly layout:

| Font | Role | Where you see it | CJK Fallback |
|------|------|------------------|--------------|
| **Anthropic Serif** | Headings (H1–H5) | Reading and Editing view headings, inline title | **Genryu Mincho (源流明朝)** → Noto Serif CJK SC |
| **Anthropic Serif** | Body text | Reading view and Edit mode paragraphs, H6 | **Source Han Sans (思源黑体)** → PingFang SC |
| **Anthropic Sans** | Interface | Sidebar, tabs, buttons, settings, status bar | **PingFang SC (苹方)** → Microsoft YaHei |
| **Anthropic Mono** | Code | Code blocks, inline code, properties panel | System Monospace |

*   **Classical Woodblock Headings**: CJK headings use the SIL open licensed **Genryu Mincho (源流明朝)** to capture the woodblock-carved stroke terminals and ink-bleed corners, providing stunning literary and vintage editorial design.
*   **Highly Legible Prose**: CJK body text falls back to high-readability sans-serif fonts (**Source Han Sans / 思源黑体**) to ensure effortless screen reading for long-form content.

### Color System

**Light mode** — warm and grounded:

| Token | Value | Role |
|-------|-------|------|
| Ivory | `#FAF9F5` | Primary background — the canvas |
| Ivory Medium | `#F0EEE6` | Tab bar, status bar, secondary surfaces |
| Ivory Dark | `#EBE9E0` | Sidebar background |
| Slate | `#141413` | Headings, primary text emphasis |
| Slate Medium | `#3D3D3A` | Body text |
| Clay | `#D97757` | Interactive accent — links, buttons, focus rings, selection |

**Dark mode** — inverted hierarchy, same warmth:

| Token | Value | Role |
|-------|-------|------|
| Charcoal | `#1C1B19` | Primary background |
| Carbon | `#232220` | Secondary surfaces |
| Graphite | `#2D2C28` | Sidebar |
| Ivory | `#E8E4DB` | Primary text |
| Clay | `#D97757` | Accent (unchanged from light) |

### Interaction Design

The Clay accent (`#D97757`) is the thread that ties interaction together. It appears on:
- Active nav items and focused tabs
- Checkbox fills and link underlines
- Scrollbar thumb when dragging
- Button primary and CTA states
- Search result highlights and selection
- **Unified Dynamic Sliders**: Both the Left Sidebar (File Explorer) and the Right Sidebar (Outline/TOC) utilize a springy vertical indicator strip (`::before` pseudoclasses) that smoothly scales on active navigation item shifts, ensuring perfect UI consistency.

### Component Coverage

- **Buttons** — 4 tiers: Primary, CTA, Secondary, Tertiary
- **Callouts** — 7 color variants (Info/Sky, Warning/Kraft, Error/Fig, Success/Olive, Clay, Slate, Heather)
- **Tables** — alternating row shading, sticky header support
- **Modals & dialogs** — focus trap visual ring, consistent shadow
- **Canvas nodes** — rounded cards with subtle elevation
- **Properties panel** — monospace key labels, clean value layout
- **Search results** — warm highlight with accent outline on focus
- **Command palette** — keyboard-navigable with visible focus state
- **Print/PDF export** — clean typography, table break avoidance, hidden UI chrome

---

## Technical Architecture

### Design Tokens

All adjustable values are centralized in the `body` selector as CSS custom properties. No magic numbers in component rules.

```
body {
  --radius-s: 4px;        /* inline code, small elements */
  --radius-m: 8px;        /* buttons, inputs, code blocks */
  --radius-l: 16px;       /* cards, modals, embeds */
  --radius-xl: 24px;      /* image hero */
  --radius-pill: 100vw;   /* tags, toggles */
  --anim-fast: 0.15s cubic-bezier(0.215, 0.61, 0.355, 1);
  --anim-medium: 0.2s ease;
}
```

### Font Loading Strategy

```css
font-display: optional;
```

Fonts use `optional` display strategy — the browser uses system fonts on first paint and swaps to Anthropic fonts on next navigation. This eliminates FOIT (Flash of Invisible Text) entirely while maintaining the Anthropic visual identity for returning users.

### Accessibility

- **High contrast mode**: `@media (prefers-contrast: more)` increases text contrast and adds borders to interactive elements
- **Reduced motion**: `@media (prefers-reduced-motion: reduce)` disables all transitions and animations
- **Keyboard navigation**: Visible `:focus-visible` rings on all interactive elements (3px Clay outline with 2px offset)
- **Touch targets**: Minimum 36px height on buttons/inputs; checkbox click area expanded via `::after` pseudo-element
- **Color contrast**: Callout text colors are darkened for WCAG AA compliance in both modes

### Performance

- `content-visibility: auto` on offscreen content sections
- `will-change` hints only on actively animated properties
- GPU compositing via `translateZ(0)` on scroll containers
- `overscroll-behavior: contain` to prevent scroll chain
- No network requests — all fonts bundled locally as woff2

---

## File Structure

```
anthropic-obsidian-theme/
├── manifest.json          # Theme metadata (name, version, minAppVersion)
├── theme.css              # 1,450+ lines, single-file, zero dependencies
├── screenshot.png         # 512×288 community store preview
├── README.md              # This file
├── LICENSE                # MIT
└── fonts/
    ├── AnthropicSans-Roman.woff2       (118 KB)
    ├── AnthropicSans-Italic.woff2      (130 KB)
    ├── AnthropicSerif-Roman.woff2      (175 KB)
    ├── AnthropicSerif-Italic.woff2     (166 KB)
    ├── AnthropicMono-Roman.woff2       (66 KB)
    └── AnthropicMono-Italic.woff2      (70 KB)
```

Total package size: ~725 KB (fonts are ~624 KB, CSS is ~48 KB).

## Typography & Font Copyright Notice

To respect intellectual property rights and comply with the Obsidian Community Theme Guidelines, this repository **does not** bundle Anthropic's proprietary font files (`Anthropic Sans`, `Anthropic Serif`, `Anthropic Mono`). 

### 🌟 Out-of-the-box Experience (Default)
By default, the theme features a beautifully customized, highly-harmonious typography setup:
* **Headings (H1–H5)**: `Lora` (Serif) for English, and the exquisite woodblock-style **Genryu Mincho (源流明朝)** / **Noto Serif CJK SC (思源宋体)** for CJK characters.
* **Prose/Text**: `Lora` (warm-toned screen-friendly Serif) for English, and **Source Han Sans (思源黑体)** (highly-legible Sans-serif) for CJK text to ensure fatigue-free screen reading.
* **UI/Interface**: `Instrument Sans` / `Inter` (Sans-serif).
* **Code**: `JetBrains Mono` (Monospace).

If these fonts are installed on your system or accessible, the theme renders them beautifully with no configuration required.

### 🚀 How to Enable 100% Genuine Anthropic Look (Optional)
If you have access to Anthropic's official `woff2` font files for personal use:
1. Create a `fonts` folder inside your vault's theme directory: `.obsidian/themes/Anthropic/fonts/`
2. Place the following 6 font files into that directory and name them exactly as shown:
   * `AnthropicSans-Roman.woff2`
   * `AnthropicSans-Italic.woff2`
   * `AnthropicSerif-Roman.woff2`
   * `AnthropicSerif-Italic.woff2`
   * `AnthropicMono-Roman.woff2`
   * `AnthropicMono-Italic.woff2`
3. Restart Obsidian. The theme will seamlessly detect and apply the genuine fonts!

---

## Installation

### From Obsidian Community Themes

Settings → Appearance → Themes → Manage → search "Anthropic" → Install

### Manual

1. Download the [latest release](https://github.com/elijahchan2019/obsidian-anthropic-theme/releases)
2. Extract into your vault's `.obsidian/themes/Anthropic/` directory
3. Settings → Appearance → Theme → select "Anthropic"

---

## Compatibility

- **Obsidian**: 1.4.0+
- **Desktop**: Full support (macOS, Windows, Linux)
- **Mobile**: Supported — CJK fallbacks handle system font differences
- **Plugins**: Compatible with Style Settings for additional customization

---

## Acknowledgments

This theme is a product of Vibe Coding — designed and built entirely through conversation with Claude. No line of CSS was written by human hand. The design system was reverse-engineered from claude.ai's live interface and the public Anthropic brand guidelines.

---

## License

[MIT](LICENSE)
