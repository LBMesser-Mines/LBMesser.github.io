# ~/academic — Yazi-Style Terminal Academic Website

A personal academic website that mirrors the [Yazi](https://github.com/sxyazi/yazi) terminal file manager, with full vim-style keyboard navigation. Content is loaded from plain `.md` markdown files and rendered at runtime.

## Quick Start

```bash
# 1. Clone or download this repo
git clone https://github.com/yourusername/yourusername.github.io.git
cd yourusername.github.io

# 2. Preview locally (required — fetch() doesn't work over file://)
python -m http.server 8000

# 3. Open http://localhost:8000 in your browser
```

## File Structure

```
├── index.html              ← The entire site (single HTML file)
├── content/                ← Your markdown content
│   ├── intro/
│   │   ├── about.md
│   │   ├── bio.md
│   │   └── news.md
│   ├── research/
│   │   ├── project_1.md
│   │   ├── project_2.md
│   │   └── open_source.md
│   ├── publications/
│   │   ├── journal_articles.md
│   │   ├── conference_papers.md
│   │   └── preprints.md
│   ├── presentations/
│   │   ├── invited_talks.md
│   │   └── conference_talks.md
│   ├── cv/
│   │   ├── education.md
│   │   ├── experience.md
│   │   ├── awards.md
│   │   ├── skills.md
│   │   └── download_cv.md
│   └── contact/
│       └── email.md
├── slides/                 ← PDF slide decks
│   └── example_talk.pdf
├── assets/                 ← Images, CV PDF, etc.
│   └── cv.pdf
└── README.md
```

## How to Edit Content

**Just edit the `.md` files.** Write standard GitHub-flavored markdown — headings, bold, italic, links, tables, code blocks, lists, images, horizontal rules. The site parses everything with [marked.js](https://marked.js.org/).

### Adding a new file

1. Create the `.md` file in the appropriate `content/` subfolder
2. Open `index.html` and find the `SITE_DATA` object near the top of the `<script>`
3. Add an entry to the relevant section:

```javascript
{ name: 'new_paper.md', icon: '▪', file: 'content/publications/new_paper.md' },
```

### Removing a file

Delete the `.md` file and remove its line from `SITE_DATA`.

### Adding a new top-level tab

1. Create a new folder in `content/`
2. Add a new key to `SITE_DATA`:

```javascript
teaching: {
  icon: '◎',
  subs: [
    { name: 'courses.md', icon: '▸', file: 'content/teaching/courses.md' },
  ]
}
```

## Embedding PDF Slide Decks

Two methods:

### Method 1: Direct PDF entry
In `SITE_DATA`, set `pdf: true`:
```javascript
{ name: 'my_talk.pdf', icon: '◧', file: 'slides/my_talk.pdf', pdf: true },
```

### Method 2: PDF inside a markdown file
Add this comment at the top of any `.md` file:
```markdown
<!-- PDF_EMBED: slides/my_talk.pdf -->

Additional notes about this presentation below the viewer.
```

## Keyboard Controls

| Key | Action |
|-----|--------|
| `h` `j` `k` `l` | Navigate (left/down/up/right between panels) |
| `Enter` | Drill into the next panel |
| `g` `g` | Jump to top of current list |
| `G` | Jump to bottom of current list |
| `/` | Open "go to" with tab completion |
| `Tab` | Cycle through matches in go-to mode |
| `:` | Command mode |
| `:ls` | Show all files popup |
| `:q` | "Quit" (fun easter egg) |
| `:intro` `:research` etc. | Jump to a tab |
| `Esc` | Return to tabs panel / close popups |

## Customization

### Change your name
Find `<div class="name">Your Name</div>` in the HTML.

### Change colors
Edit the CSS variables at the top of `<style>`:
```css
--green: #C166FA;      /* Top bar + active highlight */
--orange: #ff6a00;     /* Accent color */
--lime: #c8ff00;       /* Secondary accent */
```

### Change icons
Each tab and file has an `icon` property in `SITE_DATA`. Use any Unicode character.

## Deploy to GitHub Pages

```bash
# 1. Create repo named yourusername.github.io
# 2. Push everything
git add .
git commit -m "initial site"
git push origin main

# 3. In repo Settings → Pages → Source: Deploy from branch (main)
# 4. Your site is live at https://yourusername.github.io
```

That's it — no build step, no dependencies, no CI pipeline. Push markdown, site updates.

## Dependencies

- [marked.js](https://marked.js.org/) v12 (loaded from CDN, ~7kb gzipped)
- [Quantico](https://fonts.google.com/specimen/Quantico) font (Google Fonts CDN)

No build tools. No node_modules. No framework.
