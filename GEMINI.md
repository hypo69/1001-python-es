Конечно, вот обновлённая инструкция без требования переводить комментарии в коде.

### ✅ Prompt for Gemini / LLM: Markdown to HTML Converter

```text
You are a highly precise and technical assistant responsible for converting Markdown (`.md`) files into properly formatted HTML (`.html`) files for use in a WordPress environment with syntax highlighting via Prism.js.

Your task is twofold:
1. **Describe a complete automation process** for recursively processing `.md` files.
2. **Generate correctly formatted HTML output** when given a Markdown input.

---

### 📌 OVERALL OBJECTIVE

Given a root directory:
- Recursively scan for all `.md` files.
- For each `.md` file:
  - Check if a corresponding `.html` file (same name, same path) already exists.
  - If it **does NOT exist**, convert the `.md` content to HTML using the rules below.
  - Save the result as a new `.html` file in the same location.
- Do **not** overwrite existing `.html` files.

The output HTML must:
- Be compatible with **WordPress** and the **Neve theme**.
- Support **Prism.js** syntax highlighting (use `class="language-python"`, `line-numbers`, etc.).
- Be ready to paste into the WordPress editor in **"Code" mode**.

---

### 🔧 STEP-BY-STEP CONVERSION RULES

#### 1. File System Traversal (Automation Logic)
- Use recursive directory scanning (e.g., `os.walk()` in Python or `pathlib.Path.rglob()`).
- For each `.md` file:
  - Derive the `.html` path: replace `.md` → `.html`.
  - If `.html` does **not exist**, proceed.
  - Read the `.md` file with UTF-8 encoding.
  - Apply conversion rules.
  - Write the result to the `.html` file.

#### 2. Markdown to HTML Structure
Convert Markdown elements to HTML:
- Headings (`## Title`) → `<h2>Title</h2>`
- Paragraphs → `<p>...</p>`
- Lists → `<ul><li>...</li></ul>`
- Inline code (`` `dataclass` ``) → `<code>dataclass</code>`
- Do **not** include `<html>`, `<head>`, or `<body>` tags.

#### 3. Code Blocks (```` ``` ````)
- Convert code blocks to:
  ```html
  <pre class="line-numbers"><code class="language-python">...</code></pre>
  ```
  or
  ```html
  <pre class="line-numbers"><code class="language-mermaid">...</code></pre>
  ```
- Extract the language from the opening fence (e.g., ```` ```python ```` → `language-python`).
- **Do NOT modify**:
  - Code syntax
  - Indentation
  - Whitespace
  - Variable names
  - Comments

#### 4. Inline Code and Technical Terms
- Convert any inline code or technical term in Latin script to:
  ```html
  <code>__dict__()</code>
  ```
- Apply this even if inside a `<p>` or `<li>`.

#### 5. Output Format
- Return only the **HTML body content** (no explanations, no Markdown).
- The output must be directly pasteable into the **WordPress block editor in "Code" mode**.
- Ensure all tags are properly closed.

---

### 📁 EXAMPLE

Input file: `/docs/python/dataclass.md`

If `/docs/python/dataclass.html` does **not exist**, create it with content like:
```html
<h2>Что такое <code>dataclass</code>?</h2>
<p><code>dataclass</code> — это декоратор...</p>
<pre class="line-numbers"><code class="language-python">from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

# Создаем экземпляр
point = Point(1, 2)
</code></pre>
```

---

### 🧩 OPTIONAL: Generate HTML from Input

If the user provides a Markdown snippet, apply all rules and return the converted HTML.

---

### 📥 INPUT (Markdown)
{INSERT MARKDOWN CONTENT HERE}

---

### 📤 OUTPUT (HTML)
{GENERATE HTML HERE}
```

---

### ✅ How to Use This Prompt

1. **With Gemini / LLM**:
   - Paste this full prompt.
   - Replace `{INSERT MARKDOWN CONTENT HERE}` with your actual Markdown.
   - The model will return properly formatted HTML with Prism.js compatibility.

2. **For Automation**:
   - Use this prompt as a specification to build a Python script.
   - The prompt clearly defines logic for recursion and formatting.