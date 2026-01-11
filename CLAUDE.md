# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an academic personal website built with Jekyll, based on the Academic Pages template. It's deployed via GitHub Pages and showcases publications, research, talks, teaching materials, and a portfolio for an academic researcher.

## Development Commands

### Local Development

**Start local development server:**
```bash
bundle install
jekyll serve -l -H localhost
# OR
bundle exec jekyll serve -l -H localhost
```

The site will be available at `http://localhost:4000`. The server auto-rebuilds on file changes.

**Using Docker:**
```bash
docker compose up
```

### Asset Build Commands

**Build minified JavaScript:**
```bash
npm install
npm run build:js
```

**Watch JavaScript for changes:**
```bash
npm run watch:js
```

## Architecture

### Jekyll Collections

The site uses Jekyll collections to organize different content types. Each collection is defined in `_config.yml` and has its own directory:

- **`_publications/`**: Research papers and publications (categories: books, manuscripts, conferences, workingpapers, workinprogress)
- **`_talks/`**: Conference presentations and talks
- **`_teaching/`**: Teaching materials and courses
- **`_portfolio/`**: Portfolio items and projects
- **`_posts/`**: Blog posts (standard Jekyll posts)
- **`_pages/`**: Static pages (About, CV, etc.)

Each collection item is a markdown file with YAML frontmatter that controls layout and metadata.

### Key Configuration

**`_config.yml`**: Main configuration file containing:
- Site metadata (title, description, URL)
- Author/bio information and social links
- Collection definitions and defaults
- Plugin configuration
- Publication category definitions

**`_data/navigation.yml`**: Controls the main navigation menu header links

### Layouts and Templates

- **`_layouts/`**: Page layout templates (default, single, archive, cv-layout, etc.)
- **`_includes/`**: Reusable template partials (author-profile, archive-single, masthead, etc.)
- **`_sass/`**: Sass/SCSS stylesheets

Key layout hierarchy:
- `default.html`: Base layout with HTML structure
- `single.html`: Most content pages (extends default)
- `archive.html`: Collection listing pages
- `cv-layout.html`: Custom CV page layout

### Content Frontmatter Patterns

**Publications** (`_publications/*.md`):
```yaml
---
title: "Paper Title"
collection: publications
category: workingpapers  # books, manuscripts, conferences, workingpapers, workinprogress
permalink: /publication/paper_name
date: 2021-02-01
paperurl: 'http://link-to-pdf.pdf'
citation: 'Author names (Year). Full citation'
coauthors: "Coauthor names"
---
```

**Talks** (`_talks/*.md`):
```yaml
---
title: "Talk Title"
collection: talks
type: "Talk/Tutorial/Workshop"
permalink: /talks/talk-name
venue: "Conference/Institution Name"
date: 2021-01-01
location: "City, Country"
---
```

### Markdown Generation

The `markdown_generator/` directory contains Python scripts and Jupyter notebooks to bulk-generate markdown files from TSV data:

- **`publications.ipynb`/`publications.py`**: Generate publication markdown files from `publications.tsv`
- **`talks.ipynb`/`talks.py`**: Generate talk markdown files from `talks.tsv`
- **`PubsFromBib.ipynb`/`pubsFromBib.py`**: Generate publications from BibTeX files
- **`OrcidToBib.ipynb`**: Import publications from ORCID

These are useful for bulk updates but individual files can be edited directly.

### Static Assets

- **`files/`**: Upload PDFs, datasets, and other downloadable files here (accessible at `https://[username].github.io/files/filename.pdf`)
- **`images/`**: Image assets and figures
- **`assets/js/`**: JavaScript files (source in `assets/js/_main.js`, compiled to `assets/js/main.min.js`)

## Working with Content

### Adding a New Publication

1. Create a new markdown file in `_publications/` (e.g., `paper_name.md`)
2. Add frontmatter with required fields (see frontmatter pattern above)
3. Write abstract/description in the markdown body
4. Upload PDF to `files/` directory if available
5. Set the `category` to one of: books, manuscripts, conferences, workingpapers, workinprogress

### Adding a New Page to Navigation

1. Create markdown file in `_pages/`
2. Edit `_data/navigation.yml` to add link to main menu:
```yaml
main:
  - title: "Page Name"
    url: /pagename/
```

### Modifying Author Profile

Edit the `author:` section in `_config.yml` to update:
- Bio, location, employer
- Social media links (googlescholar, github, linkedin, etc.)
- Profile image (stored in `images/` as `profile.png`)

## Important Notes

- **GitHub Pages compatibility**: This site runs on GitHub Pages, so only whitelisted Jekyll plugins can be used (listed in `_config.yml`)
- **Permalink structure**: Collections use `permalink: /:collection/:path/` format
- **Site rebuilds**: After pushing changes to master branch, GitHub Pages automatically rebuilds the site
- **Local vs production**: Test locally before pushing to verify layout and functionality
- **Archive includes**: The `_includes/archive-single.html` partial handles display formatting for publication listings and can be customized for different display styles
