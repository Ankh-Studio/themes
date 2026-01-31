# Contributing

Thanks for your interest in contributing to @ankh-studio/themes.

## Setup

```bash
git clone https://github.com/ankh-studio/themes.git
cd themes
nvm use
npm install
```

## Development

```bash
npm run lint    # Check CSS style
npm run build   # Compile themes to dist/
```

## Making Changes

1. Create a branch from `main`
2. Make your changes in `src/`
3. Run `npm run lint` and `npm run build`
4. Submit a pull request

## Code Style

- CSS custom properties only (no preprocessors)
- Follow existing naming conventions
- Use tokens from `@ankh-studio/tokens`
- Run `npm run lint` before committing

## Theme Structure

Each theme file should:

1. Import CSS reset
2. Import tokens (base + color palette)
3. Define base styles in `@layer base`

## Design Decisions

Significant changes should be discussed first. For new themes or architectural changes, consider proposing an [ADR](./docs/adr/).

## Questions

Open an issue for discussion before starting large changes.
