# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is the root GitHub Pages site for the `tyson-swetnam` GitHub account (served at https://tyson-swetnam.github.io/). Its sole purpose is to redirect visitors to the owner's actual home page at https://tyson-swetnam.github.io/home/, which lives in a separate repository. A personal domain (https://tysonswetnam.com/) also points at that content.

## Structure

- `index.html` — a meta-refresh redirect (plus canonical link) to https://tyson-swetnam.github.io/home/. This is the entire functional content of the site.
- `robots.txt` — fully permissive crawl policy explicitly welcoming AI/agentic crawlers (GPTBot, ClaudeBot, PerplexityBot, CCBot, etc.). Because robots.txt is only honored at the origin root, this file governs every project sub-site under tyson-swetnam.github.io (e.g. `/intro-gpt/`, `/home/`) — child repos cannot serve their own. Keep it permissive.
- `okf/` — an Open Knowledge Format (OKF) v0.2 bundle (spec: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md) for agentic AI consumption: `okf/index.md` is the bundle root (declares `okf_version`), `okf/sites/*.md` hold one concept document per child Pages site (YAML frontmatter with `type`, `title`, `description`, `resource`), and `okf/log.md` records changes. When adding or retiring a child site, update all three.
- `.nojekyll` — REQUIRED: disables Jekyll so GitHub Pages serves the OKF markdown files verbatim. Without it, Jekyll strips the YAML frontmatter and converts `.md` to HTML, breaking OKF conformance. This also makes `_config.yml` inert.
- `sitemap.xml` — static, hand-maintained (Jekyll plugins can't run with `.nojekyll`); lists the root page and OKF bundle files. Regenerate when the bundle changes.

## Development notes

There is no build step, test suite, or linter. Changes to `index.html` are deployed automatically by GitHub Pages when pushed to `main`. To preview, open `index.html` in a browser (note it will immediately redirect).

If the redirect target ever changes, update all three places in `index.html`: the `<title>`, the `http-equiv="refresh"` URL, and the `rel="canonical"` href.
