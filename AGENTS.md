# AGENTS.md

This repository is an Obsidian vault.

## Remote

- `origin`: `git@github.com:guisaliba/brain.git` (public)

## Folder Structure

- `books/` — PDFs and reading materials
- `clippings/` — web clippings from Obsidian Web Clipper
- `images/` — images and media
- `journal/` — private journal (Git submodule, see below)
- `notes/` — personal annotations and study notes
- `reading-list/` — reading lists and learning paths

## Submodules

- `journal/` → `git@github.com:guisaliba/journal.git` (private)

`journal/` is a private Git submodule. It is managed by Obsidian Git on desktop with submodule support enabled.

## Environment Notes

On the primary Windows device, Obsidian runs on Windows while the Git repository lives in WSL2 at `/home/guisaliba/projects/brain`. The Windows vault path is `C:\obsidian_vault`. On other devices (Linux, Android), the vault and Git repo typically live in the same filesystem.

## Agent Rules

- Do not copy, summarize, or move journal content into public folders unless explicitly instructed.
- Preserve Obsidian-compatible Markdown, wikilinks, embeds, and frontmatter.
- Prefer small, direct edits.
- Do not add dependencies without a clear reason.
- Do not change Git submodule wiring unless explicitly asked.
- `.obsidian/` is intentionally ignored and should not be tracked.
