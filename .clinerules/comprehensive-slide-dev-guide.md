---
description: A comprehensive guide to crafting high-quality advanced presentations using Slidev, covering advanced syntax, visuals, interactivity, customization, and deployment.
author: Cline
version: 1.0
category: "Presentation Tools"
tags: ["slidev", "guide", "advanced", "presentation", "development"]
globs: ["comprehensive-slide-dev-guide.md"]
---

# Comprehensive Slidev Guide: Crafting High-Quality Advanced Presentations

This guide provides a dense overview of Slidev's capabilities, focusing on advanced techniques and best practices for creating visually stunning and highly interactive presentations. It assumes a basic understanding of Markdown and Vue.js.

## 1. Core Structure and Advanced Syntax

Slidev presentations are built upon Markdown files, enhanced with YAML frontmatter for configuration and Vue components for dynamic content.

### Slide Separation and Frontmatter

Separate slides with `---`. The first `---` block is the headmatter (global config), subsequent blocks are slide-specific frontmatter.

```yaml
---
theme: seriph # Global theme
title: Advanced Slidev Techniques
canvasWidth: 1200 # Custom canvas width
aspectRatio: 16/9 # Widescreen aspect ratio
fonts:
  sans: Roboto
  mono: 'Fira Code, monospace'
  provider: google # Use Google Fonts
---
# Welcome Slide

<!-- This is a presenter note -->

---
layout: cover # Use the cover layout
background: /images/background.png # Slide background image
class: text-white # Apply UnoCSS classes
---
# Section Title

::right::
Content for the right slot

---
src: ./sections/advanced-animations.md # Import slides from another file
---
```

**Advanced Frontmatter Options:**
- `clicks`: Manually set the total number of clicks for a slide.
- `routeAlias`: Define a custom route name for a slide for easier navigation (`<Link to="my-alias">`).
- `hideInToc`: Exclude a slide from the Table of Contents.
- `download`: Include a download button for the PDF export in the built SPA. Can be boolean (`true`) or a custom URL string.
- `monacoTypesAdditionalPackages`: Array of strings to specify extra packages for Monaco Editor type acquisition.
- `monacoTypesSource: ata`: Enable client-side auto type acquisition for Monaco.
- `drawings.persist`: Boolean (`true`/`false`) or `'dev'` to control drawing persistence.
- `transition`: Define per-slide transitions (`fade`, `slide-left`, `view-transition`, custom CSS transitions). Use `|` for forward/backward transitions (`slide-left | slide-right`). Can also be an object for advanced Vue Transition options.
- `title`: Set the title for a slide, overriding the title extracted from the first heading.
- `level`: Set the title level for a slide, affecting its appearance in the Table of Contents.
- `class`: Add custom CSS classes to the slide container.
- `style`: Add inline CSS styles to the slide container.
- `id`: Set a custom ID for the slide container.
- `name`: Set a custom name for the slide, usable with `<Link to="name">`.
- `plantUmlServer`: Configure a custom PlantUML server URL.
- `htmlAttrs`: Add attributes to the `<html>` tag for a specific slide.
- `bodyAttrs`: Add attributes to the `<body>` tag for a specific slide.
- `head`: Add custom tags to the `<head>` section for a specific slide (array of objects).
- `vue`: Configure Vue plugin options for a specific slide.
- `markdown`: Configure Markdown-it options for a specific slide.
- `highlighter`: Configure Shiki highlighter options for a specific slide.
- `katex`: Configure KaTeX options for a specific slide.
- `monaco`: Configure Monaco Editor options for a specific slide.
- `shortcuts`: Configure keyboard shortcuts for a specific slide.
- `transformers`: Configure markdown transformers for a specific slide.
- `codeRunners`: Configure code runners for a specific slide.
- `clicks`: Manually set the total number of clicks for a slide.
- `routeAlias`: Define a custom route name for a slide for easier navigation (`<Link to="my-alias">`).
- `hideInToc`: Exclude a slide from the Table of Contents.
- `download`: Include a download button for the PDF export in the built SPA. Can be boolean or a custom URL.
- `monacoTypesAdditionalPackages`: Specify extra packages for Monaco Editor type acquisition.
- `monacoTypesSource: ata`: Enable client-side auto type acquisition for Monaco.
- `drawings.persist: true`: Save drawings as SVGs. Can also be set to `false` or `dev` to disable.
- `plantUmlServer`: Configure a custom PlantUML server URL.
- `htmlAttrs`: Add attributes to the `<html>` tag for a specific slide.
- `bodyAttrs`: Add attributes to the `<body>` tag for a specific slide.
- `head`: Add custom tags to the `<head>` section for a specific slide.

### Notes and Click Markers

Add presenter notes using HTML comments `<!-- ... -->` at the end of a slide. Use `[click]` markers within notes to synchronize notes with click animations. `[click:N]` skips N-1 clicks.

```markdown
<!--
Introduction to the topic

[click] First key point

[click:3] Third key point, skipping the second click

[click:+2] Another point, 2 clicks after the previous marker
-->
```

**Advanced Click Markers:**
- Use `[click]` at the beginning of a line in notes to synchronize with the next click animation on the slide.
- Use `[click:N]` to synchronize with a specific absolute click number N.
- Use `[click:+N]` to synchronize N clicks after the previous click marker.
- Content between click markers is highlighted in the presenter notes.
- Click markers help in navigating notes during the presentation, especially with the presenter mode.

### Importing Slides

Organize large presentations by splitting content into multiple Markdown files and importing them using the `src` frontmatter option.

```yaml
---
src: ./chapters/chapter1.md # Import entire file
---

---
src: ./appendix.md#2-5,8 # Import specific slides (2, 3, 4, 5, and 8)
---
```

Frontmatter from the main entry has higher priority during merging. This allows overriding configurations from imported files.

## 2. Mastering Visuals and Styling

Create visually appealing slides using themes, custom styles, fonts, and assets.

### Themes and Customization

Apply a theme via the `theme` headmatter option. Explore the [Theme Gallery](https://sli.dev/resources/theme-gallery). Eject a theme (`slidev theme eject`) for deep customization.

**Writing Themes:** Themes are npm packages (`slidev-theme-*`) that can provide styles, layouts, components, and default configurations (`package.json` `slidev.defaults`). Themes should focus on appearance.

### Styling with UnoCSS

Slidev integrates UnoCSS for utility-first styling. Apply classes directly in Markdown or components.

```html
<div class="text-center text-primary font-bold">Centered Bold Primary Text</div>
```

**Customizing UnoCSS:** Create `uno.config.ts` in your project root to extend configurations, add shortcuts, custom rules, variants, etc.

```ts
import { defineConfig } from 'unocss'
export default defineConfig({
  shortcuts: {
    'btn': 'px-4 py-2 rounded inline-block bg-teal-600 text-white cursor-pointer hover:bg-teal-700 disabled:cursor-default disabled:bg-gray-600 disabled:opacity-50',
  },
  rules: [
    [/^my-rule-(\d+)$/, ([, d]) => ({
      margin: `${d / 4}rem`,
    })],
  ],
  variants: [
    (matcher) => {
      if (!matcher.startsWith('hover:'))
        return matcher
      return {
        matcher: matcher.slice(6),
        selector: (s) => `${s}:hover`,
      }
    },
  ],
})
```

**Scoped Styles:** Use `<style scoped>` in Markdown for slide-specific CSS. This is useful for isolated styling that doesn't affect other slides.

### Fonts and Typography

Configure fonts via the `fonts` headmatter option. Slidev automatically imports from Google Fonts by default.

```yaml
---
fonts:
  sans: 'Open Sans'
  serif: 'Georgia'
  mono: 'JetBrains Mono'
  weights: '300,400,700' # Specify weights
  italic: true # Include italics
  local: 'My Local Font' # Mark as local
  fallbacks: false # Disable default fallbacks
  provider: coollabs # Use a different provider
---
```

For fine-grained control or local fonts, use `@font-face` in custom styles (`styles/index.css`). You can also inject font links directly into `index.html`.

### Assets and Backgrounds

Place static assets in the `public/` directory and reference with absolute paths (`/image.png`). Use the `background` frontmatter option for slide backgrounds.

```yaml
---
background: /images/slide-bg.jpg
---
```

For dynamic backgrounds or more complex asset handling, use Vue components and bind the `src` attribute to data or computed properties. Use the `vite-plugin-remote-assets` for bundling remote assets.

## 3. Creating Engaging and Interactive Content

Leverage Slidev's features for animations, interactivity, and rich content types.

### Advanced Animations

**Click Animations:** Control element visibility step-by-step.
- `<v-click>` / `v-click`: Reveal on next click.
- `v-after`: Reveal with the previous `v-click`.
- `.hide`: Hide instead of show (`v-click.hide`).
- `<v-clicks>`: Apply `v-click` to children (great for lists).
- `at`: Control click timing (`v-click="3"` for absolute click 3, `v-click="'+2'"` for 2 clicks after the previous relative element).
- Enter/Leave ranges: `v-click="[2, 5]"` (visible from click 2 up to, but not including, 5).
- Custom transitions for clicked elements using CSS classes `.slidev-vclick-target` and `.slidev-vclick-hidden`. Override default opacity transition with CSS.

**Motion:** Use `v-motion` directive for element transitions powered by `@vueuse/motion`. Trigger with clicks using `:click-N` variants. Combine with `v-click` for complex animation sequences.

```html
<div v-motion :initial="{ x: -100 }" :enter="{ x: 0 }" :click-1="{ y: 50 }" :click-2-4="{ opacity: 0.5 }">Animated Element</div>
```

**Slide Transitions:** Apply transitions between slides using the `transition` frontmatter option. Customize with CSS transitions using Vue's transition classes (`.my-transition-enter-active`, etc.). Use navigation direction variants (`.slidev-nav-go-forward`, `forward:`, `backward:`) for direction-specific effects. Explore the experimental View Transitions API (`transition: view-transition`).

### Interactive Code Blocks

Slidev's code block features are powerful for technical talks.
- **Line Highlighting:** `{2,4-6}` highlights lines 2 and 4 through 6. Use `|` for dynamic highlighting with clicks (`{1|3|all}`).
- **Monaco Editor:** `{monaco}` turns a code block into a live editor. Configure editor options globally in `./setup/monaco.ts` or per-block with `{editorOptions: {...}}`. `{monaco-diff}` creates a diff view (`~~~` separates original/modified).
- **Monaco Runner:** `{monaco-run}` adds a run button to execute code (JS/TS by default). Configure custom runners for other languages in `./setup/code-runners.ts`. Use `{autorun:false}` to disable automatic execution. Use `{showOutputAt:'+1'}` to control output visibility with clicks.
- **Writable Monaco Editor:** `<<< @/path/to/file {monaco-write}` links the editor to a file for live editing and saving (use with caution and backups!).
- **TwoSlash:** ````ts twoslash```` renders TypeScript code with type info on hover or inlined. Useful for explaining types and code behavior.
- **Import Snippets:** `<<< @/path/to/snippet.js#region-name {lines:true}` imports code from files. Use `@` for project root. Combine with line highlighting and Monaco features.

### Rich Content Types

- **LaTeX:** `$inline$` and `$$block$$` for mathematical formulas (powered by KaTeX). Configure KaTeX options in `./setup/katex.ts`. Enable chemical equations by importing `katex/contrib/mhchem` in `vite.config.ts`.
- **Diagrams:** ```mermaid``` and ```plantuml``` code blocks for generating diagrams from text. Configure PlantUML server URL in headmatter.
- **Icons:** Use `<collection-name>-<icon-name>` syntax after installing `@iconify-json/*` packages. Style with CSS classes. Explore [Icônes](https://icones.js.org/) for available collections.
- **MDC Syntax:** Enable with `mdc: true` in frontmatter for enhanced Markdown with components and styles (`:inline-component{prop="value"}`, `::block-component{prop="value"}::`). Useful for applying styles or using components inline within markdown text.
- **Built-in Components:** Utilize components like `<Toc>` for table of contents, `<Tweet>` for embedding tweets, `<Youtube>` and `<SlidevVideo>` for videos, `<LightOrDark>` for theme-specific content, `<RenderWhen>` for context-specific rendering, `<Link>` for internal navigation, `<Transform>` for scaling elements, etc. Explore the [Built-in Components](https://sli.dev/builtin/components) documentation for full details and props.

## 4. Advanced Customization and Extensibility

Go beyond basic configuration by customizing the Slidev application and adding custom features.

### Directory Structure for Customization

Organize custom code in specific directories:
- `components/`: Custom Vue components (auto-imported).
- `layouts/`: Custom Vue layouts.
- `public/`: Static assets (served at `/`).
- `styles/`: Global CSS/JS styles (`index.css` or `styles/index.ts`).
- `setup/`: Custom setup files for advanced configurations:
    - `main.ts`: Extend Vue application.
    - `vite-plugins.ts`: Add custom Vite plugins based on slide data.
    - `shiki.ts`: Configure Shiki highlighter.
    - `routes.ts`: Add custom pages/routes.
    - `katex.ts`: Configure KaTeX.
    - `monaco.ts`: Configure Monaco Editor.
    - `shortcuts.ts`: Configure keyboard shortcuts.
    - `transformers.ts`: Define custom markdown transformers.
    - `code-runners.ts`: Define custom code runners for Monaco.
- `snippets/`: Code snippets for importing.
- `index.html`: Inject content into the main HTML file (`<head>` and `<body>` injections).
- `vite.config.ts`: Extend Vite configuration (merged with Slidev's config).

### Configuring the Application

- **Vite:** Extend Vite config in `vite.config.ts`. Configure internal plugins via `slidev` field. Add custom plugins based on slide data in `./setup/vite-plugins.ts` using `defineVitePluginsSetup`.
- **Vue App:** Extend the Vue application instance in `./setup/main.ts` using `defineAppSetup` to add plugins, global components, or perform initializations.
- **Routes:** Add custom pages to the presentation build by configuring routes in `./setup/routes.ts` using `defineRoutesSetup`. Useful for adding landing pages, appendixes, or interactive demos outside the main slide flow.

### Extending Functionality with Addons

Addons are npm packages (`slidev-addon-*`) that extend Slidev's features. Use them via the `addons` headmatter option. Explore the [Addon Gallery](https://sli.dev/resources/addon-gallery). Write your own addons using the same directory structure and setup files as a Slidev project to share reusable components, layouts, or configurations.

## 5. Building and Hosting High-Quality Outputs

Prepare your presentation for sharing and deployment.

### Building as a SPA

Build your slides into a static SPA using `slidev build`. Configure the base path (`--base`) for subpath deployment and output directory (`--out`). Build multiple decks at once by providing multiple markdown files.

### Exporting to Various Formats

Export to PDF, PPTX, PNG, or Markdown using `slidev export`. Install `playwright-chromium`. Use options like `--with-clicks` to export each click step, `--range` to export specific slides, `--dark` for dark mode export, `--timeout` and `--wait` for handling complex slides, `--executable-path` for specifying a browser executable, `--with-toc` for PDF outline, and `--omit-background` for transparent PNGs. Troubleshoot missing content (increase `--wait`) or broken emojis (install fonts).

**Browser Exporter:** Use the built-in UI at `/export` for interactive exporting with a live preview.

### Hosting

Deploy the built SPA (`dist` folder) to static hosting services like GitHub Pages, Netlify, or Vercel. Configuration files (`netlify.toml`, `vercel.json`, GitHub Actions workflow) are often included in starter templates. Host on Docker using provided images or by building your own Dockerfile.

## Conclusion: Crafting Your Masterpiece

Slidev provides a flexible and powerful platform for creating advanced, high-quality presentations. By mastering its syntax, leveraging its features for interactivity and visual appeal, and exploring its customization options, you can create presentations that are not only informative but also engaging and memorable. Focus on clear content, thoughtful design, and strategic use of interactive elements to make your Slidev presentations truly stand out. Utilize the advanced features like custom layouts, components, animations, code blocks, and customization options to tailor your presentation to your specific needs and audience. Remember to organize your project well and leverage the power of themes and addons for reusability and enhanced functionality.
