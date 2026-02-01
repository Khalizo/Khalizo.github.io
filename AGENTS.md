# Agent Instructions for Managing babskhalidson.com

## Local Development Workflow

**ALWAYS test locally before pushing to GitHub to avoid CI failures.**

### 1. Start Local Server
```bash
cd /Users/khalizo/Documents/coding_projects/Khalizo.github.io
hugo server -D
```
Visit `http://localhost:1313` to preview changes in real-time.

### 2. Create New Blog Post
```bash
hugo new content/posts/post-name/index.md
```
- Posts go in `content/posts/your-post-name/`
- Images go in the same folder as `index.md`
- Use relative paths for images: `![alt](image.jpg)`

### 3. Test Build Locally
```bash
hugo --gc --minify
```
This builds the site exactly as GitHub Actions will. Check for errors before pushing.

### 4. Push to GitHub
```bash
git add -A
git commit -m "Your message"
git push
```

## Site Structure

```
content/posts/          # Blog posts (each in own folder)
static/images/          # Site-wide images (profile photo, etc.)
static/                 # Published root (favicons, manifest, CNAME)
assets/images/          # Design assets (not published unless copied to static/)
hugo.yaml               # Site configuration
themes/PaperMod/        # Theme (git submodule)
```

## Configuration

- **Profile photo**: Add to `static/images/profile.jpg`
- **Social links**: Edit `params.socialIcons` in `hugo.yaml`
- **Menu items**: Edit `menu.main` in `hugo.yaml`
- **Favicons/manifest**: Must live in `static/` (e.g. `static/favicon.ico`, `static/site.webmanifest`)
- **Custom domain**: Keep `static/CNAME` in sync with `CNAME`

## GitHub Pages Deployment (Prevent 404s)

This repo uses GitHub Actions to build Hugo and publish `public/`. If Pages is set
to “Deploy from branch”, the site will 404 because the repo root does not contain
an `index.html`.

### Required Settings
- **Pages build type**: **GitHub Actions** (not “Deploy from branch”)
- **Custom domain**: `babskhalidson.com`

### Quick verification
```bash
gh api repos/Khalizo/Khalizo.github.io/pages
```
Ensure `build_type` is `workflow` and `cname` is `babskhalidson.com`.

### If the site shows a 404
1. Check Actions ran successfully:
   ```bash
   gh run list -R Khalizo/Khalizo.github.io --limit 5
   ```
2. If build type is wrong, switch back to Actions:
   ```bash
   gh api -X PUT repos/Khalizo/Khalizo.github.io/pages -f build_type=workflow -f cname=babskhalidson.com -F https_enforced=true
   ```
3. Re-run the deploy workflow:
   ```bash
   gh workflow run "Build and deploy" -R Khalizo/Khalizo.github.io
   ```

## Troubleshooting

- **Build fails**: Run `hugo --gc --minify` locally first
- **Images not showing**: Use relative paths, keep images with post
- **Theme issues**: Run `git submodule update --init --recursive`
- **Homepage 404**: Pages is likely set to “Deploy from branch”; set build type to GitHub Actions

## Key Commands

```bash
# Local preview with drafts
hugo server -D

# Build for production
hugo --gc --minify

# Create new post
hugo new content/posts/post-name/index.md

# Update theme
cd themes/PaperMod && git pull && cd ../..
```
