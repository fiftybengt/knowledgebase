# Managing MkDocs with GitHub

## Introduction
Using **GitHub** for version control and deployment is an essential practice when managing MkDocs projects. This guide covers how to **create a new repository**, update documentation, and deploy it to **GitHub Pages**.

---

##  Creating a New GitHub Repository

1. **Go to GitHub** and log in.
2. **Click on** `+` (top-right) → `New repository`.
3. **Enter repository details**:
   - Repository name: `my-mkdocs-site`
   - Description (optional): "Documentation for my project"
   - Choose **Public** or **Private**.
   - Check **Add a README** (optional).
4. **Click** `Create repository`.

### Cloning the Repository
After creating the repository, clone it to your local machine:

```bash
git clone https://github.com/your-username/my-mkdocs-site.git
cd my-mkdocs-site
```

---

##  Updating MkDocs and Pushing to GitHub
When making changes to MkDocs documentation, follow these steps:

1. **Stage all changes**:
   ```bash
   git add .
   ```
2. **Commit the changes**:
   ```bash
   git commit -m "Added my new page"
   ```
3. **Push to GitHub**:
   ```bash
   git push origin main
   ```
4. **Deploy the site to GitHub Pages**:
   ```bash
   mkdocs gh-deploy
   ```

``` 
mkdocs build --clean
git add .
git commit -m "comment"
git push origin main
mkdocs gh-deploy
```
This will build and deploy your MkDocs site to **GitHub Pages**.

---

##  Configuring GitHub Pages
Ensure that GitHub Pages is enabled for your repository:

1. **Go to your repository on GitHub**.
2. Navigate to **Settings > Pages**.
3. Under **Branch**, select `gh-pages`.
4. Click **Save**.
5. Your site will be available at:
   ```
   https://your-username.github.io/my-mkdocs-site/
   ```

---

##  Best Practices
- Always **commit meaningful messages** (`git commit -m "Updated navigation"`).
- Regularly **pull updates** from the repository before making changes:
  ```bash
  git pull origin main
  ```
- Check **Git status** to review changes before committing:
  ```bash
  git status
  ```

---

## Conclusion
Using GitHub for MkDocs makes it easy to manage documentation changes and deploy updates. By following these steps, you can keep your project well-organized and version-controlled.

