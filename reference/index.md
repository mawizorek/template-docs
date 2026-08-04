---
id: reference
title: Reference
type: reference
status: public
order: 0
summary: Pages that get looked up rather than read - the glossary for this family of sites.
revised: 2026-08
---

# Reference

Maintained by the site owner.

## Glossary

**Content repo** -- a repository holding markdown and nothing else. One per
site. Its Download ZIP button hands you exactly the documents.

**Engine** -- the renderer, in its own repository. It knows about every content
repo; no content repo knows about it.

**Instance** -- one small config file in the engine describing one site: name,
URL, content repo, palette, section order. Adding a site means adding an
instance, not forking anything.

**Type** -- what kind of thing a page is. Declared in frontmatter, defined in
the engine.

**Lede** -- the one or two lines under the title. It is the `summary:` field,
not a paragraph you type, and it is what a search result shows.

**Peer** -- another site in the family, linkable with `@slug:page-id`.

**Marker** -- an inline note on how much to trust one value, like
[to be confirmed]{.tbc}. It sits inside the sentence, so the doubt attaches to
the figure rather than the paragraph.

**Data file** -- a TSV beside a page, declared with `data:` and placed with a
`<!-- dr:table -->` marker. Where a grid of facts lives now that no type draws
one from frontmatter.

**doc-index.json** -- published at the root of every site, listing its page
ids. This is the file that makes cross-site links possible, which makes it the
one output other people's builds depend on.

## Deliberately empty

This site has no contacts page and no revision history, because it has no
readers to contact and its history is the git log. A real site would have both.
The absence is a choice rather than an omission, noted here so nobody adds them
out of a sense of tidiness.
