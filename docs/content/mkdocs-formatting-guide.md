---

# MkDocs Formatting Guide

MkDocs is a static site generator for project documentation that uses Markdown. This guide covers the essential formatting and structuring tips for writing articles in MkDocs.

---

## Basic Document Structure

MkDocs follows a simple hierarchy using **Markdown headings**:

```markdown
# Main Title (h1)
## Subheading (h2)
### Section (h3)
#### Subsection (h4)
```

**Example:**

````markdown
# My MkDocs Knowledge Base

## Networking Commands

### Scanning Open Ports with Nmap
```bash
nmap -sV -A <target>
````

````

---

## Code Blocks

For adding code snippets, use **triple backticks** (` ``` `) with the language specified:

```markdown
```bash
ls -lah
````

````

This renders as:

```bash
ls -lah
````

Alternatively, you can use **four-space indentation**, but backticks are preferred for syntax highlighting:

```markdown
    ls -lah
```

---

## Lists & Bullet Points

MkDocs supports both **unordered** and **ordered** lists:

### Unordered List:

```markdown
- Item 1
- Item 2
  - Subitem 2.1
  - Subitem 2.2
```

### Ordered List:

```markdown
1. First item
2. Second item
   1. Sub-item
   2. Sub-item
```

---

## Links & Images

### Adding Links:

```markdown
[OpenAI](https://openai.com)
```

This renders as: [OpenAI](https://openai.com)

### Adding Images:

```markdown
![Alt Text](https://example.com/image.png)
```

You can also specify image width in MkDocs using custom CSS.

---

## Blockquotes & Callouts

Blockquotes are used for emphasizing notes or warnings:

```markdown
> This is a blockquote. Use it for important notes.
```

To create **callouts** using extensions like `admonition`:

```markdown
!!! note "Important Note"
    This is a highlighted note.
```

---

## Tables

Tables can be created using **pipes (**``**)**:

```markdown
| Command  | Description       |
|----------|-----------------|
| `ls`     | List directory contents |
| `pwd`    | Print working directory |
```

This renders as:

| Command | Description             |
| ------- | ----------------------- |
| `ls`    | List directory contents |
| `pwd`   | Print working directory |

---

## Customizing MkDocs

### Configuring `mkdocs.yml`

Your `` defines the navigation and settings:

```yaml
site_name: My Documentation
nav:
  - Home: index.md
  - Guide: guide.md
theme:
  name: material
```

### Running the Local Server

Start the MkDocs server locally to preview changes:

```bash
mkdocs serve
```

Visit `http://127.0.0.1:8000/` in your browser.

---

## Extending MkDocs

### Installing Plugins

You can extend MkDocs with plugins:

```bash
pip install mkdocs-material
```

Then add it to `mkdocs.yml`:

```yaml
theme:
  name: material
```

---

## Conclusion

This guide covers the essentials for formatting articles in MkDocs, including headings, code blocks, lists, links, images, and tables. Keep your documentation structured, readable, and well-organized!


---

