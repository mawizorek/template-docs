---
id: how-this-works
title: How this works
type: page
status: public
order: 2
revised: 2026-08
summary: Where everything lives - documents, machinery, configuration - and the two questions that decide where a new thing belongs.
also_known_as: [architecture, the layer map, where does this go]
---

# How this works

You do not need this page to write a page. You need it the moment you are
holding something and cannot tell which of six places it belongs in.

## Two repositories, and the arrow only points one way

| | Holds | Knows about the other |
| --- | --- | --- |
| **A content repo** (this one, and every real site) | documents | **no** |
| **The engine** (`doc-render-engine`) | all machinery, and every site's configuration | yes |

That asymmetry is the whole design. A content repo cannot name the engine, so
it can be handed to somebody, archived, printed, or pointed at a different
renderer without anything being unpicked first.

It also means **the engine holds your site's config, not your content repo.**
Colours, section order, peer sites, the router table: all in the engine, under
that site's instance folder. If you are looking for a setting and it is not in
a page's frontmatter, it is over there.

## Four layers inside the engine

Each owns exactly one kind of decision. The names are worth knowing even if you
never open them, because knowing which one a question belongs to is most of
answering it.

| Layer | Answers | Shape |
| --- | --- | --- |
| `hooks/` | **WHEN** things happen | fifteen two-line files |
| `docrender/` | **WHAT** happens | seventeen Python modules |
| `objects/` | **WHAT A PAGE IS** | eight small YAML declarations |
| `theme/` + `instances/` | **WHAT IT LOOKS LIKE**, and which site this is | TSV tables and per-site config |

### `hooks/` is order and nothing else

Every file in it is two lines. In full:

```python
from docrender.objects import on_files, on_page_markdown
```

The renderer loads hooks by file path and calls whatever it finds, so the
**filename** is the only place the running order can be expressed. The logic
lives in a package the stages can share; the numbers live here.

That is not tidiness. The order is load-bearing: frontmatter must be read before
hidden pages are pruned, and pruning must finish before links are indexed, or a
link resolves cleanly to a URL that 404s for every reader. Written as a warning
paragraph, that constraint survives until somebody reorders a list. Written as a
filename, it does not have to.

### `docrender/` is the code

One module per concern: types, the lede, links, visibility, routers, data
tables, markers, the published index, the size budget, the theme, the site
identity, the nav, the page foot, the build stamp, assets, plus two shared
helpers everything else imports.

One of them is imported by **two** hooks. `status:` is a single decision, but the
renderer forces it in two passes -- every hook's file stage runs before any
hook's nav stage -- so *built* and *listed* cannot be settled together. The
concept stays in one module; only the order is split.

### `objects/` says what a kind of page is

A base declaration plus one file per type. The base requires `id`, `title`,
`status` and `summary`. A `space` adds `parent`. **Nothing else requires
anything, and only `index` draws anything** -- the contents list at the foot of a
section landing page.

It was more than that until 2026-08-03, when seventeen fields were removed for
holding facts about a subject. See [Frontmatter](@frontmatter).

### `theme/` and `instances/` are data

Five shared tables -- colours, typography, contrast, theme names, markers --
read by every site in the family. Adding a marker or a colour is a row, not a
code change.

Then one folder per site, holding the three things that make a build *this*
site: its name and URL and peers, its own stylesheet layer, its router table.
**Four sites exist today**, and one of them has no theatre in it at all, which
is the portability claim being tested rather than asserted.

## What is inline, in your markdown

Five pieces of syntax do something beyond plain prose. Every one degrades
gracefully: a page still reads as a document in a plain markdown viewer.

| You write | It becomes |
| --- | --- |
| `[Main Stage](@main-stage)` | a link resolved by **id**, never by path |
| `[the notes](@main-stage#venue-notes)` | the same, to an anchored heading |
| `[the rep plot](@oph:rep-plot)` | a link into a **sibling site** |
| `[40'-0"]{.conf}` or bare `{.gap}` | a confidence marker, counted in the build report |
| `!!! warning "Title"` + four-space body | a callout. `???` makes it collapsible |
| `=== "Lighting"` | department tabs |
| `<!-- dr:table circuits.tsv -->` | a declared data file, drawn **here** |

The table marker is an HTML comment deliberately. It is invisible on GitHub, in
any other renderer, and in a text editor -- so a page carrying one is still an
ordinary document everywhere this engine is not involved.

Full syntax: [Writing a page](@writing) · [Links](@links) · [Markers](@markers).

## The two questions

This is the part worth remembering. Everything above is lookup; this is the
decision.

### If it is a fact

> **Is this value needed AWAY from the page it appears on?**

**Yes** -- a title in the sidebar, a summary in a search result, an id in
somebody else's link -- it is frontmatter.

**No** -- a capacity, an address, a grid height, an owner's name -- it is the
document. Write it in a sentence, or in a TSV beside the page if there is
enough of it to want a grid.

That question removed seventeen header fields in one pass. It is the sharpest
tool on this site.

### If it is machinery

> **Which decision is it?**

- **When something runs** → a hook filename
- **What it does** → a module
- **What a kind of page is** → an object declaration
- **What it looks like** → a theme table, or one site's own stylesheet
- **Which site this is** → that site's instance config

A thing that seems to need two of those usually wants splitting, and a thing
that fits none of them is usually content.

## Related

- [Frontmatter](@frontmatter) -- the header contract, and the away-from-the-page rule
- [Writing a page](@writing) -- the inline syntax in full
- [The gold standard](@audit) -- the copyable block and the audit checklist
- [Publishing](@publishing) -- how a written page becomes a visible one
