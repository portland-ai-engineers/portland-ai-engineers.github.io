# Portland AI Engineers - Site Maintenance Guide

This document provides guidance for maintaining the [Portland AI Engineers website](https://portland-ai-engineers.github.io/). The site is built with [Hugo](https://gohugo.io/) and uses the [Hextra](https://github.com/imfing/hextra) theme.

## Site Architecture

### Key Directories and Files

- `/content/` - All site content in Markdown format
  - `_index.md` - Homepage content
  - `/posts/` - Blog posts
  - Other top-level pages (events.md, contact.md, etc.)
- `/themes/` - Contains the Hextra theme (as a Git submodule)
- `/static/` - Static assets like images, CSS, and JavaScript
- `/layouts/` - Custom layout templates (if needed to override theme defaults)
- `/archetypes/` - Templates for new content
- `hugo.toml` - Main configuration file
- `.github/workflows/hugo.yml` - GitHub Actions workflow for deployment
- `.nojekyll` - Empty file that tells GitHub Pages not to process the site with Jekyll

## Development Workflow

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/portland-ai-engineers/portland-ai-engineers.github.io.git
   cd portland-ai-engineers.github.io
   ```

2. Start the Hugo development server:
   ```bash
   hugo server -D
   ```

3. View the site at http://localhost:1313/

### Creating New Content

#### Blog Posts

Create a new blog post with:

```bash
hugo new content posts/my-new-post.md
```

This will create a new file in `/content/posts/` with front matter already set up.

#### Pages

Create a new page with:

```bash
hugo new content page-name.md
```

### Front Matter

Each content file begins with front matter (metadata) in YAML format:

```yaml
---
title: "Page Title"
date: 2025-02-28
draft: false
description: "Page description for SEO"
tags: ["tag1", "tag2"]
---
```

Set `draft: false` when ready to publish.

## Publishing Workflow

The site automatically deploys when changes are pushed to the `main` branch:

1. Make your changes locally
2. Test with `hugo server -D`
3. Commit your changes:
   ```bash
   git add .
   git commit -m "type: Brief description of changes"
   git push
   ```
4. GitHub Actions will automatically build and deploy the site

### Commit Message Format

Use the following prefixes for commit messages:
- `feat:` - New feature or content
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `style:` - Formatting, styling changes
- `refactor:` - Code/content restructuring
- `perf:` - Performance improvements
- `chore:` - Maintenance tasks

### Manual Deployment

If needed, you can manually trigger a deployment:
1. Go to the [GitHub repository](https://github.com/portland-ai-engineers/portland-ai-engineers.github.io)
2. Click on "Actions"
3. Select the "Deploy Hugo site to Pages" workflow
4. Click "Run workflow"

## Troubleshooting

### Common Issues

1. **Site shows README instead of Hugo site**
   - Check GitHub Pages settings in repository settings
   - Ensure the `.nojekyll` file exists
   - Verify GitHub Actions workflow completed successfully

2. **Missing content after deployment**
   - Check if content is marked as `draft: true`
   - Verify the file is committed and pushed
   - Check GitHub Actions logs for errors

3. **Broken links or styling**
   - Ensure `baseURL` in `hugo.toml` is correct
   - Check for typos in internal links
   - Verify theme submodule is properly initialized

## Theme Customization

To customize the [PaperMod](https://github.com/adityatelange/hugo-PaperMod/wiki/) theme:

1. Override templates by creating matching files in `/layouts/`
2. Add custom CSS in `/static/css/custom.css`
3. Configure theme settings in `hugo.toml`

## Updating Dependencies

### Update Hugo

The site uses Hugo version 0.145.0. To update:
1. Update the version in `.github/workflows/hugo.yml`
2. Test locally with the new version

### Update Theme

The [PaperMod](https://github.com/adityatelange/hugo-PaperMod/wiki/) theme is included as a Git submodule. To update:

```bash
git submodule update --remote themes/PaperMod
git add themes/PaperMod
git commit -m "chore: Update PaperMod theme"
git push
