---
id: frontmatter
title: Frontmatter
type: page
status: public
order: 10
revised: 2026-08
---

# Frontmatter

The block at the top of every page. It is the entire interface between what you
write and what the renderer does, which is why nothing else in this repository
needs to speak to the machine.

## The full shape

```yaml
---
id: main-stage          # IDENTITY. Permanent. Set once, never change.
title: Main Stage       # what humans see
type: space             # WHICH KIND OF THING this page is
status: public          # hidden | unlisted | gated | public
parent: example-house   # the id of its container, never a path
order: 10               # sidebar weight. Absent sorts alphabetically.
theme: utility          # optional skin override
related: [studio]       # ids
revised: 2026-08        # when this was last true
---
```

## The four classes of field

**Identity** (`id`, `title`). `id` is a promise. Moving the file, renaming its
folder or retitling the page cannot break an inbound link, because none of
those is what a link points at. That promise only holds if the id never
changes.

**Classification** (`type`, `parent`). `type` is the interesting one: it says
what kind of thing this page *is*, which is what lets the renderer decide how
to draw it. `parent` is an id, which turns a flat pile of files into a graph.

**Render flags** (`status`, `order`, `theme`). The only fields whose job is
purely presentational or gating.

**Provenance** (`revised`, `source`). Who to believe, and when it was last
true.

## Required, always

`id`, `title`, `status`. A page missing any of them is reported by name in the
build log, and a page missing `status` is not built at all.

## Types add their own requirements

Each type declares what it needs. A `space` requires `parent`, because a room
that does not say which building it is in is a fact with nowhere to live.

| Type | Requires | Draws |
| --- | --- | --- |
| `page` | the base three | nothing extra |
| `venue` | the base three | address, city, operator |
| `space` | `parent` | capacity, dimensions, grid height, power, seating, rigging |
| `standard` | the base three | applies to, authority, review cycle |
| `procedure` | the base three | owner, frequency, trigger, systems |
| `reference` | the base three | maintainer |

An undeclared type falls back to `page` and is reported. It does not break the
build.

## Why the tables are generated

Because a table typed by hand is a table that drifts. Thirty spaces written by
hand over two years produce thirty slightly different tables, and none of them
can be compared to any other. Declaring the fields once means adding a field to
every space in the family is one line in one file.
