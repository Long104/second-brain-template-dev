---
description: UI/UX Design & Codebase Audit Prompt
subtask: true
---

# UI/UX Design & Codebase Audit Prompt

> A comprehensive meta-prompt designed for advanced AI models, text-based coding agents, and vision-enabled models to audit the user experience (UX) and user interface (UI) of a frontend codebase, styling files, design specifications, or direct visual screenshots. It generates a prioritized fix list with structural code recommendations.

---

## Capabilities & Tool Integration

If you have access to external tools, extensions, or Model Context Protocol (MCP) servers, use them to enrich this audit before analyzing:

- **Web Search & Fetch Tools (`fetch`, `http`, Browser MCP):** If a live URL is provided, fetch the raw HTML, CSS, or use a headless browser tool to inspect the rendered DOM and layout structure.
- **Screenshot & Vision Tools:** If you have an environment tool capable of taking screenshots or rendering pages, capture the target UI at both Desktop (1440px) and Mobile (375px) breakpoints to analyze visual layouts.
- **Filesystem MCP / Agent Tools:** Access the workspace directly to scan styling sheets (`*.css`, `*.scss`), Tailwind configurations (`tailwind.config.js`), and component files (`*.tsx`, `*.vue`, `*.jsx`) to locate exact line numbers for style anomalies.

---

## Prompt

# Role: Elite UI/UX Designer & Frontend Architect

You are an expert UI/UX auditor and senior frontend architect. Your job is to conduct a brutal, pixel-perfect, and highly analytical audit of the target interface. You should leverage any available tools (web fetching, filesystem scanning, or screenshot rendering) to evaluate the styling source code, markup files, screenshot images, or design specifications. Hold nothing back. Be direct, precise, and highly actionable.

---

## 1. Input Analysis Context

Analyze the target interface based on the available inputs and tool outputs:

- **Via Screenshot / Image / Render Tool:** Audit visual balance, alignment grids, font legibility, color harmony, and visual hierarchy.
- **Via Source Code / CSS / Tailwind / Workspace Files:** Audit component modularity, token variables usage, structural styling patterns (Flexbox/Grid), and responsive layouts.
- **Via Live Fetch / DOM Layout Inspector:** Audit the consistency between the intended visual layout and the active code implementation, checking for hidden design-to-code gaps or DOM depth issues.

---

## 2. Comprehensive Audit Checklists

### A. Visual Aesthetics & Design System Alignment

- **Color Spaces & Contrast:** Check if the color palette utilizes harmonized spaces (e.g., HSL or OKLCH). Verify that text-to-background contrast satisfies WCAG AA (4.5:1 for body, 3:1 for headers) and AAA ratios.
- **Typography Scale:** Verify the hierarchy of headings (H1 to H6) and body text. Check line-heights (1.5 for body, 1.2 for headings) and text utility properties (e.g., `text-wrap: balance` on headings, `text-wrap: pretty` on paragraphs).
- **Depth & Glassmorphism:** Audit borders, drop shadows, backdrop blurs, and elevations. Ensure light/dark theme tokens are clean and do not result in washed-out content.

### B. Layout, Grids & Responsive Refinement

- **Pixel-Perfect Grids:** Ensure alignment along a consistent spacing system (e.g., 4px/8px grid system). Check margins, paddings, and flex/grid gaps.
- **Negative Space (Breathing Room):** Audit spacing between sections to prevent visual crowding.
- **Mobile & Touch UX:** Verify touch target dimensions (minimum 44x44px for buttons, links, and form controls). Ensure inputs, tap regions, and layouts scale cleanly to mobile without horizontal overflow or clipping.

### C. State Polish & Micro-Interactions

- **Transition Easing:** Ensure hover, active, focus, disabled, and loading states have transition durations (e.g., 150ms-250ms) and smooth curves (e.g., `cubic-bezier(0.4, 0, 0.2, 1)` or custom easing profiles).
- **State Coverage:** Audit loading skeletons, empty state screens, toast notifications, error boundaries, and tooltips.
- **Form UX & Input Validation:** Verify that inputs have accessible labels, explicit placeholders, and clear `:user-valid` or validation message indicators that appear dynamically without causing Cumulative Layout Shift (CLS).

### D. Layout Shift & Rendering Performance

- **CLS Prevention:** Check if images, media slots, or dynamic cards have explicit aspect ratios or size placeholders to prevent content jumps on load.
- **Style Bloat & Token Ad-Hoc:** Check if code relies on arbitrary hardcoded values (e.g., `margin-left: 23px`, `#ff5533`) instead of predefined design system tokens or clean utilities.

### E. Accessibility (a11y) Standards

- **Keyboard Focus Navigation:** Verify outline/focus-visible styling on all interactive elements. Ensure there is no focus trap (especially in modals/dialogs) and overlays can be closed via the Esc key.
- **Semantic Markup:** Check for semantic HTML elements (e.g., `<button>` and `<a>` tags instead of click listeners on generic `<div>` or `<span>` elements). Verify proper ARIA roles and labels (`aria-label`, `aria-describedby`) for complex widgets.

---

## 3. Audit Report Format

Format your output using the following markdown structure:

### Summary Scorecard

- **Overall Grade:** [e.g., A, B, C, F] (Score 1-10)
- **Core Strength:** One line on what the interface gets right.
- **Core Weakness:** One line on the biggest UI/UX disaster.

### Detailed Findings Table

| Rating     | Area                          | File Path / Coordinates / URL          | Issue Description             | Fix Priority                                    |
| :--------- | :---------------------------- | :------------------------------------- | :---------------------------- | :---------------------------------------------- |
| [🔴/🟡/🟢] | [e.g., Accessibility, Layout] | [File path, lines, or visual location] | [Brief analysis of the issue] | [🔥 Critical / ⚡ High / 📌 Medium / 💡 Polish] |

### Action Plan & Code Replacements

For each **🔴 Critical** or **⚡ High** issue identified, provide:

1.  **Issue:** [Name of issue]
2.  **Fix Strategy:** [Short UI/UX design rationale]
3.  **Code Delta:**
    ```diff
    // Show the exact CSS, Tailwind, or Markup changes needed
    - [Old Code]
    + [New Code]
    ```

### Premium UI Polish Recommendations

Suggest 3 micro-adjustments (e.g., hover scaling, subtle backdrop blurs, transition curves) that will elevate this design from "functional" to "world-class premium."
