# Copilot instructions for this repository

Purpose
- This repository contains a built static personal website (compiled site output). Future Copilot sessions should treat it as the generated site unless the user supplies a separate source repository.

Build / test / lint commands
- No build/test/lint scripts or tool manifests (package.json, Gemfile, Makefile) are present in this repo.
- Quick local preview (recommended):
  - Python: python3 -m http.server 8000 (run from repo root), then open http://localhost:8000
  - If Node's http-server is available: npx http-server ./ -p 8000
- To preview a specific page, open its index.html directly (e.g., posts/first-post/index.html).
- If asked to add CI/test/lint, request the preferred tooling (e.g., Playwright, Jest) because none are preconfigured.

High-level architecture (big picture)
- Flattened compiled static site layout (pre-rendered HTML):
  - Root: index.html, sitemap.xml, index.json, index.xml and CNAME (custom domain)
  - Content pages are organized by directory: posts/<slug>/index.html, tags/<name>/index.html, categories/<name>/index.html, about/index.html
  - assets/: compiled static assets (CSS, images). CSS file names include a content hash (e.g., stylesheet.<hash>.css)
- This repo appears to be the output of a static site generator (e.g., Jekyll/Hugo/other). There is no source site config in this repository.

Key conventions and patterns
- Per-post pages: each post is a directory under posts/ with an index.html. Edit that index.html to change that post in this repo.
- Tag/category pages: tags/<tag>/ and categories/<cat>/ each have index.html and index.xml where present.
- Asset hashing: CSS files in assets/css are content-hashed. When editing HTML to reference a new asset, update the filename in the HTML head accordingly.
- CNAME: the CNAME file contains the single custom domain; keep it as one-line plain text.
- Generated artifacts: sitemap.xml, index.json, and index.xml are generated outputs; do not hand-edit unless intentionally updating the generated output.

Guidance for Copilot sessions
- Always detect whether the user intends to modify the built output or the source site. If the user wants to change content but has not provided the source, ask whether to:
  1) make changes directly to the built HTML in this repo (quick, immediate), or
  2) work in the source repository (recommended if the site is generated) — request its location or config files.
- When editing HTML files, search for references to assets/css to find the hashed CSS filename and update consistently.
- When adding posts, follow the existing pattern: create posts/<slug>/index.html and replicate the structure used by existing posts.
- If asked to add build/test tooling, present options (example: add package.json + scripts for npm tooling, or add a simple Makefile), and note that adding these changes requires creating a source toolchain rather than editing only generated output.

Checked AI assistant configs
- No repository files matching known assistant configs were found (CLAUDE.md, .cursorrules, AGENTS.md, .windsurfrules, CONVENTIONS.md, AIDER_CONVENTIONS.md, .clinerules). If a source repo contains such files, incorporate them when available.

Notes for reviewers
- If a full rebuild pipeline is required, request the original source repository or provide instructions to re-generate the site with a chosen static-site tool.

---

If you want, Copilot can also add a minimal local test/preview workflow (e.g., a GitHub Actions job to serve the site or run Playwright checks). Would you like to configure any MCP servers (for example, Playwright or other web test servers) for this project?