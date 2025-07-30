---
weight: 4
title: How to Write Pretty Markdown Files. A Guide for Clean and Readable Content
date: 2025-07-30
draft: false
author: Vincent
description: How to Write Pretty Markdown Files. A Guide for Clean and Readable Content
tags:
  - IT
categories:
  - IT
---
---

Markdown is a lightweight markup language that lets you format plain text into structured documents — ideal for blogging, notes, wikis, and technical documentation.

Whether you're writing blog posts for Hugo, documentation for GitHub, or notes in Obsidian, writing **pretty Markdown** improves **readability**, **maintainability**, and **presentation**.

In this post, I'll cover:
- Core Markdown syntax (headers, lists, links, images)
- Tips for structure and aesthetics
- Useful extended syntax (tables, code blocks, alerts)

---

## ✍️ Basic Markdown Syntax

### 📌 Headers

Use `#` to define headers. Each additional `#` represents a smaller heading:

```markdown
# Heading 1 (Title)
## Heading 2 (Section)
### Heading 3 (Subsection)
```

Avoid skipping levels (e.g., don’t jump from `#` to `####`).

### 📋 Lists

**Unordered List**:

```markdown
- Item A
- Item B
	- Subitem B.1
```

**Ordered List**:

```markdown
1. Step One
2. Step Two
   3. Substep
```

Tip: Indent subitems with 2 spaces.

---

### 🔗 Links and Images

**Link**:

```markdown
[OpenAI](https://openai.com)
```

**Image**:

```markdown
![Alt text](https://example.com/image.jpg)
```

Use descriptive `alt` text — it improves accessibility and SEO.

---

### 🧾 Blockquotes

Use `>` for quoting text:

```markdown
> This is a quote. Great for highlighting notes or references.
```

You can nest them or use multiple lines for longer quotes.

---

### 💻 Code Blocks

**Inline Code**:

``Use backticks like this for `inline code`.``

**Multi-line Code Block**:

<pre> ```python def greet(name): return f"Hello, {name}!" ``` </pre>

Specifying the language (`python`, `bash`, `json`, etc.) gives you **syntax highlighting** in most Markdown renderers (like Hugo or GitHub).

---

## 📐 Tips for a Clean Markdown Structure

✅ **Use consistent header levels**  
✅ **Use whitespace to separate sections** — 1 blank line between paragraphs or headers  
✅ **Avoid overly long paragraphs** — split ideas into smaller chunks  
✅ **Use bullet points or tables for structured info**

---

## 📊 Extended Markdown: Tables, Alerts, and More

### 📋 Tables

```markdown
| Name       | Role         | Favorite Tool |
|------------|--------------|---------------|
| Alice      | DevOps       | Docker        |
| Bob        | Backend Dev  | Django        |
```

This is **GitHub-Flavored Markdown (GFM)** — supported in most modern tools.

---

### 💡 Callouts or Alerts (Hugo or Markdown extensions)

Some Markdown renderers (like Hugo with shortcodes or Obsidian plugins) allow callouts:

```markdown
> 💡 **Tip:** You can use emoji in headings and callouts for visual emphasis.
```

Or if using Hugo shortcodes:

```markdown
{{% alert note %}}
This is a note or tip box.
{{% /alert %}}
```

## 🔠 Text Formatting Cheatsheet

|Format|Markdown Syntax|Example Output|
|---|---|---|
|Bold|`**bold**` or `__bold__`|**bold**|
|Italic|`*italic*` or `_italic_`|_italic_|
|Bold + Italic|`***bold italic***`|_**bold italic**_|
|Strikethrough|`~~strikethrough~~`|~~strikethrough~~|
|Inline code|`` `inline` ``|`inline`|
## 📁 Organizing Markdown Files for Static Sites (like Hugo)

- Store posts in `content/posts/`
    
- Use front matter for metadata:

```markdown
---
title: "My Blog Post"
date: 2025-07-30
tags: ["tag1", "tag2"]
draft: false
---
```

## 🧠 Final Thoughts

Markdown is simple but powerful. By following best practices and learning the richer syntax options, you can make your content:

- Easier to read
    
- Nicer to look at
    
- More useful to others (or your future self)
