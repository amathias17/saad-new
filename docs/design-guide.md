# Saad Endodontics Design Guide

## Visual Direction
Soft Modern Wellness. The site should feel calm, warm, and trustworthy with spa-like softness, rounded corners, and organic shapes. Avoid clinical, cold, or overly sharp treatments.

## Typography
**Headings:** Plus Jakarta Sans (400, 500, 600, 700, 800)
**Body:** Manrope (400, 500, 600)

Usage:
- Headings use Plus Jakarta Sans for warmth and clarity.
- Body copy uses Manrope for readable, friendly text.

CSS:
```css
font-family: 'Plus Jakarta Sans', sans-serif; /* headings */
font-family: 'Manrope', sans-serif; /* body */
```

## Color Palette
**Core neutrals and brand hues:**
- Ivory: `#FAF9F6` (primary background)
- Warm Gray: `#E8E4DF` (subtle panels)
- Sage: `#A8C5B5` (soft brand accent)
- Sage Dark: `#2A5F4F` (primary contrast)
- Terracotta: `#E8AE90` (warm accent)
- Text Primary: `#2C3E38`
- Text Secondary: `#5A6E68`

**Supporting accents:**
- Deep Green: `#1F4D3F` (CTA gradients and depth)
- Amber: `#F59E0B` (CTA highlight and ratings)

**Navigation palette (current):**
- Teal: `#02B8BF`
- Teal Light: `#40C0F2`
- Deep Teal: `#154051`
- Nav Text: `#333333`
- Nav Light Text: `#626262`
- Nav White: `#FFFFFF`
- Nav Cream: `#F6F6F6`

## Tokens (Source of Truth)
Maintain tokens in `src/styles/global.css` so new components inherit the system. Use these variable names:
```css
:root {
  --ivory: #FAF9F6;
  --warm-gray: #E8E4DF;
  --sage: #A8C5B5;
  --sage-dark: #2A5F4F;
  --terracotta: #E8AE90;
  --text-primary: #2C3E38;
  --text-secondary: #5A6E68;
  --deep-green: #1F4D3F;
  --amber: #F59E0B;
}
```

## Layout & Spacing
- Use generous vertical spacing and breathable sections.
- Typical section padding: 6rem to 8rem vertical, 1.5rem to 2rem horizontal.
- Containers generally cap around 80rem for wide layouts.

## Borders & Corners
- Cards and panels: 16px to 24px radius.
- Buttons and pills: 12px to 16px radius.
- Prefer soft, rounded silhouettes.

## Shadows
Use soft, diffused shadows with low opacity. Avoid hard drops.
Example: `0 10px 30px rgba(42, 95, 79, 0.12)`

## Gradients & Backgrounds
- Green gradient: `var(--sage-dark)` to `#1F4D3F` for CTAs.
- Warm gradient: `var(--terracotta)` to `#F59E0B` for highlights.
- Background accents: soft radial gradients using `--sage` with low opacity.

## Components Patterns
- **Hero:** Calm, spacious, with floating cards and gentle gradients.
- **Services:** Grid of cards, icon + heading + short text.
- **Testimonials:** Soft cards, warm highlights, subtle glow.
- **CTA:** Bold gradient background, primary action button.
- **Footer:** Calm, muted background with clear link clusters.

## Motion
CSS-only animations for performance. Use gentle, slow movements:
- Staggered entrance reveals
- Floating elements (low amplitude)
- Gradient shift on backgrounds

## Iconography
- Line icons with 2px stroke weight.
- Rounded shapes, simple silhouettes.
- Consistent sizing (16px to 24px in most UI).

## Accessibility
- Ensure text contrast meets WCAG AA.
- Preserve readable type sizes on mobile.
- Provide focus styles on interactive elements.
