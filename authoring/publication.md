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

## Folders

A folder's `index.md` can set the state for everything under it. Two rules that
point deliberately in opposite directions:

- **Access cascades down and the most protective statement wins.** A locked
  folder beats a child page that declares itself public.
- **Look cascades down and the most specific statement wins.** A page's own
  `theme:` beats its folder's.

Being overridable is right for appearance and wrong for access.

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
