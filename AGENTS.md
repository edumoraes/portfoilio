# Repository Guidelines

## Project Structure & Module Organization

This repository is a Hugo-based one-page portfolio. Main content lives in `content/_index.md`. Layout templates are in `layouts/`, with shared HTML in `layouts/partials/`. Static assets such as CSS and JavaScript live in `static/`. Hugo configuration is in `hugo.toml`. Local preview and build helpers are defined in `docker-compose.yml`. Generated output goes to `public/` and must not be committed.

## Build, Test, and Development Commands

- `docker compose up`: starts the local Hugo dev server at `http://localhost:1313`.
- `docker compose run --rm hugo --minify`: builds the production site into `public/`.
- `docker compose config`: validates the Compose file configuration.

Use Docker Compose by default; do not assume a local Hugo binary is installed.

## Coding Style & Naming Conventions

Use 2-space indentation in YAML, HTML templates, and CSS. Keep Hugo templates simple and data-driven; prefer editing `content/_index.md` over hardcoding copy in templates. Use lowercase, descriptive keys in front matter such as `hero`, `metrics`, `projects`, and `contact`. Keep CSS class names readable and component-oriented, for example `.project-card` or `.site-header__inner`.

## Testing Guidelines

There is no automated test suite yet. The required validation is:

- run `docker compose run --rm hugo --minify`
- confirm the build completes without errors
- review the home page in desktop and mobile widths

When changing copy structure or template fields, verify the generated `public/index.html` renders the expected sections and links.

## Commit & Pull Request Guidelines

Follow Conventional Commits. Example: `feat: update portfolio case studies` or `fix: adjust header layout`. Keep commits scoped to one change set.

Pull requests should include:

- a short summary of what changed
- screenshots for visible UI changes
- notes about content/schema changes in `content/_index.md`
- confirmation that the Hugo build command passed

## Content & Configuration Notes

Do not commit `public/`, `.hugo_build.lock`, or local helper files listed in `.gitignore`. Keep `profile.pdf` untracked unless there is an explicit reason to version it. Use real contact data only when confirmed.
