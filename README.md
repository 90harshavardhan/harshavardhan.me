# harshavardhan.me

Personal website of Harsha Vardhan — engineering leader, AI builder, distributed systems thinker.

Built with [Hugo](https://gohugo.io/) + [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, hosted on GitHub Pages via Cloudflare.

**Live site:** [harshavardhan.me](https://harshavardhan.me)

---

## Stack

| Layer | Technology |
|---|---|
| Static site generator | Hugo v0.163.3 (extended) |
| Theme | PaperMod (git submodule) |
| Hosting | GitHub Pages |
| DNS + CDN | Cloudflare |
| Forms | Formspree |
| Newsletter | Buttondown |
| Deploy | GitHub Actions |

---

## Local Development

### Prerequisites

- Hugo extended v0.112+ ([install via snap](https://snapcraft.io/hugo): `sudo snap install hugo`)
- Git

### Setup

```bash
# Clone the repo with submodules
git clone --recurse-submodules git@github.com:90harshavardhan/harshavardhan.me.git
cd harshavardhan.me

# Start local server with drafts visible
hugo server --buildDrafts
```

Open [http://localhost:1313](http://localhost:1313) in your browser.

### Preview without drafts (production mode)

```bash
hugo server
```

### Build static output

```bash
hugo --minify
# Output is in public/ (gitignored)
```

---

## Project Structure

```
harshavardhan.me/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions — auto deploy on push to master
├── archetypes/                 # Hugo content templates
├── assets/
│   └── css/
│       └── extended/
│           └── custom.css      # Custom CSS overrides (WordPress alignment classes etc)
├── content/
│   ├── posts/                  # Blog posts (Markdown)
│   ├── about/                  # About page
│   ├── projects/               # Projects page
│   ├── whoami/                 # Draft — old about page (pending review)
│   └── search.md               # Search page (required by PaperMod)
├── static/
│   └── wp-content/
│       └── uploads/            # Migrated images from harshachandra.org
├── themes/
│   └── PaperMod/               # Theme as git submodule
└── hugo.toml                   # Hugo configuration
```

---

## Content Workflow

### Writing a new post

```bash
hugo new content posts/my-new-post.md
```

This creates a new post with `draft: true`. Edit the file, then when ready to publish change `draft: true` to `draft: false`.

### Publishing a draft post

Open the post's `.md` file and change the front matter:

```yaml
draft: true   →   draft: false
```

Then commit and push — GitHub Actions will auto-deploy within ~1 minute.

### Viewing all drafts locally

```bash
hugo server --buildDrafts
```

---

## Deployment

Deployment is fully automated via GitHub Actions (`.github/workflows/deploy.yml`).

**Trigger:** Every push to `master` branch

**Pipeline:**
```
Push to master
  → GitHub Actions triggered
  → Checkout repo + submodules
  → Setup Hugo extended
  → Build: hugo --minify
  → Deploy public/ to GitHub Pages
```

No manual steps needed after pushing.

---

## Theme

Using [PaperMod](https://github.com/adityatelange/hugo-PaperMod) as a git submodule.

### Update theme

```bash
git submodule update --remote themes/PaperMod
git commit -am "chore: update PaperMod theme"
git push
```

### Custom CSS

Theme overrides live in `assets/css/extended/custom.css`. PaperMod automatically picks up any CSS files in this directory.

---

## Content Migration

Content was migrated from [harshachandra.org](https://harshachandra.org) (WordPress) using the [wordpress-to-hugo-exporter](https://github.com/SchumacherFM/wordpress-to-hugo-exporter) plugin.

All migrated posts are marked `draft: true` and require review before publishing.

**Old domain redirect:** harshachandra.org → harshavardhan.me (301 via Cloudflare)

---

## Forms

- **Contact / Speaking / Collaboration** — [Formspree](https://formspree.io) (free tier, 50 submissions/month)
- **Newsletter signup** — [Buttondown](https://buttondown.email) (free up to 100 subscribers)

---

## License

Content © Harsha Vardhan. All rights reserved.

Theme (PaperMod) is MIT licensed.
