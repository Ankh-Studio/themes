# @okja/chi-themes

Pre-composed CSS themes built on Chi Design System tokens. Import one file and get reset, tokens, and base styles.

Built on [@okja/chi-tokens](https://github.com/Okja-Engineering/chi-tokens) - the foundational design tokens for the Chi Design System.

## Installation

```bash
npm install @okja/chi-themes
```

## Quick Start

```css
@import '@okja/chi-themes/default.css';
```

Or in HTML:

```html
<link rel="stylesheet" href="node_modules/@okja/chi-themes/dist/default.css">
```

## Available Themes

| Theme | Description |
|-------|-------------|
| `default.css` | Grayscale - wireframing, prototyping |
| `blue.css` | Corporate blue - healthcare, enterprise |
| `purple.css` | Creative purple - consumer apps |
| `reset.css` | Reset only - bring your own tokens |

## Using Tokens

All themes include design tokens:

```css
.card {
  background: var(--color-surface-container);
  padding: var(--space-4);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-2);
}

.button {
  background: var(--color-primary);
  color: var(--color-on-primary);
  font-family: var(--font-sans);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-sm);
  transition: opacity var(--duration-short2) var(--easing-standard);
}
```

### Token Categories

- **Colors** - Primary, secondary, surface, error (auto light/dark)
- **Spacing** - 9-step scale (`--space-1` to `--space-9`)
- **Typography** - Fonts, sizes, weights, line heights
- **Radius** - `--radius-none` through `--radius-full`
- **Shadows** - `--shadow-0` through `--shadow-5`
- **Motion** - Durations and easings

See [@okja/chi-tokens](https://github.com/Okja-Engineering/chi-tokens) for the complete token reference.

## Dark Mode

Colors adapt automatically via `prefers-color-scheme`. No configuration needed.

## Browser Support

Requires browsers supporting:
- CSS `light-dark()` function
- OKLCH color space
- CSS Cascade Layers (`@layer`)

**Supported:** Chrome 123+, Safari 17.5+, Firefox 120+

## Customization

### Scaling

```html
<html data-scaling="110">
```

Options: `90`, `95`, `100` (default), `105`, `110`

### Border Radius

```html
<html data-radius="large">
```

Options: `none`, `small`, `medium` (default), `large`

## Architecture

Each theme uses CSS Cascade Layers:

```css
@layer reset, tokens, base;
```

- **reset** - Normalize browser defaults
- **tokens** - Design tokens from @okja/chi-tokens
- **base** - Typography, links, focus states

Your styles layer on top, giving you full cascade control.

## Changelog

### 0.1.0
- Initial release with default, blue, purple themes
- CSS reset included
- Automatic dark mode via `prefers-color-scheme`

## License

MIT
