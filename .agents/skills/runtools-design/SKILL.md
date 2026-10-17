---
name: runtools-design
description: Design, implement, and review Runtools, Therapy Products, and client UI with deliberate references, readable typography, and purposeful layouts. Choose existing components, adapted designs, or custom UI; React Bits and Superdesign are optional resources for landing pages, demos, dashboards, and agent interfaces.
---

# Runtools design

Build interfaces that feel considered, useful, and specific to the business. Choose how expressive to be based on the project: a sales page can be visually ambitious; a dashboard should make everyday work easy. Simple should still feel designed. Expressive should still be usable.

## Start with the actual project

- Read the existing UI, styles, shared components, and the user's references before choosing a direction. Preserve approved work and focus on the requested change.
- Identify the screen's main job, its primary action, and who uses it. Let those determine the layout and visual emphasis.
- For Runtools branding, inspect the current `/software` page and shared design tokens. Its visual language is monochrome. Light mode means white surfaces, dark text, and neutral grays; dark mode means dark surfaces and light text. Select the requested mode explicitly. Do not introduce cream, terracotta, blue, or another accent by assumption.
- For a client product, use that client's brand and context. Do not automatically apply Runtools branding to every business.
- For Therapy Products, preserve the relevant product's brand and established interface patterns. Apply this guidance alongside any product-specific design skill; it does not replace that product's design system.

## Establish a concrete design brief

Before styling a new interface or substantial redesign, establish four choices from the request, existing product, and references:

1. **Reference or direction:** inspect an actual site, screen, or brand. When no reference is provided, choose a specific direction such as editorial, technical, or utilitarian, rather than calling the result modern and clean.
2. **Palette:** use the actual brand or make an explicit color choice for the project. A framework's default palette, a dark purple hero, and a cream/serif/sage combination are all defaults to question, not styles to substitute for each other.
3. **Typography:** choose the face and hierarchy for a reason: the established product identity, readable operational data, or the character of the reference. Reusing a suitable existing face is a valid choice. Do not swap in a fashionable font just to appear less generic.
4. **Layout purpose:** state what someone should understand and do first. Arrange the content around that job instead of automatically producing a centered hero, three equal cards, and a closing CTA.

When the user asks to proceed, make these choices and briefly state them; do not stop for a design questionnaire when the context is sufficient. A background or color change alone does not complete a requested redesign of the page's elements.

## Make the interface readable and remove decorative filler

- Avoid small text as a styling device. For marketing pages and demos, use visible body copy and controls at roughly 18–22px on desktop and at least 16px on mobile, with larger headings that establish a clear hierarchy. Navigation, examples, helper copy, and review controls must remain comfortably readable too.
- Do not add badges, eyebrow labels, decorative pills, tiny captions, or rows of tags to make a layout look finished. If a label conveys no useful information, remove it. Put essential instructions into the main readable copy or the relevant form state.
- Dense product data can follow its established, accessible type scale; this is not a requirement to enlarge every clinical table. Keep the main task, labels, and actions easy to read and use, and preserve a more specific product design system.
- Give forms and buttons deliberate anatomy: clear input boundaries, meaningful grouping, visible focus, understandable action labels, and comfortable hit areas. Avoid styling every element as the same rounded, bordered, shadowed card. Use shared spacing and radius tokens where they make sense, rather than adding arbitrary variety.
- Use SVG icons or real assets where icons are useful. Do not fill feature slots with emoji or decorative symbols. Remove unsupported claims, vague slogans, and filler such as transform, supercharge, and unleash.
- Use motion to explain a transition, show state, or create the chosen atmosphere. Avoid repeated hover scaling, entrance animations on every section, and scrolljacking. A selected animated background can be enough.

These are guardrails for deliberate design, not a new mandatory house style. Gradients, bento layouts, glass surfaces, monochrome, expressive color, and simple layouts can all work when they fit the brief. Do not replace an intentional, approved choice just because it resembles a common pattern.

## Choose the right starting point

Choose between the project's existing design system, a suitable reference design, selected library components, and custom UI. [React Bits](https://reactbits.dev/) and [Superdesign](https://superdesign.dev/) are useful resources, not requirements for every screen. Use them when they help the design; a strong result can use either, both, or neither.

React Bits supplies individual components and effects. Superdesign can provide loose inspiration or a design to adapt directly. Sometimes a close-fitting reference only needs different colors, content, and a few layout or interaction changes. Other projects need an original composition or familiar existing controls. Choose based on fit, rather than trying to demonstrate a particular library or invent something new every time.

### Find React Bits elements by category

When React Bits would help, browse the relevant categories rather than treating it as only a background library. The examples below are discovery suggestions, not a list of components to include in every project. The catalog changes, so check the live site for current examples, props, and source code when selecting a component.

| Category | What to look for | Example components to inspect |
| --- | --- | --- |
| [Text Animations](https://reactbits.dev/c/text-animations) | Headline entrances, changing phrases, animated numbers, text reveals | Split Text, Blur Text, Rotating Text, Count Up |
| [Animations](https://reactbits.dev/c/animations) | Content entrances, transitions, hover treatments, pointer effects | Animated Content, Fade Content, Magnet, Glare Hover |
| [Components](https://reactbits.dev/c/components) | Buttons, navigation, lists, cards, galleries, step-based flows | Specular Button, Pill Nav, Animated List, Spotlight Card, Stepper |
| [Backgrounds](https://reactbits.dev/c/backgrounds) | Atmosphere behind a hero, demo, or selected section | Gradient ASCII, Topography, Dot Grid, Silk |
| [Micro Interactions](https://reactbits.dev/c/micro) | Small interactive moments on controls and objects | Flying Button, Flip Card, Branched Menu |

**Buttons and CTAs:** when a button needs a distinctive treatment, check Components and Micro Interactions for button designs, and Animations for treatments that wrap an existing button. The library's categories overlap with UI needs. An ordinary button with a restrained hover or press state is often the better choice. Keep ordinary form actions and destructive actions predictable.

**Text:** match the effect to the message. A short changing industry phrase can use a rotating treatment; a long description should stay still and readable. Do not animate every heading or make users wait for essential text.

**Backgrounds:** a plain background is a valid choice. If an effect fits the project, inspect its real demo before choosing. Tune its palette, light/dark mode, scale, density, and motion for the page. Keep content legible through the component's settings and foreground layout. Do not automatically add a fade, vignette, or dimming overlay that changes the reference.

**Navigation, cards, and lists:** choose a component because it improves browsing or comprehension. Preserve familiar navigation, selection, scrolling, and keyboard behavior in operational software.

### Use Superdesign for inspiration or an adapted design

Browse [Superdesign's library](https://superdesign.dev/library), or use available connected design-search tools, when the overall direction needs work. Search for the actual surface and mood: a service-business intake page, a restrained operations dashboard, an editorial landing page, or a client portal.

Use a reference in the way that best fits the project:

- **Inspiration:** borrow useful ideas about hierarchy, spacing, typography, content density, navigation, or interaction, then build a composition for the actual product.
- **Adapted design:** when a design already fits, use it as the starting point and keep the parts that work. Adapt reusable source or templates when available. Change colors to the brand palette, replace the content and imagery, and adjust the sections, density, or controls that need to serve this product. Small, deliberate changes can be enough; a complete redesign is not automatically better.

Do not force React Bits effects into a reference that works without them. Replace irrelevant placeholder content and preserve any required source credits or license notices. If a source is inaccessible, state that briefly and work from accessible references.

## Choose the right amount of visual treatment

- Give a page a clear visual idea. A distinctive background, typographic treatment, or interactive element can carry the design without competing effects everywhere.
- On marketing pages and demos, use expressive elements where they help explain or sell the product. Keep the primary action obvious.
- In dashboards and agent workspaces, favor readable information, clear states, and efficient controls. Put richer visuals in an overview, onboarding moment, or purposeful interaction when they earn the space.
- Write concrete copy about the business and the work. Avoid filler slogans, decorative badges, repetitive labels, and tiny text added just to make the page look busy. Keep labels that help people understand data or controls.
- Remove filler while preserving the explanation, examples, and workflow needed to understand the product. Minimal design should not leave the pitch or interface incomplete.

## Implement the chosen design faithfully

- When the user chooses a named React Bits component, use its real implementation as the starting point. Inspect its demo, documented options, dependencies, and [installation instructions](https://reactbits.dev/get-started/installation). Do not approximate the effect and present it as the original.
- When adding a library component, choose the source variant that matches the repository: TypeScript or JavaScript, CSS or Tailwind. Keep required license notices and add only the dependencies the selected component needs.
- Adapt colors, typography, spacing, radii, and interaction settings to the project's design system. Do not copy unrelated demo scaffolding into the product.
- Keep decorative effects separate from application behavior. Forms, uploads, navigation, data loading, and approvals must continue to work.
- Keep essential content available without animation. Respect reduced-motion preferences, provide a static fallback for GPU effects, and pause expensive work when hidden or offscreen. Decorative layers must not intercept input.
- Treat real product screenshots, illustrations, and company materials as assets with a purpose. Do not add a mascot or stock illustration just to fill empty space.

## Review in the real interface

Use the project's local development server or existing preview so the user can see changes as they happen. During local design exploration, keep edits local unless the user asks to publish.

Inspect the rendered result at desktop and mobile sizes. Check text contrast, hierarchy, layout overflow, the primary action, and any interaction affected by the change. Check focus and touch behavior for interactive components, and reduced-motion behavior when adding animation. Run the checks appropriate to the code change.

For an existing interface, inspect both the source and the rendered result. Look for untouched library defaults, unchosen accents or fonts, repeated gradient text, uniform card styling, gratuitous glow or motion, decorative microcopy, weak hierarchy, inconsistent edges, and overflow. Treat these as findings to assess against the actual brief, not an automatic ban list. Prioritize usability and readability over cosmetic tells. When an audit is requested, give concrete findings with file/line, impact, and a proposed fix; distinguish intentional choices from defects. Do not invent statistical weights or a scientific-looking design score, and do not add a scanner or CI gate unless requested.

When the user is exploring a specific part, such as the background, iterate on that part before expanding into a full redesign. Carry their accepted choices forward.

Show the result with a screenshot and the local or preview URL. If external components or references were used, briefly identify them, link their official sources, and describe the meaningful adaptations. Do not claim a component, integration, or workflow works until it has been verified.
