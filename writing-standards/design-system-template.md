> **Brand:** [Brand name]
> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name]
> **Status:** [Draft / Final]

# Design System Template

This template governs how `design-system/design-system.md` is written and maintained. Every section listed here must appear in the document. The design system is the single source of truth for all visual decisions across the product's screens and prototypes.

---

## Required Sections

### 1. Document Header
- Metadata block (Brand, Last updated, Owner, Status)
- One-paragraph summary: what this document covers and who it's for
- Link to `product-design-overview.md` for screen context
- Link to `brand.md` for brand identity and positioning context

### 2. Design Principles
3–6 short principles that guide all design decisions. Each principle should be:
- A bold statement (e.g., "Data Density Over Decoration")
- A 1–2 sentence explanation of what it means in practice
- Specific enough to resolve ambiguous design choices

### 3. Colour System
- **3.1 Brand Palette** — table of brand colours with Name, Hex value, CSS variable, and Usage description
- **3.2 Status Colours** — table of semantic status colours. Each status maps to a foreground and a background (dim) colour. Include the specific states each colour represents (e.g., green = approved, confirmed, complete, active)
- **3.3 Neutral Palette** — table of greys and neutrals used for text, backgrounds, borders, and surfaces
- **3.4 Theme** — statement confirming whether the product uses a single theme or supports light/dark variants

### 4. Typography
- **4.1 Typefaces** — primary typeface name, source, and weights loaded; monospace typeface (if used) and when to use it
- **4.2 Type Scale** — table of every text element with Element name, Font family, Size, Weight, Letter-spacing, Colour token
- **4.3 Typography Rules** — bullet list of rules (e.g., "Table headers are always UPPERCASE with 0.06em tracking")

### 5. Spacing & Layout
- **5.1 Base Scale** — table of spacing values used throughout (based on a consistent base unit, e.g. 4px)
- **5.2 Component Spacing** — table of specific component padding and gap values
- **5.3 Border Radius** — table of border-radius values by element type
- **5.4 Full-Width Content** — explicit rule for how content fills the viewport (sidebar layouts, topbar-only layouts, tables/grids stretching to fill, behaviour on very wide screens)
- **5.5 Responsive Breakpoints** — table of breakpoints with layout behaviour at each size

### 6. Component Catalogue
One subsection per component. Each subsection must include:
- What it is — one sentence
- Variants — table of variants with visual properties (background, text, border, etc.)
- Specs — padding, font-size, font-weight, border-radius, etc.
- States — default, hover, active, disabled (where applicable)

Required components (add more as the system grows):

| Component | Notes |
|---|---|
| Buttons | Primary, secondary, danger, small modifier |
| Badges (Status) | Dot + label pattern, one variant per status |
| Metric Cards | Label, value, trend, icon |
| Data Tables | Header, body, hover, expandable rows |
| Filter Pills | Default, active |
| Tabs | Underline variant and pill variant |
| Progress Bars | Track, fill, colour rules |
| Sidebar | Expanded, collapsed, nav items, section labels |
| Topbar | Search, notifications, user context |
| Cards | Default surface container |
| Modals | Overlay + card pattern |
| Breadcrumbs | Separator, current-page styling |
| Toast Notifications | Success, info, warning, error variants |

### 7. Iconography
- Icon style (e.g., stroked SVGs, Heroicons-style)
- Default sizes (nav, button, placeholder)
- Stroke width and line cap/join
- Colour inheritance rules

### 8. Shadows & Elevation
- **8.1 Elevation Levels** — table of shadow levels with CSS values and usage
- **8.2 Theme Variants** — note whether shadow/elevation values differ between light/dark themes, or whether a single theme is used throughout

### 9. Animation & Transitions
Table of all animations with: Name, CSS definition, and where they're used.

### 10. CSS Variables — Copy-Paste Reference
Complete `:root` block, ready to copy into a stylesheet. This is the developer-facing quick reference.

### 11. Prototype Warning Banner
Spec for the required demo warning banner shown on every `design-preview-[name].html`. Include the exact CSS and HTML so it can be copy-pasted directly.

---

## Maintenance Rules

- When a new component pattern appears in any prototype → add it to the catalogue
- When a colour is introduced → add it to the palette and theme mapping
- When a token changes → update both the semantic table and the CSS reference block
- When a new animation is added → add it to the animation table
- Flag which `design-preview-[name].html` files need regeneration after any change
- Always update the "Last updated" date in the metadata header
- Log all changes to the change-log, if one exists for this repo
