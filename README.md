# Folio

An elegant, warm, and highly readable Obsidian theme inspired by beautiful editorial design and modern literary publishing aesthetics, featuring a carefully calibrated layout with beautiful typography, high-readability margins, and a comfortable warm ivory and clay palette.

## Why this exists

Many writers, researchers, and developers love the warm, literary look of modern publishing—characterized by soft Ivory backgrounds, subtle Clay accents, and a serif font stack that makes long-form reading effortless. This theme adapts those design philosophies to Obsidian's CSS architecture.

---

## Design Language

### Typography

The theme leverages high-fidelity open-source typefaces configured in a beautiful, highly legible CJK-friendly layout:

| Font | Role | Where you see it | CJK Fallback |
|------|------|------------------|--------------|
| **Lora** / Georgia | Headings (H1–H5) | Reading and Editing view headings, inline title | **Genryu Mincho (源流明朝)** → Noto Serif CJK SC |
| **Lora** / Georgia | Body text | Reading view and Edit mode paragraphs, H6 | **Source Han Sans (思源黑体)** → PingFang SC |
| **Instrument Sans** / Inter | Interface | Sidebar, tabs, buttons, settings, status bar | **PingFang SC (苹方)** → Microsoft YaHei |
| **JetBrains Mono** | Code | Code blocks, inline code, properties panel | System Monospace |

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

Fonts use `optional` display strategy — the browser uses system fonts on first paint and swaps to custom fonts on next navigation. This eliminates FOIT (Flash of Invisible Text) entirely while maintaining the theme's visual identity for returning users.

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


---

## Compatibility

- **Obsidian**: 1.4.0+
- **Desktop**: Full support (macOS, Windows, Linux)
- **Mobile**: Supported — CJK fallbacks handle system font differences
- **Plugins**: Compatible with Style Settings for additional customization

---

## Acknowledgments

This theme is designed and built entirely through pair-programming conversation with AI. It is an independent homage to beautiful, editorial web interfaces.

---

## License

[MIT](LICENSE)
