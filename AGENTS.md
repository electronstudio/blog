# AGENTS.md

Guidance for AI coding agents working in this repository.

## Project overview

Personal blog built with [Zola](https://www.getzola.org/) (static site generator, Rust) using the [tabi](https://github.com/welpo/tabi) theme. No JavaScript build tooling, no package manager — Zola does everything.

## Commands

```sh
# Local dev server at http://127.0.0.1:1111
zola serve

# Build site to public/ (also validates content)
zola build
```

There is no test suite; `zola build` succeeding is the primary check. CI runs a build via `.github/workflows/test-build.yml`.

Note: tabi requires Zola ≥ 0.23.6.

## Structure

- `config.toml` — site configuration (Zola settings + `[extra]` tabi settings)
- `content/` — all Markdown content with TOML front matter (`+++` blocks)
  - `_index.md` — home page
  - `blog/` — blog posts (one `.md` file per post)
  - `projects/` — project cards
  - `archive/` — archive page
- `static/` — static assets (e.g. `img/profile.webp` for the home header)
- `themes/tabi/` — the theme, checked out as a git submodule. **Do not edit files here**; overrides belong in the site root or via `config.toml`.
- `public/` — build output (gitignored)

## Conventions

- Posts use TOML front matter: `title`, `date` (YYYY-MM-DD), `description`, and optional `[taxonomies]` with `tags`.
- Site config lives in `config.toml`; tabi-specific options are under `[extra]`. Documented at https://welpo.github.io/tabi/blog/mastering-tabi-settings/
- `base_url`, `title`, `description`, `author` at the top of `config.toml` still contain template placeholders (`YOUR_URL.TLD`, `YOUR_SITE_DESCRIPTION`) — update when personalizing the site.
- Markdown highlighting: `error_on_missing_language = true`, so code blocks must use supported language tags or the build fails.
- Theme updates are automated weekly via `.github/workflows/update-tabi.yml`.

## Git

- `themes/tabi` is a submodule: use `git submodule update --init --recursive` after cloning; commit submodule pointer bumps separately.
