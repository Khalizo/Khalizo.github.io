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
assets/images/          # Favicon files
hugo.yaml               # Site configuration
themes/PaperMod/        # Theme (git submodule)
```

## Configuration

- **Profile photo**: Add to `static/images/profile.jpg`
- **Social links**: Edit `params.socialIcons` in `hugo.yaml`
- **Menu items**: Edit `menu.main` in `hugo.yaml`

## Troubleshooting

- **Build fails**: Run `hugo --gc --minify` locally first
- **Images not showing**: Use relative paths, keep images with post
- **Theme issues**: Run `git submodule update --init --recursive`

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
