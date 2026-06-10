---
description: UI Design Prompts
subtask: true
---

# UI Design Prompts

> Prompts for generating UI designs, mockups, and design systems.

---

## Prompt: Component Design

```
Design a {component_name} component.

Context:
- Application type: {web / mobile / desktop}
- Design system: {material / shadcn / custom}
- Target audience: {description}

Requirements:
- {requirement_1}
- {requirement_2}
- Accessible by default (contrast, focus states, screen reader)
- Responsive: mobile → tablet → desktop

Deliver:
- Visual mockup description
- Layout structure (grid, flex)
- Color scheme with hex values
- Typography hierarchy
- Spacing and sizing
- Interaction states: default, hover, active, disabled, focus, error
```

---

## Prompt: Design System Token

```
Define a design token for {token_type}.

Type: {color / spacing / typography / shadow / radius}
Usage: {what it's used for}

Deliver as JSON:
{
  "token_name": "",
  "value": "",
  "description": "",
  "alias_of": "",
  "usage": ""
}
```

---

## Prompt: Page Layout

```
Design a {page_type} page layout.

Purpose: {what the user should accomplish on this page}
User type: {who uses this page}

Content sections:
- {section_1}
- {section_2}
- {section_3}

Constraints:
- Max {n} CTAs per viewport
- Fold: {most_important_content_above_fold}
- Navigation: {sidebar / top nav / none}

Deliver:
- Wireframe description (top to bottom)
- Information hierarchy
- Primary, secondary, tertiary action placement
- Empty state design
- Loading state skeleton
- Error state
```

---

## References

- [[prompt/code/code-generation.md]]
- [[../../design/design-system.md]]
