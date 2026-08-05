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
summary: The 480-seat proscenium house, and what it takes to work in it.
parent: example-house   # the id of its container, never a path
order: 10               # sidebar weight. Absent sorts alphabetically.
indexed: false          # keep out of the parent index page's contents list
nav: collapse           # index.md ONLY. What this FOLDER does in the sidebar.
theme: utility          # optional skin override
related: [studio]       # ids
keywords: [the big house]        # other names and search words, shown at the foot
data: [circuits.tsv]    # data files beside this page, drawn as tables
revised: 2026-08        # when this was last true
---
```

That is the whole vocabulary. **There is no field for a fact about the thing
the page is about** -- no capacity, no address, no owner, no phone number. See
the rule below; it is the most important thing on this page.

## ⭐ The rule: away from the page

> **A value belongs in frontmatter if, and only if, it is needed AWAY from the
> page it appears on.**

That is the entire test, and every field above passes it:

| Field | Where it is needed away from the page |
| --- | --- |
| `id` | every inbound link, from this site and from sibling sites |
| `title` | the sidebar, the browser tab, search results, `doc-index.json` |
| `status` | whether the page is built at all |
| `summary` | the search result, where the page's own body is not shown |
| `order` | the sidebar's sort |
| `nav` | the sidebar, on every page of the site, not just this one |
| `type`, `parent` | what kind of thing this is, published as data |
| `keywords` | words a searcher uses that the page does not |

A room's grid height fails it. So does an address, a capacity, a phone number,
an owner's name. Those are read in exactly one place -- **on the page** -- so
they are prose, and putting them in the header only hides them from the reader
while pretending to be structure.

!!! note "Seventeen fields were removed on 2026-08-03 for failing this test"

    `space` had capacity, dimensions, grid_height, power, seating and rigging.
    `venue` had address, city, operator, access_notes. `standard` had
    applies_to, authority, review_cycle. `procedure` had owner, frequency,
    trigger, systems. `reference` had maintainer, updated_by.

    Each type drew its set into a grey table at the top of the page, and two
    of them printed a *"Not documented yet"* box naming the ones a page had
    left out.

    The evidence that settled it: across the whole URITP site, **not one of the
    four `space` pages ever filled in a single one of the six fields.** The
    table rendered nothing and the callout nagged four pages for values nobody
    intended to put in a header. A field set that goes a year unpopulated is
    not waiting for content.

    Michael, ruling on it: *"they're slop and not real metadata."*

**Where those facts go instead.** In a sentence, if there are a few of them. In
a TSV beside the page, declared with `data:` and placed with a
`<!-- dr:table -->` marker, if there are enough to want a grid. The engine had
already made this call for the data files: *a table of dimmer circuits is not
machinery, it IS the documentation.* A grid height is the same kind of thing.

## The four classes of field

**Identity** (`id`, `title`). `id` is a promise. Moving the file, renaming its
folder or retitling the page cannot break an inbound link, because none of
those is what a link points at. That promise only holds if the id never
changes.

**Classification** (`type`, `parent`). What kind of thing this page is, and
what contains it.

**Render flags** (`status`, `order`, `indexed`, `nav`, `theme`, `contents`,
`data`). Instructions to the build.

**Provenance** (`revised`, `source`). Who to believe, and when it was last
true.

`summary` and `keywords` are the two that are genuinely text a reader reads,
which makes them look like a fifth class. **They are not a licence for more.**
Both are up here for the same narrow reason: each is needed somewhere the
page's body is not available. Anything that does not clear that bar is prose.

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

## `keywords` is for the words that are not on the page

Other names for the same thing, and the words somebody would search for that
the page never says. It renders as a quiet line at the foot -- *Also called:
genie, personnel lift, MEWP* -- which is exactly how it reaches search: **the
words are indexed because they are genuinely on the page.**

That is the whole design, and the rejected alternative explains it. A hidden
keywords block does the same job invisibly, and a field nobody can see is a
field nobody can audit: it rots, and the first symptom is a search that quietly
stopped matching a term it used to find.

Use it for jargon that differs from house vocabulary, not for stuffing. The
search already indexes the entire body of every page; this is only for words
that are genuinely absent from it.

!!! warning "It was called `also_known_as` until 2026-08-04"

    The old key is valid YAML, so a page still using it parses fine, is
    silently ignored, and loses the line at the foot -- which looks exactly
    like the feature being broken. Every page still carrying it is named in
    the build report until nobody is.

    The name widened what belongs here, which was the point rather than a side
    effect: `also_known_as` could only honestly hold aliases, and `keywords`
    also holds search words that are not names at all -- a lighting page
    wanting `LX` and `electrics`. The rendered label moved for the same reason.

## `nav` is what a FOLDER does in the sidebar

**On an `index.md`, and nowhere else.** A `nav:` on a leaf page does nothing
and the build report says so by name.

| Value | Alias | The sidebar |
| --- | --- | --- |
| `collapsed` | `collapse` | a closed row you click to open |
| `expanded` | `expand` | opens by itself, and so does everything under it |
| `hidden` | `hide` | the folder keeps its row and loses its children |

**The branch you are IN is always open, whatever it says.** That is Material's
own behaviour and the engine is built never to remove it. So `collapsed` on a
folder you are standing inside does nothing, and `hidden` is the value that
empties a sidebar you are looking at.

### The site root declares the default

This is the part that is not like any other key on this page: **a folder's
value can come from a different file.**

The repo's top-level `index.md` sets what every folder inherits. Flipping the
whole site between open and shut is one line there, in the content repo that
owns the question -- not a setting in the engine four sites share.

```yaml
# index.md at the root of the content repo
nav: collapsed   # every folder starts shut unless it says otherwise
```

A root index with no `nav:` collapses and is **reported**, in its own section
of the build report. That is deliberate: on a folder, silence means *whatever my
parent said*, which is the feature. On the site index there is no parent, so
silence means nobody ever answered a question about every folder on the site.

🚫 **`nav: hidden` on the site root is refused, out loud.** Inherited by every
top-level folder it renders a sidebar of bare labels with nothing under any of
them. The build reports it and uses `collapsed`. Put `hidden` on the individual
folders you meant.

### The cascade, and where it stops

`expanded` flows down until a descendant index says otherwise. That is the
whole reason the key has three values instead of being a boolean:

```
production/index.md          nav: expanded    opens
production/crew/index.md     (nothing)        opens, inherited
production/archive/index.md  nav: collapsed   stops here
```

`hidden` does not cascade, and does not need to: the whole subtree leaves the
sidebar in one cut, so there is nothing underneath for an inherited value to
reach.

!!! warning "`expanded` anywhere turns pruning off for the WHOLE site"

    Material's `navigation.prune` renders only the ancestors and siblings of
    the page you are on. Every other section arrives with no children at all,
    so opening one would open an empty box -- the control would work perfectly
    and produce nothing.

    So the engine drops pruning from the build the moment anything resolves to
    `expanded`, and says so in the report. The cost is that every page then
    ships the whole nav tree: **~33% of page weight**, Material's own figure.

    It is **not available per-subtree.** Pruning is one boolean for the entire
    theme. A site that never writes `expanded` never pays, and `nav: hidden`
    claws a large part of it back, which is why both live in one key.

### It is a curtain, not a lock

A `hidden` folder's pages are still built, still have live URLs, still resolve
by `@id`, and are **still in search**. `nav:` changes what a reader is OFFERED;
`status:` changes what reaches the site at all. See
[Publication states](@publication), including the table of which lever costs
you what.

## Types

| Type | Requires | Draws |
| --- | --- | --- |
| `page` | the base four | nothing |
| `index` | the base four | the section contents, at the foot |
| `venue` | the base four | nothing |
| `space` | `parent` | nothing |
| `standard` | the base four | nothing |
| `procedure` | the base four | nothing |
| `reference` | the base four | nothing |

An undeclared type falls back to `page` and is reported. It does not break the
build.

!!! warning "Only `index` still draws anything, and that is an open question"

    Since the field removal, five of the seven types are `page` with a
    different label. A type earns its existence by having fields or a way of
    drawing, and these currently have neither.

    They are kept for now because a `type` is still published in
    `doc-index.json`, so it says something true about a page to anything
    reading these docs as data -- and because retiring one would make every
    page using it report an undeclared type. Whether that is enough to justify
    five names is not settled.

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

!!! note "`nav:` follows the FILENAME, not the type"

    A folder index typed `venue` still speaks for its folder's sidebar
    behaviour, and a root `index.md` typed `reference` still sets the site
    default. The engine reads the filename, exactly as it does for the other
    three index behaviours above.

    Worth knowing because the type declaration is where a reader looks for the
    list of legal keys, and `nav` is declared on `index` only.

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

⭐ **A `nav: hidden` folder still draws its contents list.** That is the pairing
the feature is for: the pages leave the drawer and stay on the page that is
supposed to point at them.

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
`nav: hidden` on the folder or `status: unlisted` on the page, and you do not
need both. See [Publication states](@publication).

!!! warning "Three things here are called an index. `indexed:` means one of them"
    It refers to the contents list on the index **page** above this one, and
    nothing else.

    It does **not** remove the page from `doc-index.json`, the file every other
    site in the family reads to resolve `@peer:id` links. The page is still
    published there, and it has to be, or cross-site links to it would break.

    It does **not** touch the search index either. That is `status: unlisted`.

    A page with `indexed: false` is still listed in the sidebar, still
    searchable, still linkable from anywhere, and still a public URL.
