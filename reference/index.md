---
id: reference
title: Reference
type: reference
status: public
order: 0
maintainer: Site owner
revised: 2026-08
---

# Reference

Pages that get looked up rather than read.

## Glossary

**Content repo** -- a repository holding markdown and nothing else. One per
site. Its Download ZIP button hands you exactly the documents.

**Engine** -- the renderer, in its own repository. It knows about every content
repo; no content repo knows about it.

**Instance** -- one small config file in the engine describing one site: name,
URL, content repo, palette, section order. Adding a site means adding an
instance, not forking anything.

**Type** -- what kind of thing a page is. Declared in frontmatter, defined in
the engine, and responsible for drawing the page's generated table.

**Peer** -- another site in the family, linkable with `@slug:page-id`.

**doc-index.json** -- published at the root of every site, listing its page
ids. This is the file that makes cross-site links possible, which makes it the
one output other people's builds depend on.

## Deliberately empty

This site has no contacts page and no revision history, because it has no
readers to contact and its history is the git log. A real site would have both.
The absence is a choice rather than an omission, noted here so nobody adds them
out of a sense of tidiness.
