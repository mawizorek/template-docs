---
id: publication
title: Publication states
type: page
status: public
order: 30
revised: 2026-08
---

# Publication states

Four values for `status`. One of them is not what it appears to be, and this
page says so plainly rather than letting somebody find out the hard way.

## The four

| Status | Built | In nav | In search | Notes |
| --- | --- | --- | --- | --- |
| `hidden` | no | no | no | URL 404s. **Start here.** |
| `unlisted` | yes | no | no | Live URL, shareable by link |
| `gated` | see below | see below | see below | **Not implemented** |
| `public` | yes | yes | yes | Done |

Start every page at `hidden` and promote it deliberately. A page nobody has
finished writing is a page nobody should be reading.

`unlisted` is the right state for a page that exists to be linked TO rather than
found: a revision log, a form, a one-off handout. It stays reachable by `@id`
from anywhere, and an `@id` link to it is not broken.

!!! warning "`unlisted` did not work until 2026-08-03"
    It removed a page from search and left it in the sidebar, because the
    renderer set a Material page property that hides the sidebar *on* a page
    rather than removing that page *from* the sidebar. Nav membership is not a
    page property in Material at all: the tree has to be edited. If you set a
    page unlisted before that date and it stayed in the sidebar, that was the
    bug and it is fixed. Republish.

## Removing a whole folder from the sidebar

There is no folder-level switch. Set every page in the folder to `unlisted` and
the section disappears on its own, because a section with no listed pages left
is dropped rather than rendered as a heading that expands to nothing.

The build report names any section it removes this way. That is deliberate: the
usual cause is one page changing status and taking its entire folder off the
sidebar with it, which is a bigger effect than the edit looked like.

## There is no cascade

**Every page carries its own `status:`, and nothing reads its parent's.** A
folder's `index.md` does not set the state of the pages under it.

This page previously claimed the opposite -- that access cascaded down and the
most protective statement won. That was never implemented. It is written here
as a retraction rather than quietly deleted, because the sentence was wrong in
the most expensive direction available: somebody could set a folder index to
`hidden`, believe the pages under it were covered, and publish all of them.

`theme:` genuinely is inherited, and a page's own value beats its folder's.
Being overridable is right for appearance and wrong for access, which is why
the two are not built the same way.

## Keeping a page out of an index list only

`indexed: false` is a different lever and does not touch publication:

```yaml
---
id: rehearsal-studio
title: Rehearsal Studio
status: public
indexed: false
---
```

That page stays in the sidebar and stays searchable. It just does not appear in
the generated contents list of the [index page](@frontmatter) above it. Use it
for something real but peripheral that would clutter a section's front door.
The default is `true`.

An `unlisted` page is already left out of those lists, so the two never need to
be combined.

!!! warning "`indexed: false` is not a privacy setting"
    It hides one list of links on one page. The page stays in the sidebar,
    stays in search, stays in `doc-index.json`, and stays a public URL. If you
    want it out of the sidebar, that is `status: unlisted` -- and read the rest
    of this page before assuming that means protected either.

## About `gated`

**It is not implemented, and a page declaring it is published as `unlisted`
with a warning in the build log.**

That is a choice, not an oversight. A gate that looks like access control but
is not is more dangerous than no gate at all, because people put things behind
it. The limits that would apply even to a real implementation:

- a browser-side password ships to the reader inside the page it protects;
- publication states control what reaches the **site**, never what is readable
  in the repository, which is public;
- **a GitHub Pages site is publicly reachable even when its repository is
  private.** Privately published Pages requires GitHub Enterprise Cloud.

## So the actual rule

Before writing anything, in any repo in this family: **if a stranger read this
page, would it matter?**

If yes, it does not belong in a doc repo. It belongs somewhere with real
authentication in front of it. An unlisted URL is obscurity, and a crawler does
not need to be told where to look.
