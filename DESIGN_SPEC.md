# Visual & UX Specification

### 1. Brief Inference & Vibe Read
- Vibe sentence: "Reading this as: Socratic belief deconstruction engine for intellectually rigorous seekers, with an editorial, academic, and deeply quiet visual language, leaning toward a high-contrast layout reminiscent of *The Pudding* and minimalist publisher *Distill.pub*."
- Core Dials: VARIANCE = 4/10, MOTION = 3/10, DENSITY = 6/10

### 2. Colors & Typography
- Primary Brand Color: Forest Ochre / Warm Olive (`oklch(62% 0.12 95)`) for heavy states; Sage Moss (`oklch(68% 0.08 145)`) for resolved open space.
- Background Theme: Dark Editorial Academic (`oklch(14% 0.01 240)`).
- Font Families: Sans = **Satoshi**, Mono = **Geist Mono**, Serif = **Newsreader** (for quote/belief representations).

### CSS Token Blueprint
```css
@theme {
  --background: oklch(14% 0.01 240);       /* Core midnight-ink paper */
  --foreground: oklch(89% 0.02 240);       /* Soft linen white */
  
  --card: oklch(17% 0.015 240);           /* Slate/ink overlay card */
  --card-foreground: oklch(89% 0.02 240);
  
  --muted: oklch(22% 0.02 240);           /* Silent, structural borders/bgs */
  --muted-foreground: oklch(62% 0.03 240);  /* Subdued commentary */
  
  --border: oklch(25% 0.02 240);          /* Thin gridlines, paper rules */
  
  --accent: oklch(62% 0.12 95);           /* Warm Ochre (Active challenge) */
  --accent-foreground: oklch(14% 0.01 240);
  
  /* Semantic philosophical states */
  --fact: oklch(80% 0.02 240);            /* Neutrally acknowledged truth */
  --leap-heavy: oklch(62% 0.12 95);       /* Heavy Amber-Ochre (Dogma) */
  --leap-resolved: oklch(68% 0.08 145);   /* Sage Moss (Open reflection) */
  --middle-way-glow: oklch(88% 0.04 100);  /* Soft ivory glow (Synthesis) */
}
```

### 3. Page Layout & Component Grid
- **Navbar**: Minimalist brand typography. Font: `Satoshi` Medium, 16px. Height: 56px. Border bottom `1px solid var(--border)`. Pill badge: "Guide Mode: Socratic Mirror" in `Geist Mono` 9px. Mind State Badge on right with 6px status LED.
- **Left Chat Panel**: Width 40% of viewport. Height: `calc(100vh - 56px)`. Border right `1px solid var(--border)`. Message scroller with hidden custom scrollbars. 
  - AI message: Transparent base, left border 2px (`--border`), Newsreader serif italic body. No round pill bubbles.
  - User message: Flat `--card` bg with thin `--border` wrap. Small caps label: `"USER REFLECTION"` above it. Sans font.
- **Hero / Initial Overlay**: Absolute fullscreen overlay. Card layout with square corners. Headline: "What belief feels heavy?" in Newsreader serif. CTA: Kokonut-shiny styled deconstruct button.
- **Right React Flow Canvas**: Width 60% of viewport. Background: React Flow dot grid at 15% opacity using `--border` color. Edges: SVG paths styled with animated `stroke-dashoffset`. Solid Sage Moss for resolved paths, Dashed Amber Ochre for active path, Dashed Grey for locked paths.
- **React Flow Custom Nodes**:
  - ROOT Node: Square corners, double border, Newsreader italic serif quote. Width: 300px.
  - ASSUMPTION Node: Divided into Fact (Satoshi, `--muted-foreground`) and Leap (Newsreader serif, dynamic amber-to-sage transition) with a dotted rule separator. Width: 220px.
  - MIDDLE WAY Node: Monolithic slate slab with a subtle `--middle-way-glow` shadow. Title: `"The Middle Way"`. Synthesis text: Newsreader Italic, center-aligned. Width: 340px.

### 4. Interactive & Motion Blueprints
- Transitions: React Flow progressive reveal: fade in + translate Y up (`y: 250 -> 230`, `opacity: 0 -> 1`) utilizing Spring dynamics via `motion/react` (`stiffness: 120, damping: 20`).
- Advanced Animations: Node State shift from Heavy to Resolved runs a variable transition over `450ms` using `cubic-bezier(0.16, 1, 0.3, 1)`. Chat message slide-in (200ms slide-up from bottom). Gated behind user's `prefers-reduced-motion` settings.

### 5. Visual Asset Plan
- SVG Logos needed: None (purely custom semantic badges and typography-driven UI).
- Seeded Photo placement: None (non-visual philosophical engine, layouts rely entirely on color states and high-quality type contrast).
- Node status labels: Geist Mono uppercase tags.
- Background grid: React Flow Background dot system.
- Edges animation: Custom SVG dash array shift on step completion.
