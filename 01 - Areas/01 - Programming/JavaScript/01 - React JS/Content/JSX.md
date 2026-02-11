---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - React_JS
note type: Informational Note
---
JSX is a powerful tool in React that simplifies the process of writing UI components by combining markup and logic in a single place. By following its rules (single root element, closing tags, camelCase attributes), developers can create clean, maintainable, and dynamic components. The examples above demonstrate how JSX is applied in real-world scenarios, from static markup to interactive and dynamic UI elements. If you’d like more examples or help with a specific JSX use case, let me know!

**Why JSX in React?**
Historically, web development separated HTML, CSS, and JavaScript into different files. However, as web applications became more interactive, JavaScript increasingly controlled the HTML content.
In React, JSX allows developers to write both the rendering logic and markup together in a single component, ensuring consistency and reducing errors during updates.

**JSX vs. HTML**
JSX looks similar to HTML but is stricter and has specific rules:

**Single Root Element**: A component must return a single element (or a Fragment `<>` to avoid extra DOM nodes).

**Close All Tags**: All tags must be explicitly closed (e.g., for self-closing tags, 
`text` for wrapping tags).

**camelCase Attributes**: HTML attributes like `class` become `className` in JSX (to avoid JavaScript reserved words), and attributes like `stroke-width` become `strokeWidth`. Exceptions are `aria-*` and `data-*` attributes, which retain dashes.
JSX is transformed into JavaScript objects under the hood, which is why these rules are necessary.

**Converting HTML to JSX**
The article provides an example of converting HTML markup into JSX by applying the above rules. For instance, a simple HTML list needs to be wrapped in a single root element, have all tags closed, and use camelCase for attributes.
Tools like JSX converters can automate this process, but understanding the rules is essential for writing JSX manually.

**Benefits of JSX**
JSX makes React components more readable and maintainable by keeping related markup and logic together.
React’s error messages often guide developers to fix JSX syntax issues, making debugging easier.

The HTML in JS can't use reserved word such as  `class`, that need to be changed to: `className`
