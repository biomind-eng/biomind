# BioMIND — Cluster Website

**BioMIND** — *BioAI, Molecular Intelligence, Networks, and Discovery* — is an interdisciplinary research cluster at the University of Central Florida. The cluster federates:

- **Complex Adaptive Systems Laboratory (CASL)** — *Ivan I. Garibay*
- **Human-Centered AI Research Lab (Human-CAIR)** — *Ozlem Ozmen Garibay*
- **Molecular Machine Learning (MoML)** — *Ozlem Ozmen Garibay*
- **Applied Innovative AI Research Lab (AI-AIR)** — *Niloofar Yousefi*

This repository contains the source of the BioMIND website — a static [Quarto](https://quarto.org) site deployed via GitHub Pages.

> **Beta notice.** This site is in beta. Some entries — funding, exact citation counts, patents, collaborators — require faculty review before they should be made public. Search the source for `TODO(faculty-approval)` to find items awaiting confirmation. Official UCF branding will be added after the relevant approvals are in place.

---

## Repository structure

```
biomind-website/
├── _quarto.yml                  # Site configuration (navbar, footer, theme)
├── index.qmd                    # Homepage (hero, pillars, labs, news, CTA)
├── about.qmd                    # About the cluster
├── contact.qmd                  # Contact page
├── people/
│   ├── index.qmd                # People landing
│   ├── faculty.qmd              # Faculty profiles (Ivan, Ozlem, Niloofar)
│   ├── students.qmd             # Student profiles (template-driven)
│   └── alumni.qmd               # Alumni
├── research/
│   ├── index.qmd                # Research landing (6 pillars)
│   ├── bioai.qmd
│   ├── molecular-ml.qmd
│   ├── foundation-models.qmd
│   ├── complex-systems.qmd
│   ├── trustworthy-ai.qmd
│   └── agentic-ai.qmd
├── publications/
│   ├── index.qmd                # Renders publications, grouped
│   └── publications.bib         # Source of truth for citations
├── labs/
│   ├── index.qmd
│   ├── casl.qmd
│   ├── human-cair.qmd
│   ├── moml.qmd
│   └── aiair.qmd
├── news/
│   ├── index.qmd                # Auto-listing of posts/
│   └── posts/                   # One .qmd per news item
├── seminars/
│   ├── index.qmd
│   └── past.qmd
├── outreach/index.qmd
├── funding/index.qmd
├── collaborators/index.qmd
├── assets/
│   ├── logo/                    # Logo / favicon (placeholder mark + SVG favicon)
│   ├── photos/                  # Cluster photos
│   ├── people/                  # Headshots (square, ~400×400)
│   └── icons/                   # SVG/PNG icons
├── styles.css                   # BioMIND visual identity (navy/teal/green/gold)
├── README.md                    # This file
├── _inbox/                      # Gitignored staging area for CVs / drafts / private files
└── .github/workflows/publish.yml  # GitHub Actions: render + deploy
```

---

## Local development

### 1. Install Quarto

- macOS: `brew install quarto`
- Linux: download the `.deb` / `.rpm` / tarball from <https://quarto.org/docs/get-started/>
- Windows: download the installer from <https://quarto.org/docs/get-started/>

Verify:

```bash
quarto --version
```

### 2. Preview the site locally

```bash
quarto preview
```

This starts a dev server (default <http://localhost:4200>) with **live reload** on `.qmd`, `.bib`, and `.css` changes.

### 3. Render a static build

```bash
quarto render
```

Output goes to `_site/` — open `_site/index.html` directly or serve with any static HTTP server.

---

## How to update content

### Update a faculty member

Edit `people/faculty.qmd`. Each profile is a section heading + a `bm-person-card` block + body content. Update the bio, links, research tags, and (after PI approval) the *Selected highlights* numbers. Headshots live in `assets/people/firstname-lastname.jpeg` and are referenced from inside each `bm-person-photo` block.

### Update a student profile

Edit `people/students.qmd`. The page contains template cards under **Ph.D. Students**, **M.S. Students**, and **Undergraduate Researchers**. Copy a template card and replace the placeholder fields. See the *Content checklists* below for what to include.

### Update publications

The single source of truth is `publications/publications.bib`.

1. Open `publications/publications.bib`.
2. Append a new BibTeX entry, including a `keywords` field. Recommended keywords:
   - `selected`, `recent`, `preprint`, `workshop`, `software`
   - One of `bioai`, `molecular-ml`, `foundation-models`, `human-centered-ai`, `complex-systems`, `learning-theory`
3. To feature a publication on the homepage or as a flagship card on `publications/index.qmd`, add a corresponding `bm-pub-card` block. The full reference list at the bottom of `publications/index.qmd` is rendered automatically from the `.bib` file.

### Add a news post

1. Create a new file in `news/posts/`, named `YYYY-MM-short-slug.qmd`.
2. Front matter:

   ```yaml
   ---
   title: "Your post title"
   description: "Short summary for the listing."
   date: "2026-05-15"
   categories: [announcement, paper, talk]
   author: "BioMIND"
   ---
   ```

3. The post appears on `news/index.qmd` automatically (Quarto listing).

### Add a lab update

Lab pages live under `labs/`. Each is a normal `.qmd` file with sections for *About*, *Director*, *Connection to BioMIND*, *Research themes*, *People*, and *Publications and news*.

---

## Deploying to GitHub Pages

### One-time setup

1. **Create the GitHub repository** — push this directory to a new repository (private or public).
2. **Update placeholders in `_quarto.yml`** — replace `your-org/biomind-website` with the actual `owner/repo` slug for `repo-url`, the navbar GitHub link, and `site-url`.
3. **Enable GitHub Pages** — in the repository on GitHub, go to **Settings → Pages**, set **Source** to **GitHub Actions**.
4. **(Optional) Custom domain** — when the official UCF domain is ready, configure it under Settings → Pages and add a `CNAME` file to the repo root.

### Automated deployment

`.github/workflows/publish.yml` is configured to:

- Trigger on every push to `main` (or manual `workflow_dispatch`)
- Install Quarto, render the site, upload `_site/` as a Pages artifact, and deploy via `actions/deploy-pages@v4`.

The first successful run on `main` publishes the site. Subsequent pushes redeploy automatically.

---

## UCF branding notice

This beta site uses BioMIND's own color palette (deep navy, teal, soft green, with UCF gold as a sparing accent) and **does not embed official UCF logos or trademarks**. Before adding any UCF marks, logos, or wordmarks:

- Obtain approval from **UCF Communications and Brand Standards**
- Follow the official UCF brand guidelines

Sections of the site reserve space where UCF branding can be added once approved.

## Faculty review before public release

The following items should be reviewed by the relevant faculty before being made public on the production site:

- **Exact funding entries** — award names, sponsors, dollar amounts
- **Exact citation, h-index, or impact metrics** — currently flagged as "selected highlights" with `TODO(faculty-approval)` comments
- **Patent and patent-pending claims** — keep concise and faculty-approved
- **Collaborator listings** — both UCF and external; should be confirmed with the named collaborators
- **Selected publication lists** — verify author lists and venue metadata
- **Selected highlights blocks** — confirm numbers before publication

Search the repository for `TODO(faculty-approval)` to find every flagged item.

---

## Content collection checklist

### Faculty profile checklist

- Name
- Title
- Department
- Lab
- Email
- Website
- Google Scholar
- LinkedIn
- ORCID
- Short bio
- Research keywords
- Selected publications
- Headshot (square, ~400×400 px)
- Approved grants / funding highlights (with PI approval)

### Student profile checklist

- Name
- Program / year
- Advisor
- Lab affiliation
- Research keywords
- Short bio
- Publications / preprints
- GitHub
- Google Scholar
- LinkedIn
- Personal website
- ORCID
- Headshot (square, ~400×400 px)

### Website review checklist (pre-launch)

- [ ] Confirm faculty titles and departmental affiliations
- [ ] Confirm lab names and director assignments
- [ ] Confirm emails and external profile links
- [ ] Confirm selected publication metadata (titles, authors, venues, DOIs)
- [ ] Confirm funding statements (sponsors, programs, periods)
- [ ] Confirm collaborator listings (UCF, external, international)
- [ ] Confirm UCF branding compliance (no unauthorized logos)
- [ ] Confirm headshot permissions

---

## License and content

- Code and configuration in this repository: MIT-style permissive, unless overridden by member-lab decisions.
- Page text and images: © 2026 BioMIND Research Cluster, University of Central Florida. Reuse with attribution; for substantial reuse, please contact the cluster.

---

## Questions

- Site issues — open an issue in this repository.
- Content additions — submit a pull request or contact the cluster coordinator.
- Faculty / staff / student onboarding — see the *Content collection checklist* above.
