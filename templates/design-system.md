---
title: "{{PROJECT_NAME}} — Design System Reference"
aliases:
  - "{{PROJECT_NAME}} Design System"
  - "{{PROJECT_NAME}} UI"
  - "{{PROJECT_SHORT}} Design"
tags:
  - type/resource
  - para/resource
  - topic/design
  - topic/design-system
created: "{{CREATED_DATE}}"
updated: "{{UPDATED_DATE}}"
type: "resource"
id: "{{ID}}"
source: "{{SOURCE_URL}}"
---

# {{PROJECT_NAME}} — Design System Reference

> {{ONE_LINE_DESCRIPTION}}. Source: [{{SOURCE_NAME}}]({{SOURCE_URL}})

---

## 1. Design Philosophy

- {{PHILOSOPHY_POINT_1}}
- {{PHILOSOPHY_POINT_2}}
- {{PHILOSOPHY_POINT_3}}
- {{PHILOSOPHY_POINT_4}}

---

## 2. Full Page Layout Sketch (ASCII Wireframe)

```
{{ASCII_WIREFRAME}}
```

---

## 3. Scroll & Section Flow Model

```
SCROLL POSITION:     TOP ----------------------------------------> BOTTOM

                     +------++------++------+
SECTION FLOW:        | A    || B    || C    |
(reveal pattern)     |fade^ ||fade^ ||fade^ |
                     +--+---++--+---++--+---+
                        |       |       |
TIMING:              0ms    100ms    200ms
```

### Scroll Behavior

| Property         | Value                | Notes               |
| ---------------- | -------------------- | ------------------- |
| Scroll type      | {{SCROLL_TYPE}}      | {{SCROLL_NOTES}}    |
| Section snap     | {{SECTION_SNAP}}     | {{SNAP_NOTES}}      |
| Reveal trigger   | {{REVEAL_TRIGGER}}   | {{REVEAL_NOTES}}    |
| Reveal direction | {{REVEAL_DIRECTION}} | {{DIRECTION_NOTES}} |
| Navbar           | {{NAVBAR_TYPE}}      | {{NAVBAR_NOTES}}    |

---

## 4. Animation & Motion System

### 4.1 Design Tokens -- Motion

```css
/* Timing functions */
--ease-default:     {{EASE_DEFAULT}};
--ease-enter:       {{EASE_ENTER}};
--ease-exit:        {{EASE_EXIT}};
--ease-bounce:      {{EASE_BOUNCE}};

/* Durations */
--duration-instant:  {{DURATION_INSTANT}};
--duration-fast:     {{DURATION_FAST}};
--duration-normal:   {{DURATION_NORMAL}};
--duration-medium:   {{DURATION_MEDIUM}};
--duration-slow:     {{DURATION_SLOW}};
--duration-dramatic: {{DURATION_DRAMATIC}};

/* Stagger */
--stagger-cards:     {{STAGGER_CARDS}};
--stagger-features:  {{STAGGER_FEATURES}};
--stagger-lines:     {{STAGGER_LINES}};
```

### 4.2 Keyframe Animations

```css
/* Card entrance */
@keyframes cardIn {
  from {
    opacity: 0;
    transform: translateY({{CARD_IN_Y}}) scale({{CARD_IN_SCALE}});
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

/* Hero text lines */
@keyframes heroLineIn {
  from {
    opacity: 0;
    transform: translateY({{HERO_LINE_Y}});
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Floating / hover indicator */
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50%      { transform: translateY(-{{FLOAT_DISTANCE}}); }
}

/* Pulse / glow for CTAs */
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 0 0 {{GLOW_COLOR}}; }
  50%      { box-shadow: 0 0 {{GLOW_SIZE}} {{GLOW_SPREAD}} {{GLOW_COLOR}}; }
}

/* Shimmer / loading */
@keyframes shimmer {
  0%   { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}
```

### 4.3 Transition Defaults

```css
/* Interactive elements */
transition: border-color {{TRANSITION_DURATION}}, box-shadow {{TRANSITION_DURATION}}, transform {{TRANSITION_DURATION}};

/* Color transitions */
transition: color {{TRANSITION_FAST}}, background-color {{TRANSITION_FAST}};

/* Card hover */
transition: transform {{TRANSITION_DURATION}}, box-shadow {{TRANSITION_DURATION}};
```

### 4.4 Scroll-Triggered Reveal Pattern

```
+--------------------------------------------------+
|  VIEWPORT                                        |
|                                                  |
|  +------------------------------------------+    |
|  |  Element visible -- fully opaque           |    |
|  +------------------------------------------+    |
|                                                  |
| - - - - - INTERSECTION THRESHOLD - - - - - - -  |  ~{{INTERSECTION_THRESHOLD}} from bottom
|                                                  |
|  +------------------------------------------+    |
|  |  Element entering -- animation triggers   |    |
|  +------------------------------------------+    |
|                                                  |
+--------------------------------------------------+
|  +------------------------------------------+    |
|  |  Element below fold -- hidden (opacity 0) |    |
|  +------------------------------------------+    |
```

---

## 5. Component Motion Catalog

### 5.1 {{COMPONENT_1_NAME}} ({{COMPONENT_1_TYPE}})

| State               | Property   | Value     |
| ------------------- | ---------- | --------- |
| {{STATE_1_DEFAULT}} | {{PROP_1}} | {{VAL_1}} |
| {{STATE_1_HOVER}}   | {{PROP_2}} | {{VAL_2}} |
| {{STATE_1_ACTIVE}}  | {{PROP_3}} | {{VAL_3}} |

```
{{COMPONENT_1_ASCII}}
```

### 5.2 {{COMPONENT_2_NAME}} ({{COMPONENT_2_TYPE}})

| State               | Property   | Value     |
| ------------------- | ---------- | --------- |
| {{STATE_2_DEFAULT}} | {{PROP_4}} | {{VAL_4}} |
| {{STATE_2_HOVER}}   | {{PROP_5}} | {{VAL_5}} |

```
{{COMPONENT_2_ASCII}}
```

---

## 6. Color Palette

### Dark Mode (Primary)

| Token                    | Value                | Usage                    |
| ------------------------ | -------------------- | ------------------------ |
| `--bg-page`              | `{{BG_PAGE}}`        | Page background          |
| `--bg-surface`           | `{{BG_SURFACE}}`     | Cards, elevated surfaces |
| `--bg-navbar`            | `{{BG_NAVBAR}}`      | Navbar                   |
| `--bg-footer`            | `{{BG_FOOTER}}`      | Footer                   |
| `--color-primary`        | `{{COLOR_PRIMARY}}`  | Primary accent, CTAs     |
| `--color-primary-hover`  | `{{PRIMARY_HOVER}}`  | Hover state              |
| `--color-primary-active` | `{{PRIMARY_ACTIVE}}` | Active state             |
| `--color-primary-muted`  | `{{PRIMARY_MUTED}}`  | Disabled/muted           |
| `--text-primary`         | `{{TEXT_PRIMARY}}`   | Main body text           |
| `--text-secondary`       | `{{TEXT_SECONDARY}}` | Muted text               |
| `--border-default`       | `{{BORDER_DEFAULT}}` | Borders, dividers        |
| `--border-hover`         | `{{BORDER_HOVER}}`   | Hover borders            |
| `--glow`                 | `{{GLOW_VALUE}}`     | Button shadows           |

### Light Mode (Secondary)

| Token                    | Value                      | Usage          |
| ------------------------ | -------------------------- | -------------- |
| `--color-primary`        | `{{LIGHT_PRIMARY}}`        | Primary accent |
| `--color-primary-hover`  | `{{LIGHT_PRIMARY_HOVER}}`  | Hover          |
| `--color-primary-active` | `{{LIGHT_PRIMARY_ACTIVE}}` | Active         |
| `--color-primary-muted`  | `{{LIGHT_PRIMARY_MUTED}}`  | Disabled/muted |

---

## 7. Typography System

### Font Stack

```css
--font-base: "{{FONT_BASE}}", {{FONT_FALLBACK}};
--font-mono: "{{FONT_MONO}}", {{FONT_MONO_FALLBACK}};
```

### Type Scale

| Element         | Size                  | Weight                  | Line-height         | Letter-spacing      | Font                  |
| --------------- | --------------------- | ----------------------- | ------------------- | ------------------- | --------------------- |
| Hero headline   | {{TYPE_HERO_SIZE}}    | {{TYPE_HERO_WEIGHT}}    | {{TYPE_HERO_LH}}    | {{TYPE_HERO_LS}}    | {{TYPE_HERO_FONT}}    |
| Section title   | {{TYPE_SECTION_SIZE}} | {{TYPE_SECTION_WEIGHT}} | {{TYPE_SECTION_LH}} | {{TYPE_SECTION_LS}} | {{TYPE_SECTION_FONT}} |
| Card heading    | {{TYPE_CARD_SIZE}}    | {{TYPE_CARD_WEIGHT}}    | {{TYPE_CARD_LH}}    | {{TYPE_CARD_LS}}    | {{TYPE_CARD_FONT}}    |
| Body text       | {{TYPE_BODY_SIZE}}    | {{TYPE_BODY_WEIGHT}}    | {{TYPE_BODY_LH}}    | 0                   | {{TYPE_BODY_FONT}}    |
| Small / caption | {{TYPE_SMALL_SIZE}}   | {{TYPE_SMALL_WEIGHT}}   | {{TYPE_SMALL_LH}}   | 0                   | {{TYPE_SMALL_FONT}}   |
| Button text     | {{TYPE_BUTTON_SIZE}}  | {{TYPE_BUTTON_WEIGHT}}  | {{TYPE_BUTTON_LH}}  | 0                   | {{TYPE_BUTTON_FONT}}  |
| Code / mono     | {{TYPE_CODE_SIZE}}    | {{TYPE_CODE_WEIGHT}}    | {{TYPE_CODE_LH}}    | 0                   | Mono                  |
| Footer          | {{TYPE_FOOTER_SIZE}}  | {{TYPE_FOOTER_WEIGHT}}  | {{TYPE_FOOTER_LH}}  | 0                   | {{TYPE_FOOTER_FONT}}  |

---

## 8. Spacing System

```
{{SPACING_UNIT}}px -- micro (icon padding, badge padding)
{{SPACING_UNIT_2}}px -- tight (inline gaps, compact padding)
{{SPACING_UNIT_3}}px -- small (button vertical padding, card internal gaps)
{{SPACING_UNIT_4}}px -- base (section internal padding, card gaps)
{{SPACING_UNIT_5}}px -- medium (between card heading and body)
{{SPACING_UNIT_6}}px -- large (card padding, between sections on mobile)
{{SPACING_UNIT_7}}px -- section (between major sections)
{{SPACING_UNIT_8}}px -- page (top/bottom page margins)
{{SPACING_UNIT_9}}px -- dramatic (hero vertical padding)
```

---

## 9. Background & Texture

```css
/* Pattern */
background-image: {{BACKGROUND_PATTERN}};
background-size: {{PATTERN_SIZE}};
```

### Page Background Layers (bottom to top)

```
Layer 1: Solid {{BG_LAYER_1}}
Layer 2: {{BG_LAYER_2}}
Layer 3: Content
Layer 4: Navbar ({{NAVBAR_EFFECT}})
```

---

## 10. Border & Radius System

| Token           | Value           | Usage               |
| --------------- | --------------- | ------------------- |
| `--radius-sm`   | {{RADIUS_SM}}   | Inline code, badges |
| `--radius-md`   | {{RADIUS_MD}}   | Buttons, inputs     |
| `--radius-lg`   | {{RADIUS_LG}}   | Cards, modals       |
| `--radius-xl`   | {{RADIUS_XL}}   | Feature preview     |
| `--radius-full` | {{RADIUS_FULL}} | Pills, avatars      |

### Border Colors

```css
/* Standard */     {{BORDER_STANDARD}}
/* Hover */        {{BORDER_HOVER_STYLE}}
/* Active/Focus */ {{BORDER_ACTIVE_STYLE}}
```

---

## 11. Shadow & Glow System

```css
/* Card default */       box-shadow: {{SHADOW_CARD}};
/* Card hover */         box-shadow: {{SHADOW_CARD_HOVER}};
/* Button hover */       box-shadow: {{SHADOW_BUTTON_HOVER}};
/* Focus ring */         outline: {{FOCUS_RING}};
/* Navbar shadow */      box-shadow: {{SHADOW_NAVBAR}};
```

---

## 12. Responsive Breakpoints

| Breakpoint | Width                                 | Behavior                |
| ---------- | ------------------------------------- | ----------------------- |
| Mobile     | < {{BP_MOBILE}}px                     | {{BP_MOBILE_BEHAVIOR}}  |
| Tablet     | {{BP_TABLET_MIN}}-{{BP_TABLET_MAX}}px | {{BP_TABLET_BEHAVIOR}}  |
| Desktop    | > {{BP_DESKTOP}}px                    | {{BP_DESKTOP_BEHAVIOR}} |
| Wide       | > {{BP_WIDE}}px                       | {{BP_WIDE_BEHAVIOR}}    |

### Container

```css
max-width: {{CONTAINER_MAX}}px;
margin: 0 auto;
padding: 0 {{CONTAINER_PADDING}}px;
```

---

## 13. Accessibility & Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

- {{ACCESSIBILITY_NOTE_1}}
- {{ACCESSIBILITY_NOTE_2}}
- {{ACCESSIBILITY_NOTE_3}}

---

## 14. Interaction States Summary

```
                  DEFAULT          HOVER              ACTIVE            FOCUS
---------------------------------------------------------------------------------
Card border       {{CARD_BORDER_D}} {{CARD_BORDER_H}}   {{CARD_BORDER_A}}   {{CARD_BORDER_F}}
Card bg           {{CARD_BG_D}}     {{CARD_BG_H}}       {{CARD_BG_A}}       {{CARD_BG_F}}
Card transform    {{CARD_TF_D}}     {{CARD_TF_H}}       {{CARD_TF_A}}       {{CARD_TF_F}}
Button bg         {{BTN_BG_D}}      {{BTN_BG_H}}        {{BTN_BG_A}}        {{BTN_BG_F}}
Button transform  {{BTN_TF_D}}      {{BTN_TF_H}}        {{BTN_TF_A}}        {{BTN_TF_F}}
Link color        {{LINK_C_D}}      {{LINK_C_H}}        {{LINK_C_A}}        {{LINK_C_F}}
Nav link          {{NAV_C_D}}       {{NAV_C_H}}         {{NAV_C_A}}         {{NAV_C_F}}
```

---

## 15. Complete CSS Variables (Copy-Paste Ready)

```css
:root {
  /* Typography */
  --font-base: '{{FONT_BASE}}', {{FONT_FALLBACK}};
  --font-mono: '{{FONT_MONO}}', {{FONT_MONO_FALLBACK}};
  --code-font-size: {{CODE_FONT_SIZE}};
  --heading-font-weight: {{HEADING_WEIGHT}};

  /* Motion */
  --duration-fast: {{DURATION_FAST}};
  --duration-normal: {{DURATION_NORMAL}};
  --duration-medium: {{DURATION_MEDIUM}};
  --duration-slow: {{DURATION_SLOW}};
  --ease-default: {{EASE_DEFAULT}};
  --stagger-card: {{STAGGER_CARDS}};

  /* Spacing */
  --space-xs: {{SPACE_XS}};
  --space-sm: {{SPACE_SM}};
  --space-md: {{SPACE_MD}};
  --space-lg: {{SPACE_LG}};
  --space-xl: {{SPACE_XL}};
  --space-2xl: {{SPACE_2XL}};
  --space-3xl: {{SPACE_3XL}};

  /* Radius */
  --radius-sm: {{RADIUS_SM}};
  --radius-md: {{RADIUS_MD}};
  --radius-lg: {{RADIUS_LG}};
  --radius-xl: {{RADIUS_XL}};
  --radius-full: {{RADIUS_FULL}};
}

[data-theme='dark'] {
  /* Backgrounds */
  --bg-page: {{BG_PAGE}};
  --bg-surface: {{BG_SURFACE}};
  --bg-navbar: {{BG_NAVBAR}};
  --bg-footer: {{BG_FOOTER}};
  --bg-code: {{BG_CODE}};

  /* Primary */
  --color-primary: {{COLOR_PRIMARY}};
  --color-primary-hover: {{PRIMARY_HOVER}};
  --color-primary-active: {{PRIMARY_ACTIVE}};
  --color-primary-muted: {{PRIMARY_MUTED}};

  /* Text */
  --text-primary: {{TEXT_PRIMARY}};
  --text-secondary: {{TEXT_SECONDARY}};

  /* Borders */
  --border-default: {{BORDER_DEFAULT}};
  --border-hover: {{BORDER_HOVER}};
  --border-active: {{BORDER_ACTIVE}};

  /* Shadows */
  --shadow-card-hover: {{SHADOW_CARD_HOVER}};
  --shadow-button-hover: {{SHADOW_BUTTON_HOVER}};
  --shadow-glow: {{SHADOW_GLOW}};
}
```

---

## 16. Tech Stack

| Layer        | Tool                  |
| ------------ | --------------------- |
| Framework    | {{FRAMEWORK}}         |
| CSS approach | {{CSS_APPROACH}}      |
| Fonts        | {{FONTS}}             |
| Animations   | {{ANIMATION_LIBS}}    |
| Color mode   | {{COLOR_MODE_SYSTEM}} |
| Scroll       | {{SCROLL_LIBS}}       |
| i18n         | {{I18N}}              |

---

## 17. Quick Reference — Design Tokens At A Glance

```
COLORS
  Background:     {{BG_PAGE}}
  Surface:        {{BG_SURFACE}}
  Primary:        {{COLOR_PRIMARY}}
  Primary hover:  {{PRIMARY_HOVER}}
  Primary active: {{PRIMARY_ACTIVE}}
  Text:           {{TEXT_PRIMARY}}
  Text muted:     {{TEXT_SECONDARY}}

TYPOGRAPHY
  Body:           {{TYPE_BODY_SIZE}}/{{TYPE_BODY_LH}}
  Heading:        {{HEADING_DESCRIPTION}}
  Mono:           {{MONO_DESCRIPTION}}
  Hero:           {{TYPE_HERO_DESCRIPTION}}

MOTION
  Fast:           {{DURATION_FAST}}
  Normal:         {{DURATION_NORMAL}}
  Card enter:     {{DURATION_CARD_ENTER}}
  Hero stagger:   {{HERO_STAGGER_DESCRIPTION}}
  Card stagger:   {{CARD_STAGGER_DESCRIPTION}}

LAYOUT
  Container:      max-width {{CONTAINER_MAX}}px, centered
  Card padding:   {{CARD_PADDING}}
  Section gap:    {{SECTION_GAP}}
  Border radius:  {{RADIUS_BUTTONS}} buttons, {{RADIUS_CARDS}} cards

EFFECTS
  Navbar blur:    {{NAVBAR_BLUR}}
  Texture:        {{TEXTURE_DESCRIPTION}}
  Shadow:         {{SHADOW_DESCRIPTION}}
```

---

## References

- [[{{LINKED_NOTE_1}}]]
- [[{{LINKED_NOTE_2}}]]
- [{{EXTERNAL_LINK_TEXT}}]({{EXTERNAL_LINK_URL}})
