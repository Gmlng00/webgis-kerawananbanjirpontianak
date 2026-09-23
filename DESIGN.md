# DESIGN.md — WebGIS Kerawanan Banjir Kota Pontianak
> Reference for AI agents and developers. Defines the visual language, design tokens, and component contracts for this dashboard.

---

## Design Philosophy

**Principle: "Neutral Frame, Vivid Data"**

The chrome (header, sidebar, panels) should be quiet, neutral, and professional — it is the *frame*, not the *painting*. The map canvas and spatial data are the star. Every UI decision should push visual weight toward the data, not away from it.

**Avoid:**
- Loud electric-blue gradients spanning the full header
- Oversaturated badge pills stacked side-by-side
- Hard-edged card borders with heavy shadows
- Generic "AI dashboard" patterns: pastel stat cards with identical icons, neon glow effects

**Pursue:**
- Thin 1px borders, near-invisible dividers
- Soft ambient shadows (multiple layered, very low opacity)
- Generous spacing — breathe between elements
- Typographic hierarchy (weight + size, not color alone)
- Micro-interactions that feel instant yet smooth (150–200ms)

---

## Color Tokens

### Neutrals (Core Palette)
These drive all chrome, text, and surface colors. Derived from a warm-neutral Zinc scale.

```css
--color-bg-base:       #F7F8FA;   /* Page background — off-white, not pure white */
--color-bg-surface:    #FFFFFF;   /* Sidebar, panels, cards */
--color-bg-subtle:     #F4F5F7;   /* Secondary surfaces, input fills */
--color-bg-hover:      #EEF0F3;   /* Hover state on list items */

--color-border:        #E4E6EA;   /* Default border — 1px solid */
--color-border-strong: #C8CDD6;   /* Elevated borders, dividers */

--color-text-primary:  #18191B;   /* Headers, labels — near-black */
--color-text-secondary:#52555F;   /* Body copy, descriptions */
--color-text-muted:    #8B8FA6;   /* Placeholders, metadata, captions */
--color-text-inverse:  #FFFFFF;   /* Text on dark backgrounds */
```

### Brand — GIS Blue (Restrained Use)
Only used for: active states, primary CTAs, focus rings. **Never** for large surfaces.

```css
--color-brand:         #2563EB;   /* Primary brand — calm cobalt */
--color-brand-hover:   #1D4ED8;   /* On hover */
--color-brand-subtle:  #EFF6FF;   /* Background tint for selected states */
--color-brand-muted:   #BFDBFE;   /* Border for active/selected items */
```

### Hazard — Flood Risk Classification (Cartographic Standard)
These must remain unchanged — they map directly to research classification output.

```css
--color-rawan-tinggi:  #DC2626;   /* High risk   — saturated red    */
--color-rawan-sedang:  #EA7500;   /* Medium risk — deep amber       */
--color-rawan-rendah:  #EAB308;   /* Low risk    — golden yellow    */
--color-rawan-tidak:   #E5E7EB;   /* No flood    — light gray       */
--color-air:           #7DD3FC;   /* Water body  — sky blue         */
--color-air-border:    #0EA5E9;   /* Water border                   */
```

---

## Typography

**Font Family:** `'Inter', system-ui, sans-serif`

| Token         | Size  | Weight | Usage                          |
|---------------|-------|--------|-------------------------------|
| `--text-xs`   | 10px  | 500    | Section labels (ALL CAPS), captions |
| `--text-sm`   | 11.5px| 400    | Table data, metadata           |
| `--text-base` | 13px  | 400    | Sidebar body copy              |
| `--text-md`   | 14px  | 600    | Card headings, panel titles    |
| `--text-lg`   | 17px  | 700    | Stat values                    |
| `--text-xl`   | 22px  | 800    | Large metric numbers           |

---

## Shadow System

Layered, ambient — never hard or plastic-looking.

```css
--shadow-sm:       0 1px 2px rgba(0,0,0,0.05), 0 1px 3px rgba(0,0,0,0.04);
--shadow-md:       0 2px 6px rgba(0,0,0,0.06), 0 4px 12px rgba(0,0,0,0.06);
--shadow-lg:       0 4px 16px rgba(0,0,0,0.08), 0 8px 32px rgba(0,0,0,0.06);
--shadow-floating: 0 8px 24px rgba(0,0,0,0.10), 0 2px 6px rgba(0,0,0,0.06);
```

---

## Border Radius

```css
--radius-xs:  4px    /* Chips, tight badges */
--radius-sm:  6px    /* Buttons, inputs, small cards */
--radius-md:  8px    /* Cards, panels */
--radius-lg:  12px   /* Floating surfaces */
--radius-xl:  16px   /* Modal dialogs */
```

---

## Motion

```css
--ease-default: cubic-bezier(0.4, 0, 0.2, 1);
--duration-fast:   100ms;   /* Hover color changes */
--duration-base:   150ms;   /* Most transitions */
--duration-slow:   250ms;   /* Layout shifts */
--duration-panel:  300ms;   /* Drawer/sidebar slide */
```

---

## Layout Dimensions

```css
--header-h:   58px;    /* Tighter than before */
--sidebar-w:  300px;   /* Slightly narrower */
--panel-h:    280px;   /* Bottom chart drawer */
```

---

## Component Specs

### Header
- Background: white (`--color-bg-surface`) + `border-bottom: 1px solid --color-border`
- **NO gradient** — the gradient reads as "old government dashboard"
- Logo: small rounded icon, brand color (`--color-brand`)
- Title: `13–14px`, weight 600, `--color-text-primary`
- Subtitle/meta: `11px`, weight 400, `--color-text-muted`
- Badges: flat, `background: --color-bg-subtle`, `border: 1px solid --color-border`, small text
- Action buttons: ghost style — border only, on hover background `--color-brand-subtle`

### Sidebar — Section Labels
- `10px` ALL CAPS, `--color-text-muted`, letter-spacing `0.07em`
- **No icon prefix** — remove icon clutter from section headers

### Stat Cards
- **Remove colored icon boxes** — use a single colored number instead
- `background: --color-bg-subtle`, `border: 1px solid --color-border`, `border-radius: 8px`
- Value: large + colored, Label: `--text-xs` muted

### Progress Bars
- Height: 5px (thinner = more refined)
- Track: `--color-border`

### Layer Items
- Simple rows with padding and bottom divider — remove card-like background

### FAB Buttons (Map Controls)
- White + `--shadow-floating` + `--radius-sm`
- On hover: `--color-brand-subtle` bg, `--color-brand` icon color

### Map Legend
- White card, `--shadow-floating`, `--radius-md`
- Swatches: 14×9px, `--radius-xs`

### Popup
- `border-radius: 10px`, `--shadow-floating`
- Title bottom border: `2px solid --color-brand`

---

## Anti-patterns to Avoid

| ❌ Avoid                                      | ✅ Do instead                                  |
|----------------------------------------------|-----------------------------------------------|
| Electric gradient headers                     | White header with 1px bottom border           |
| 3+ pill badges stacked in header             | Max 2 metadata chips, move rest to sidebar    |
| Heavy `box-shadow` everywhere                | Layered micro-shadows on floating items only   |
| Colored icon boxes in stat cards             | Colored numeral, monochrome label              |
| Progress bar height > 6px                    | 5px for refinement                             |
| `border-radius: 20px` on rectangular cards  | 8px max on cards                               |
