---
description: Provides guidelines and best practices for creating and working with Slidev presentation projects.
author: https://github.com/nickbaumann98
version: 1.0
category: "Presentation Tools"
tags: ["slidev", "slides", "markdown", "vue", "vite", "guide"]
globs: ["slides.md", "**/slides.md", "*.vue", "layouts/**/*.vue", "components/**/*.vue"]
---
# Slidev Project Instructions

This document provides guidelines for working with Slidev projects. Slidev is a Markdown-based presentation tool powered by Vue and Vite.

## Core Concepts & Structure

1. **Entry Point**: The main presentation content is typically in `http://slides.md`.
2. **Slide Separation**: Slides are separated by `---` on a new line.
3. **Frontmatter/Headmatter**:
* YAML blocks at the beginning of the file (`--- ... ---`) configure the deck (headmatter) or individual slides (frontmatter).
* Headmatter (first block) applies globally (e.g., `theme`, `title`, `addons`).
* Frontmatter configures specific slides (e.g., `layout`, `background`, `class`, `transition`, `clicks`).
* **YAML Quoting:** Prefer double quotes (`"..."`) for strings containing single quotes (`'`) to avoid parsing errors (e.g., `title: "My Deck's Title"`).
4. **Layouts**:
* Define the structure of slides. Specified via `layout:` in frontmatter.
* Default layout for the first slide is `cover`, others are `default`.
* Custom layouts are placed in the `layouts/` directory as `.vue` files. Use `<slot />` for default content and named slots (`<slot name="xxx" />`) for specific sections.
5. **Components**:
* Vue components can be used directly in Markdown (e.g., `<MyComponent />`).
* Components are auto-imported from:
* Slidev built-ins (`@slidev/client/builtin/`).
* The active theme.
* Installed addons.
* The local `components/` directory.
* Custom components go in the `components/` directory as `.vue` files.
6. **Styles**:
* [UnoCSS](https://unocss.dev) is built-in for utility-first styling. Apply classes directly in Markdown or components.
* Global styles can be added in the `styles/` directory (e.g., `styles/index.css`).
* Scoped styles for a specific slide can be added using `<style scoped>...</style>` within the slide's Markdown.
7. **Assets**:
* Static assets (images, videos) can be placed in the `public/` directory and referenced with absolute paths starting with `/` (e.g., `background: /my-image.png`).
* Relative paths (e.g., `./image.png`) work for standard Markdown image syntax (`![alt](./image.png)`) but might break in frontmatter or components after building. Prefer the `public/` directory method for reliability.
8. **Notes**:
* Presenter notes are added as HTML comments (`<!-- ... -->`) at the *very end* of a slide's Markdown content.
* Notes support Markdown formatting.

## Key Features & Syntax

1. **Code Blocks**:
* Use standard Markdown fenced code blocks (e.g., ` ```ts ... ``` `).
* Syntax highlighting is provided by Shiki.
* Supports line highlighting (`{1,3-5}`), line numbers (`{lines:true}`), Monaco editor (`{monaco}`), diffs (`{monaco-diff}`), code imports (`<<< @/path/to/file.js#region {lines=...}`). Refer to the Syntax Guide for details.
2. **Animations (Clicks)**:
* Use `<v-click>` component or `v-click` directive to reveal elements step-by-step.
* `v-after` reveals elements simultaneously with the previous `v-click`.
* `.hide` modifier (e.g., `v-click.hide`) hides elements instead of showing them.
* `<v-clicks>` component applies `v-click` to its children (useful for lists).
* Control timing with `at="..."` (e.g., `v-click="3"` for absolute click 3, `v-click="'+2'"` for 2 clicks after the previous relative element).
* Specify enter/leave ranges: `v-click="[2, 5]"` (visible from click 2 up to, but not including, 5).
* Override total clicks per slide with `clicks: N` in frontmatter.
3. **Motion (VueUse Motion)**:
* Use the `v-motion` directive for element transitions (e.g., `:initial="{ x: -80 }" :enter="{ x: 0 }"`).
* Can be triggered by clicks using `:click-N` attributes (e.g., `:click-1="{ y: 30 }"`).
4. **Slide Transitions**:
* Set in headmatter (`transition: slide-left`) for global effect or frontmatter for specific slides.
* Built-in transitions: `fade`, `fade-out`, `slide-left`, `slide-right`, `slide-up`, `slide-down`, `view-transition`.
* Specify different forward/backward transitions: `transition: slide-left | slide-right`.
5. **Diagrams**: Supports Mermaid (` ```mermaid ... ``` `) and PlantUML (` ```plantuml ... ``` `).
6. **LaTeX**: Use `$` for inline math (`$a^2+b^2=c^2$`) and `$$` for block math.
7. **Global Context**: Access runtime info like `$nav` (navigation controls), `$clicks` (current click count), `$page` (current slide number), `$frontmatter`, `$slidev.configs` within components or directly in Markdown using `{{ }}`. Use composables like `useNav()` from `@slidev/client` in `<script setup>`.

## Development Workflow

1. **Initialization (Full Project)**: Use `pnpm create slidev <project-name>` (or npm/yarn/bun equivalent).
2. **Development Server (Full Project)**: Run `pnpm dev` (or `npm run dev`, etc.) in the project directory. Access at `http://localhost:3030`.
3. **Development Server (Single File)**: Navigate to the directory containing your `slides.md` and run `npx @slidev/cli`. This is useful for quick previews without a full project setup.
    * **Note:** Ensure you use the correct package name: `@slidev/cli`.
    * **Theme Installation:** If a theme specified in the frontmatter (e.g., `theme: seriph`) isn't installed, Slidev will prompt you to install it. Confirm by pressing 'y' and choosing your package manager (e.g., 'npm').
4. **Editing**: Modify `slides.md` and add custom components/layouts/styles as needed.
4. **Exporting**:
* Install `playwright-chromium` (`pnpm add -D playwright-chromium`).
* Run `pnpm export` (or `npm run export`, etc.) to generate a PDF (`slides-export.pdf` by default).
* Use `--format png` or `--format pptx`.
* Use `--with-clicks` to export each click step as a separate page/image.
* Use `--output <filename>` to specify the output file.
* Use `--dark` for dark mode export.
5. **Building for Hosting**:
* Run `pnpm build` (or `npm run build`, etc.) to create a static SPA in the `dist/` folder.
* Use `--base /path/` if deploying to a subpath.
* Deploy the `dist` folder to static hosting (Netlify, Vercel, GitHub Pages). Configuration files (`netlify.toml`, `vercel.json`, GitHub Actions workflow) are often included in the starter template.

## Best Practices

* Keep `http://slides.md` focused on content.
* Use layouts for consistent slide structure.
* Use components for reusable UI elements and interactivity.
* Leverage themes and addons for styling and features before building custom solutions.
* Use the `public/` directory for static assets referenced in frontmatter or components.
* Utilize presenter mode (`/presenter` route or button) for notes and controls during presentation.
* Pay attention to terminal output for errors (e.g., YAML parsing issues) when starting the server.
