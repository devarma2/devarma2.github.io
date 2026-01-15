# Copilot Instructions for devarma2's Personal Site

## Project Overview

This is a personal Jekyll blog/portfolio site built with the **no-style-please** theme (forked from [riggraz/no-style-please](https://github.com/riggraz/no-style-please)). It's hosted on GitHub Pages at `devarma2.github.io`.

- **Framework**: Jekyll static site generator
- **Theme**: no-style-please (minimalist, no CSS framework)
- **Special Features**: LaTeX math rendering via jektex plugin, GoatCounter analytics
- **Posts Organized By**: Category (engineering, personal, example)

## Architecture & Key Components

### Directory Structure
- **`_posts/`** - Blog posts (Jekyll posts, YYYY-MM-DD-slug.md format)
- **`_layouts/`** - HTML templates (default.html, post.html, home.html, page.html, archive layouts)
- **`_includes/`** - Reusable HTML components (back_link, menu_item, post_list, head, goat_counter)
- **`_data/menu.yml`** - Menu structure definition with category-based post lists
- **`_sass/`** - SCSS stylesheets (minimalist approach, single file: no-style-please.scss)
- **`assets/`** - CSS and JS (main.scss compiles to CSS, mouse_coords.js for interactive demos)

### Data Flow
1. Posts in `_posts/` are processed by Jekyll with frontmatter (layout, category, custom_js, etc.)
2. `_data/menu.yml` defines menu structure with `post_list` entries that render posts by category
3. Templates in `_layouts/` render posts using Liquid templating
4. SCSS compiles to CSS, minimalist styling applied site-wide
5. jektex plugin processes LaTeX math in posts (inline `$$..$$` and display mode)

## Development Workflow

### Local Preview
```bash
bundle exec jekyll serve
# Serves at http://localhost:4000
```

### Build for Deployment
```bash
bundle exec jekyll build
# Output in _site/
```

### Dependencies
- Managed via Gemfile (Ruby bundler)
- Key gems: kramdown-parser-gfm (markdown parsing), jektex (LaTeX rendering)
- Required Ruby stdlib: webrick, csv, bigdecimal, base64, logger

## Post Authoring Conventions

### Frontmatter Structure
```yaml
---
layout: post              # Always "post" for blog posts
category: engineering     # One of: engineering, personal, example
custom_js: mouse_coords   # Optional: load specific JS files from assets/js/
---
```

### Post Naming
- Format: `YYYY-MM-DD-slug.md` (Jekyll standard)
- Example: `2023-02-03-jektex-post.md`

### LaTeX Math Support
- **Inline**: `$$e^{i\theta}$$` renders in-line
- **Display**: Wrapped in `$$ ... $$` on separate lines renders as block
- Jektex caches compiled math in `.jektex-cache/` (don't commit)
- Custom macros defined in `_config.yml`: `\Q` → `\mathbb{Q}`, `\C` → `\mathbb{C}`

## Theme Configuration

Key settings in `_config.yml`:
- **`appearance`**: "dark" (light/dark/auto supported)
- **`lowercase_titles`**: false (preserve post title casing)
- **`show_description`**: false (don't show site description on homepage)
- **`date_format`**: "%Y-%m-%d" (post date display)
- **Permalink**: `/:slug.html` (URLs based on post slug, not date)

## Menu & Category System

`_data/menu.yml` drives the entire site structure:
- **Top-level entries**: Create menu sections
- **`post_list`** entries: Render posts by category with optional "See more" link
  - `category`: Filter posts by frontmatter category
  - `limit`: Show first N posts
  - `show_more_url`: Link to full archive (e.g., `engineering-archive.html`)
- **Direct entries**: Static links or text

Archive pages (`engineering-archive.md`, `personal-archive.md`) use layout matching category name.

## Important Patterns

### Custom JavaScript
Posts can load custom JS by setting `custom_js: filename` in frontmatter. The file is included from `assets/js/filename.js`. Used for interactive demos (e.g., mouse coordinate tracking).

### Minimalist CSS Philosophy
- No CSS framework or bloat
- Single SCSS file (`_sass/no-style-please.scss`)
- Semantic HTML with browser defaults
- When modifying styles, keep changes minimal and aligned with existing approach

### Plugin Extensions
- **jektex**: Math rendering (configured in _config.yml with cache directory and macro definitions)
- **jekyll-feed**: Atom feed generation
- **jekyll-seo-tag**: SEO metadata

## Common Tasks

### Add a New Post
1. Create `_posts/YYYY-MM-DD-title.md`
2. Add frontmatter with layout, category, optional custom_js
3. Write content (supports Markdown + Liquid + LaTeX)
4. If category is new, update `_data/menu.yml` to add post_list entry

### Modify Menu Structure
- Edit `_data/menu.yml`
- Add/remove/reorder entries
- Update `show_more_url` to point to appropriate archive layout

### Add Interactive Feature to Post
1. Create `assets/js/feature_name.js`
2. Add `custom_js: feature_name` to post frontmatter
3. Post can reference DOM hooks added in content

## Deployment

Site is hosted on GitHub Pages. Push to `master` branch triggers automatic build via remote_theme.

## Resources

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [no-style-please Theme Docs](https://github.com/riggraz/no-style-please)
- [jektex LaTeX Plugin](https://github.com/yagarea/jektex)
- [Liquid Templating](https://shopify.github.io/liquid/)
