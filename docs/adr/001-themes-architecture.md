# ADR-001: Themes as Composable and Consumable Design Layer

**Status:** Accepted
**Date:** 2026-01-30

## Context

We're building a design system following well-established patterns — Material Design, Radix, Tailwind, and others have proven that tokens, themes, and layered architecture work. We're building on that foundation.

But we have bigger intentions.

### The Proven Foundation

**What we know works:**
- Design tokens as single source of truth
- CSS custom properties for runtime theming
- Cascade layers for predictable specificity
- `light-dark()` and `prefers-color-scheme` for dark mode
- `prefers-reduced-motion` for accessibility
- Semantic color roles (primary, surface, error)
- Separation of structure (spacing, radius) from color

We're aligning with Material Design 3's multi-dimensional customization:
- Color (dynamic palettes, tonal ranges)
- Typography (type scales)
- Shape (corner radii)
- Motion (springs, easing, duration)
- Spacing/Density
- Elevation

### The Bigger Intentions

**What we're reaching for:**

1. **Cognitive context as a design dimension** — Not just "what color" but "what cognitive state." We're calling these "design intentions" (Expressive, Focus, Intense). The same interface might need different intentions in different contexts.

2. **Themes as more than color swatches** — Color calibrated for cognitive context. Purple-expressive isn't just purple + generous spacing. The colors themselves shift — higher chroma for engagement, muted baseline for expert vigilance.

3. **Granular intention control** — Not just "the whole app is Focus" but the ability for individual modules or sections to dial in their own intention. A dashboard where one panel is Intense while another is Focus.

We're exploring ways to support this. It's ongoing.

## Decision

### The Layered System

```
┌─────────────────────────────────┐
│     @ankh-studio/themes         │  ← color palettes, modes, intention calibration
├─────────────────────────────────┤
│     @ankh-studio/tokens         │  ← structure, intentions, primitives
└─────────────────────────────────┘
```

**`@ankh-studio/tokens`** provides:
- Base design tokens (spacing, typography, radius, shadow, motion)
- Design intention system (Expressive, Focus, Intense)
- Structural customization dimensions

**`@ankh-studio/themes`** provides:
- Color palettes with chromatic identity
- Mode-aware variants (light/dark, reduced motion)
- Intention-specific color calibration
- Directly consumable theme bundles

### Directly Consumable

Themes work today as single imports:

```css
@import '@ankh-studio/themes/purple.css';
/* You get: reset + tokens + palette + base styles */
```

This is the primary use case. Import a theme, build your application.

### Granular Intention Control

The goal is for individual modules or sections of a codebase to dial in their intention — not just a global setting. How we support this is being explored.

Possibilities we're considering:
- Data attributes on containers
- Scoped CSS custom property overrides
- Separate intention stylesheets that can be applied per-region

We don't have the answer yet.

### Separation of Concerns

**Tokens own structure:**
- Spacing, typography, radius, shadows, motion
- Design intentions (how these shift per cognitive context)

**Themes own color:**
- Palettes (chromatic identity)
- Light/dark mode
- Reduced motion mode
- Intention-specific color calibration

| Intention | Chroma | Contrast | Accent Usage |
|-----------|--------|----------|--------------|
| Expressive | Higher, vibrant | Softer | Liberal |
| Focus | Moderate | Balanced | Purposeful |
| Intense | Low baseline | Sharp, high-contrast alerts | Reserved for signals |

### Cascade Layer Structure

```css
@layer reset, tokens, intention, palette, base;
```

## What We're Exploring

**Granular intention mechanics:**
- How do sections/modules opt into different intentions?
- CSS-only or does it require JavaScript coordination?
- How do nested intentions interact?

**Color calibration:**
- How granular should intention-specific color shifts be?
- Per-role adjustments or systematic chroma/lightness transforms?

**Mode switching:**
- Manual user control vs system preference vs hybrid
- Per-section mode overrides

These are active questions. The answers will come from building and using the system.

## Consequences

### Positive

- Following proven patterns reduces risk
- Directly consumable themes work now
- Granular intention control opens possibilities we're still discovering
- Clear separation between tokens (structure) and themes (color)

### Negative

- Granular intention control is unproven
- Cognitive framing is unvalidated
- We're committing to a direction before knowing the mechanics

### Neutral

- Current themes work as Focus-intention defaults
- We can iterate as we learn

## Implementation Path

1. **Phase 1** (Current): Simple palette themes — directly consumable
2. **Phase 2**: Implement intention tokens in `@ankh-studio/tokens`
3. **Phase 3**: Create intention-calibrated color variants per palette
4. **Phase 4**: Explore and validate granular intention control patterns
5. **Phase 5**: Tooling for custom palette generation

## The Bet

We're betting that:
- Cognitive context is a useful design dimension
- Color calibration per intention creates meaningfully different experiences
- Granular intention control (per-module, not all-or-nothing) is valuable

These bets might be wrong. But they're worth making.
