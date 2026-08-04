---
id: frontmatter
title: Frontmatter
type: page
status: public
order: 10
revised: 2026-08
summary: The block at the top of every page, and the entire interface between what you write and what the renderer does.
---

# Frontmatter

## The full shape

```yaml
---
id: main-stage          # IDENTITY. Permanent. Set once, never change.
title: Main Stage       # what humans see
type: space             # WHICH KIND OF THING this page is
status: public          # hidden | unlisted | gated | public
summary: The 500-seat proscenium house, and what it takes to work in it.
parent: example-house   # the id of its container, never a path
order: 10               # sidebar weight. Absent sorts alphabetically.
indexed: false          # keep out of the parent index page's contents list
theme: utility          # optional skin override
related: [studio]       # ids
also_known_as: [the big house]   # other names, rendered visibly at the foot
revised: 2026-08        # when this was last true
---
```

## The five classes of field

**Identity** (`id`, `title`). `id` is a promise. Moving the file, renaming its
folder or retitling the page cannot break an inbound link, because none of
those is what a link points at. That promise only holds if the id never
changes.

**Classification** (`type`, `parent`). `type` is the interesting one: it says
what kind of thing this page *is*, which is what lets the renderer decide how
to draw it. `parent` is an id, which turns a flat pile of files into a graph.

**Render flags** (`status`, `order`, `indexed`, `theme`). The only fields whose
job is purely presentational or gating.

**Provenance** (`revised`, `source`). Who to believe, and when it was last
true.

**Content** (`summary`, `also_known_as`). The odd ones out, and worth naming as
their own class: everything above is an instruction to the machine, and these
two are text a reader reads. They are up here rather than in the body because
both are needed *away* from the page -- in a search result, in a sidebar
preview, in another site's index -- and a fact that has to travel cannot live
in the prose.

## Required, always

`id`, `title`, `status`, `summary`. A page missing any of them is reported by
name in the build log. A page missing `status` is not built at all, and a page
missing `summary` shows up in search with nothing under its title.

## `summary` is the lede

One or two lines: what this is and who needs it. It renders large and light
directly under the H1, and it is what a search result shows.

**Do not also write a paragraph under the H1.** That used to be the lede -- the
renderer took whatever paragraph happened to sit there -- and it is now a
reported defect. A page with both renders the same thought twice, once as the
lede and once as ordinary body text immediately below it.

!!! note "Why it moved out of the body"

    Because three separate things decided what the lede was, in three
    different languages, and none of them agreed once a page opened with
    anything other than exactly one paragraph. The stylesheet looked for the
    paragraph element after the H1, the renderer looked for the first non-blank
    run of lines, and the search plugin took everything before the next
    heading. Nothing checked any of it, so a page that opened with a callout or
    a table quietly had no lede and nobody found out.

    A field cannot be in the wrong place.

## `also_known_as` is for the words that are not on the page

A list of other names for the same thing. It renders as a quiet line at the
foot -- *Also called: genie, personnel lift, MEWP* -- which is exactly how it
reaches search: **the words are indexed because they are genuinely on the
page.**

That is the whole design, and the rejected alternative explains it. A hidden
keywords block does the same job invisibly, and a field nobody can see is a
field nobody can audit: it rots, and the first symptom is a search that quietly
stopped matching a term it used to find.

Use it for jargon that differs from house vocabulary, not for stuffing. The
search already indexes the entire body of every page; this is only for words
that are genuinely absent from it.

## Types add their own requirements

Each type declares what it needs. A `space` requires `parent`, because a room
that does not say which building it is in is a fact with nowhere to live.

| Type | Requires | Draws |
| --- | --- | --- |
| `page` | the base four | nothing extra |
| `index` | the base four | the section contents, at the foot |
| `venue` | the base four | address, city, operator |
| `space` | `parent` | capacity, dimensions, grid height, power, seating, rigging |
| `standard` | the base four | applies to, authority, review cycle |
| `procedure` | the base four | owner, frequency, trigger, systems |
| `reference` | the base four | maintainer |

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

`indexed:` is a CHILD deciding whether to appear in one:

```yaml
indexed: false    # stay in the sidebar and in search, out of the list
```

The default is `true`, so writing it changes nothing and is only worth typing
if you want the intent on the record. It is not an override: it will not force a
page into the list when your prose already links it, because that would print
the same link twice on one page.

Three different things keep a page out of that list, and they are worth telling
apart:

| | Sidebar | Search | Index list |
| --- | --- | --- | --- |
| `status: unlisted` | no | no | no |
| `indexed: false` | **yes** | **yes** | no |
| linked from the body | yes | yes | no, it is filed already |

So `indexed: false` is for something real but peripheral that would clutter a
section's front door. If you want it gone from the sidebar too, that is
`status: unlisted` and you do not need both. See
[Publication states](@publication).

!!! warning "Three things here are called an index. `indexed:` means one of them"
    It refers to the contents list on the index **page** above this one, and
    nothing else.

    It does **not** remove the page from `doc-index.json`, the file every other
    site in the family reads to resolve `@peer:id` links. The page is still
    published there, and it has to be, or cross-site links to it would break.

    It does **not** touch the search index either. That is `status: unlisted`.

    A page with `indexed: false` is still listed in the sidebar, still
    searchable, still linkable from anywhere, and still a public URL.

## Why the tables are generated

Because a table typed by hand is a table that drifts. Thirty spaces written by
hand over two years produce thirty slightly different tables, and none of them
can be compared to any other. Declaring the fields once means adding a field to
every space in the family is one line in one file.
