# CLAUDE.md

## Project Context

This is a rapid prototyping workspace for a product designer at Jane.
Prototypes are interactive, code-based representations of Figma component and pattern designs.
Optimize for visual fidelity to the Figma design, using real Burrito components and tokens wherever possible.

---

## Design System: Burrito

Burrito is Jane's design system. **ALWAYS prefer Burrito components over custom HTML/CSS or third-party UI libraries.**

### Installation & Setup

```javascript
npm install @janeapp/burrito-design-system

// Required imports in every prototype's root
import '@janeapp/burrito-design-system/fonts.css';
import '@janeapp/burrito-design-system/globalTheme';
```

### Component Priority Rules

1. **First:** Use an existing Burrito component directly
2. **Second:** Compose from Burrito primitives
3. **Last resort:** Custom HTML/CSS — flag it with a `{/* TODO: No Burrito equivalent — custom component */}` comment

### Before Using Any Component

Check Storybook for the correct component name, prop names, and accepted values. Do not guess or infer API shape from other design systems.

### Documentation References

- **Storybook:** Source of truth for all component props and usage (ask me for the URL if needed)
- **Figma:** Burrito Design System UI Kit (accessible via Figma MCP)
- **Slack:** #ask-burrito-anything, #team-front-end
- **Component reference:** See `docs/burrito-components.md` in this project (if generated)

---

## Figma Integration

**Always use the Figma MCP to inspect a design before writing any code.** When I share a Figma URL:

1. Use the Figma MCP to inspect layout, components, spacing, and hierarchy
2. Identify all Figma components and map them to Burrito equivalents (e.g., Figma "Button/Primary" → `<Button variant="primary">`)
3. Identify all Figma tokens (color, spacing, typography) and map them to Burrito token equivalents — do not create custom styles for values that already exist in Burrito
4. Flag anything with no Burrito match before proceeding
5. See `docs/figma-to-burrito-mapping.md` for the mapping (if created)

---

## Tokens & Styles

**Always use Burrito tokens before writing any custom styles.** This applies to color, spacing, typography, border radius, shadows, and any other design decisions.

- Check Storybook or the Burrito theme for available token values
- If a Figma value maps to a Burrito token, use the token — not a hardcoded value
- Only write custom styles when no Burrito token or utility exists, and flag it:

```jsx
{/* TODO: No Burrito token equivalent — using custom value */}
```

---



Icons used in Figma designs have been exported as SVGs and are available in `src/assets/icons/`.

**Always check this folder first** before using any third-party icon library or creating new SVGs. The goal is for prototypes to display the same icons as the design.

```jsx
import MyIcon from '@/assets/icons/my-icon.svg';

<MyIcon />
```

If an icon from the design is missing from the folder, flag it with a comment and substitute a generic alternative so the prototype still renders:

```jsx
{/* TODO: Missing icon — need [icon-name] exported from Figma */}
```

---

## Accessibility

- All prototypes must meet **WCAG 2.2 AA** by default. Flag where they don't
- Use semantic HTML, proper heading hierarchy, visible focus states
- Burrito components handle most a11y — **do not override their accessibility features**
- Test with keyboard navigation at minimum
