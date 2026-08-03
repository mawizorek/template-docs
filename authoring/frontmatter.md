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
listed: false           # keep out of the parent index's contents list
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

**Render flags** (`status`, `order`, `listed`, `theme`). The only fields whose
job is purely presentational or gating.

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
| `index` | the base three | the section contents, at the foot |
| `venue` | the base three | address, city, operator |
| `space` | `parent` | capacity, dimensions, grid height, power, seating, rigging |
| `standard` | the base three | applies to, authority, review cycle |
| `procedure` | the base three | owner, frequency, trigger, systems |
| `reference` | the base three | maintainer |

An undeclared type falls back to `page` and is reported. It does not break the
build.

## `index` is about POSITION, not subject

Every other type says what a page is about. `index` says where it sits: it is
the landing page of a folder, and pointing at the pages underneath it is the
whole job.

The renderer already treated `index.md` specially in three ways, all of them
triggered by the filename -- it sorts to the top of its section, it gives the
folder its title so the sidebar and the page agree on what a thing is called,
and it is the page every link on the site is resolved relative to. Declaring
the type does not change any of that. It puts the fact in the METADATA, where
`doc-index.json` publishes it and anything reading these docs as data can see
which pages are hubs without inspecting file paths.

**Not every `index.md` should be `type: index`.** Two on this site are
deliberately not:

- [Reference](@reference) is a `reference`, because it is a glossary.
- [Example House](@example-house) is a `venue`, because it is a building.

Both are the landing page of their folder, but that is an accident of where the
file sits rather than what the page is about. Type the subject when there is
one. The build does not complain either way.

### What it draws

A contents list at the FOOT of the page -- after your prose, never above it --
of the pages directly beneath this one: files in the same folder, plus the
landing page of any folder one level down. It leaves out anything the body
already links.

That last part is the whole design. A good index page is prose with a line of
explanation per link, and drawing the full list under that would duplicate
every link and teach people to skip the writing. Drawing only what is LEFT
means a curated index shows no list at all, and an unfiled page appears there
until somebody files it. See [Standards](@standards), which is fully curated
and therefore generates nothing.

The heading reads **In this section** normally, and **Also in this section**
when your prose already covered some of them.

### Two controls, and they are opposite ends of one relationship

`contents:` is the PARENT deciding whether to draw a list at all:

```yaml
contents: false   # draw nothing, ever
contents: auto    # draw it from ANY type, not just index
```

`contents: auto` is for a page that is genuinely about something and also
happens to sit above a folder of pages, like a building with its rooms in files
underneath. `false` wins over everything.

`listed:` is a CHILD deciding whether to appear in one:

```yaml
listed: false     # stay in the sidebar and in search, out of the list
```

Three different things keep a page out of that list, and they are worth telling
apart:

| | Sidebar | Search | Index list |
| --- | --- | --- | --- |
| `status: unlisted` | no | no | no |
| `listed: false` | **yes** | **yes** | no |
| linked from the body | yes | yes | no, it is filed already |

So `listed: false` is for something real but peripheral that would clutter a
section's front door. If you want it gone from the sidebar too, that is
`status: unlisted` and you do not need both. See
[Publication states](@publication).

## Why the tables are generated

Because a table typed by hand is a table that drifts. Thirty spaces written by
hand over two years produce thirty slightly different tables, and none of them
can be compared to any other. Declaring the fields once means adding a field to
every space in the family is one line in one file.
