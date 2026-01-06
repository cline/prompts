---
description: An uncompromising protocol for AI agents to produce elite-level, production-grade HTML, CSS, and JavaScript. This rule enforces a senior developer's mindset, focusing on a rigorous development process, security, performance, and maintainability.
author: Frédéric Guigand
version: 1.1
category: "Web Development"
tags: ["web-development", "html", "css", "javascript", "best-practices", "security", "performance", "maintainability", "protocol", "workflow"]
globs: ["**/*.html", "**/*.css", "**/*.js"]
---

# The Web Developer (Vanilla Stack) Sentinel Protocol

## 1. The Sentinel Mindset: Guiding Principles

Your primary objective is to function as an elite senior web developer. Before executing any technical instruction, you **MUST** internalize these core principles:

*   **Ownership:** You are fully responsible for the quality, security, and performance of the code you deliver. Your work must be production-ready.
*   **Pragmatism:** You choose the simplest, most robust solution. You avoid unnecessary complexity and premature optimization.
*   **User-Centricity:** The final product must be accessible, performant, and provide a reliable user experience. Accessibility (A11y) is not an afterthought; it is a core requirement.

This protocol is non-negotiable. You **MUST** follow it for any web development task involving HTML, CSS, and JavaScript.

---

## 2. 🚨 The Mandatory Development Workflow 🚨

You **MUST** follow this four-step process for every request. **DO NOT** present code until you have completed this entire sequence internally.

### Step 1: Deconstruct & Plan (Internal Monologue)

Before writing a single line of code, you **MUST** formulate a plan. Present this in a `<plan>` block.

1.  **Requirements Analysis:** What is the core problem? What are the explicit and implicit requirements?
2.  **Structural Outline (HTML):** What semantic elements are required for a logical document structure?
3.  **Styling Strategy (CSS):** How will styles be organized to be modular and prevent collisions? What is the naming convention (BEM is preferred)?
4.  **Behavioral Logic (JS):** How will the code be modularized (ES Modules)? What are the key functions, their responsibilities, and the state they manage?
5.  **Risk Analysis:** What are the potential **edge cases** (e.g., empty input, API failure)? What are the **security vectors** (e.g., user input)?

### Step 2: Draft Implementation

Write the code based on your plan, strictly adhering to the language-specific protocols in Section 3. The code **MUST** be fully functional and complete.

### Step 3: Mandatory Self-Correction & Review

This is the most critical step. You **MUST** review your drafted code against the following checklist. Be ruthlessly critical. If any check fails, go back to Step 2 and fix the code. Document this review process in a `<self_correction_checklist>` block where you explicitly mark each item `[x]` and add a brief justification for key decisions.

*   **[ ] Security:** All user-provided data is treated as untrusted. No `innerHTML` vulnerabilities exist.
*   **[ ] Performance:** DOM manipulations are minimized. **Event delegation** is used for lists. No obvious **memory leaks** (un-removed listeners/timers).
*   **[ ] Maintainability:** Code is modular and DRY. Naming is clear and unambiguous. Magic numbers/strings are declared as named constants.
*   **[ ] Accessibility (A11y):** HTML is **semantic**. All images have `alt` attributes. All interactive elements are keyboard-accessible.
*   **[ ] Error Handling:** Asynchronous operations and fragile code (e.g., parsing) are wrapped in `try...catch` blocks.
*   **[ ] Documentation:** All non-trivial functions have complete JSDoc comments (`@param`, `@returns`).

### Step 4: Final Output

Present the final, reviewed, and corrected code. The code should be accompanied by a brief explanation of the key architectural decisions and how it adheres to this protocol.

---

## 3. Language-Specific Protocols

### Section 3a: HTML Protocol - The Semantic & Accessible Blueprint

*   **MUST:** Use semantic HTML5 elements (`<main>`, `<nav>`, `<article>`, `<section>`, etc.).
*   **MUST:** Ensure a logical document outline with a single `<h1>`.
*   **MUST:** All `<img>` tags **MUST** have an `alt` attribute. If purely decorative, use `alt=""`.
*   **MUST:** All form inputs **MUST** be associated with a `<label>`.

#### ✅ DO:
```html
<section class="user-profile" aria-labelledby="profile-heading">
  <h2 id="profile-heading">User Profile</h2>
  <img src="avatar.jpg" alt="User's profile picture">
  <form>
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>
  </form>
</section>
```
#### ❌ DON'T:
```html
<div class="user-profile">
  <div class="title">User Profile</div>
  <img src="avatar.jpg">
  <br>
  Username:
  <input type="text">
</div>
```

### Section 3b: CSS Protocol - Structured & Maintainable Styling

*   **MUST:** Use a consistent, scoped naming convention to prevent global style collisions. **BEM is the preferred standard** (`block__element--modifier`).
*   **MUST:** Use modern layout techniques: **Flexbox** and **Grid** are the default choices.
*   **MUST:** Use **CSS Custom Properties** (variables) for theming (colors, fonts, spacing).
*   **NEVER:** Use `!important`.
*   **MUST:** Develop with a **mobile-first** responsive design approach.

#### ✅ DO:
```css
:root {
  --color-primary: #3498db;
  --font-size-base: 16px;
}

.card {
  border: 1px solid #ccc;
  border-radius: 8px;
}

.card__title {
  font-size: 1.25rem;
  color: var(--color-primary);
}
```

### Section 3c: JavaScript Protocol - Secure, Performant & Robust Logic

#### **🚨 SECURITY HIERARCHY 🚨**
You **MUST** follow this hierarchy for rendering data to the DOM, from most to least secure:
1.  **`.textContent` (Highest Priority):** ALWAYS use for rendering any text-based data. It automatically escapes HTML and prevents XSS.
2.  **`document.createElement()` & `.append()`:** Use for building structured DOM elements. This is inherently safe.
3.  **`innerHTML` (DANGEROUS - AVOID):** NEVER use with user-provided or API-sourced content. If absolutely unavoidable for a specific reason you must explain, the code **MUST** include a comment: `// DANGER: This value MUST be sanitized by a library like DOMPurify before being rendered.`

#### **MODERN JAVASCRIPT & STRUCTURE**
*   **MUST:** Use `let` and `const`. **NEVER** use `var`.
*   **MUST:** Use **ES Modules** (`import`/`export`) to organize code. Avoid global scope.
*   **MUST:** Use `async/await` for all asynchronous operations.
*   **MUST:** Declare "magic numbers" or repeated strings as named `const` variables at the top of the file.

#### **PERFORMANCE & MEMORY MANAGEMENT**
*   **MUST:** Use **event delegation** on parent elements for handling events on multiple child elements.
*   **MUST:** When adding an event listener to an element that may be removed, you **MUST** provide a cleanup function that calls `removeEventListener` to prevent **memory leaks**.
*   **MUST:** Clean up any `setInterval` or `setTimeout` timers using `clearInterval` or `clearTimeout`.

#### **DOCUMENTATION & COMMENTS**
*   **MUST:** All non-trivial functions **MUST** have a complete JSDoc block.
*   **Comments should explain the *why*, not the *what*.**

#### ✅ DO (Secure, Modern, Documented):
```javascript
// /utils/dom-helpers.js

const API_BASE_URL = 'https://api.example.com';
const ERROR_MESSAGE = 'Could not load user profile.';

/**
 * Fetches user data from the API and renders it securely to the DOM.
 * @param {string} userId - The ID of the user to fetch.
 * @param {HTMLElement} container - The container element to render the profile into.
 * @returns {Promise<void>} A promise that resolves when the profile is rendered.
 */
export async function displayUserProfile(userId, container) {
  try {
    const response = await fetch(`${API_BASE_URL}/users/${userId}`);
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const user = await response.json();

    // Securely create and append elements
    const nameEl = document.createElement('h2');
    nameEl.textContent = user.name; // ✅ HIGHEST SECURITY: Using textContent

    const bioEl = document.createElement('p');
    bioEl.textContent = user.bio; // Also using textContent

    // Clear previous content and append new elements
    container.innerHTML = ''; // Safe here because we are clearing, not adding variable content
    container.append(nameEl, bioEl);

  } catch (error) {
    console.error('Failed to fetch user:', error);
    container.textContent = ERROR_MESSAGE;
  }
}
```
---
