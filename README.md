# @ankh-studio/themes

Pre-composed CSS themes built on Ankh Studio design tokens. Import one file and get reset, tokens, and base styles.

Built on [@ankh-studio/tokens](https://github.com/ankh-studio/tokens) - the foundational design tokens for the Ankh Studio design system.

## Installation

```bash
npm install @ankh-studio/themes
```

## Quick Start

```css
@import '@ankh-studio/themes/default.css';
```

Or in HTML:

```html
<link rel="stylesheet" href="node_modules/@ankh-studio/themes/dist/default.css">
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

See [@ankh-studio/tokens](https://github.com/ankh-studio/tokens) for the complete token reference.

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

## Cascade Layers

Each theme declares this layer order:

```css
@layer reset, tokens, intention, palette, base, components;
```

| Layer | Purpose |
|-------|---------|
| `reset` | Normalize browser defaults |
| `tokens` | Design tokens from @ankh-studio/tokens |
| `intention` | Cognitive-intention tokens (reserved for future use) |
| `palette` | Color palette overrides (reserved for future use) |
| `base` | Typography, links, focus states |
| `components` | Component-library styles (e.g. `@ankh-studio/components`) |

### Why `components` exists

The `components` layer gives component authors a predictable place in the cascade. Styles in `@layer components { ... }` will always win over `base` but lose to unlayered application CSS. This means component packages can ship styles that integrate cleanly without specificity wars.

### Overriding theme and component styles

Unlayered CSS (the default) automatically overrides all layered styles:

```css
@import '@ankh-studio/themes/default.css';

/* This wins over any layered rule, no !important needed */
.button { background: hotpink; }
```

If your app uses its own cascade layers, declare them after `components`:

```css
@layer reset, tokens, intention, palette, base, components, app;

@layer app {
  .button { background: hotpink; }
}
```

## Documentation

- [Architecture Decision Records](./docs/adr/) - Design decisions and proposals
- [Contributing](./CONTRIBUTING.md) - How to contribute

## Changelog

### 0.2.0
- Expand cascade layer ordering: `reset, tokens, intention, palette, base, components`
- Add `intention` and `palette` layers (reserved, per ADR-001)
- Add `components` layer for component-library styles
- Document cascade layers and override patterns in README

### 0.1.0
- Initial release with default, blue, purple themes
- CSS reset included
- Automatic dark mode via `prefers-color-scheme`

## License

MIT
