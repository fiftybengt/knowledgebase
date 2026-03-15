# Creating MkDocs Pages & Managing Navigation

## Introduction

MkDocs is a powerful static site generator designed for documentation projects. This guide covers how to create new **MkDocs pages** and manage site **navigation** using `mkdocs.yml`.

---

##  Creating a New MkDocs Page

Each page in MkDocs is a **Markdown (********`.md`********\*\*\*\*\*\*\*\*) file** stored in the `docs/` directory.

### Steps to Create a Page:

1. **Navigate to the ****************`docs/`**************** folder**:
   ```bash
   cd docs/
   ```
2. **Create a new Markdown file**:
   ```bash
   touch my-new-page.md
   ```
3. **Edit the file** using any text editor:
   ```bash
   code my-new-page.md
   ```
4. **Add content** inside `my-new-page.md`:
   ```markdown
   # My New Page

   Welcome to my new page in MkDocs!
   ```

---

##  Managing Navigation in `mkdocs.yml`

Navigation is defined in **`mkdocs.yml`** under the `nav:` section.

### Example Structure:

```yaml
site_name: My Documentation

nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - Features:
      - Page One: page-one.md
      - Page Two: page-two.md
  - About: about.md
```

### Explanation:

- **Top-level items** (e.g., `Home`, `Getting Started`, `About`) are direct links.
- **Nested items** under `Features` group related pages together.
- **Each entry** follows the format: `Page Title: filename.md`.

---

##  Previewing Changes Locally

After adding pages or updating navigation, preview the changes using:

```bash
mkdocs serve
```

Visit `http://127.0.0.1:8000/` in your browser to see the live site.

---

##  Deploying the Site

When ready, build and deploy the MkDocs site:

```bash
mkdocs build
mkdocs gh-deploy
```

This will generate static files in the `site/` folder and deploy them to GitHub Pages if configured.

---

##  Best Practices

- Keep **file names lowercase** and use `-` instead of spaces.
- Structure navigation **logically** for easy access.
- Use **nested navigation** for better organization.
- Regularly run `mkdocs serve` to preview changes before deployment.

---

## Conclusion

Creating pages in MkDocs is simple, and navigation is controlled via `mkdocs.yml`. By following these best practices, you can build a well-organized documentation site with ease.



