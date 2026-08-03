---
id: routers
title: Routers
type: page
status: public
order: 50
revised: 2026-08
---

# Routers

A page with a text field on it. Type a key, get sent somewhere. Type the wrong
thing and the router does not know what to do with you.

## Two pieces, in two places

**The page opts in**, in its frontmatter:

```yaml
---
id: crew-start
title: Crew start
type: page
status: public
router: crew
router_prompt: Got a code?
---
```

**The keys live in the engine**, in `instances/<site>/routes.yml`:

```yaml
crew:
  loadin24: crew-call-sheet
  grid: spac-main-stage
```

That is the whole setup. `router_prompt` is optional and defaults to *Enter your
code*.

## Several keys on one page

Everything pools into one field. Tables, local codes, all of it.

!!! danger "Never repeat `router:` on two lines"
    ```yaml
    router: pm
    router: crew      # the line above is GONE
    ```

    That is YAML, not this renderer: **a repeated key silently keeps the LAST
    value.** Half your tables disappear and the page looks completely normal.
    It is reported in the build log, at the top, but nothing on the page says
    so.

    **Use a list.**

```yaml
---
id: staff
status: public
router: [pm, crew, guests]        # three tables
router_code: [tryme, temp26]      # plus two local codes
router_prompt: Got a code?
---
```

That page accepts every key in all three tables plus the two written into the
page. A key defined in two different tables is reported in the build log and the
first one listed wins.

## Local codes vs remote tables

Two places a key can live, and the difference is durability, not syntax.

| | `router_code:` (local) | `router:` (remote) |
| --- | --- | --- |
| Lives in | this page | `instances/<site>/routes.yml` |
| Edit needs | one file in this repo | an engine commit |
| Can redirect elsewhere | **no** | yes |
| Visible in the ZIP | **yes** | no |

**Local is for trash. Remote is for real.** A code you are trying for an
afternoon should not require an engine commit. A code you actually hand to
people should not sit in a public content repo with a Download ZIP button on it.

A local code can only draw a curtain over the page it is written on. Sending
somebody to a *different* page needs a remote table, because that is the only
form where the destination is sealed rather than sitting in the page as plain
text.

## Durable keys: three shapes in one table

What a remote entry does is decided by its **destination**, not by any mode
flag:

```yaml
pm:
  maw:                          # PORTABLE curtain -- no destination

staff:
  staff26: staff                # PINNED curtain -- names its own page id
  loadin24: crew-call-sheet     # REDIRECT -- names a different page
```

**Portable curtain** (no value) means *curtain on whichever page uses this
table*. One entry, reusable on any number of pages, and it never has to know
their ids. This is the shape to reach for by default.

**Pinned curtain** names the id of the page it sits on. Same behaviour, tied to
one page, which is what you want when a single table holds curtains for several
different pages.

**Redirect** names a different page and sends you there.

## A router on a folder index covers the whole folder

```
production/staff/index.md      router: pm      <- declared once
production/staff/props.md                      <- inherits it
production/staff/notes/x.md                    <- inherits it too
```

The nearest ancestor wins, so a subfolder can redeclare and override rather than
stack. A single page opts out with `router_inherit: false`.

A pause that only applies to a folder's front page is a pause a reader walks
around by clicking any child in the sidebar. And it costs the reader nothing:
one code at the index opens the folder for the session.

!!! warning "Use the PORTABLE shape on anything you expect to cascade"
    A pinned curtain inherited by a child page no longer matches that page's
    id, so it is read as a **redirect back to the folder index** instead. That
    is coherent, and almost never what anybody wanted. Leave the value blank.

## The value on the right is an id

```yaml
loadin24: crew-call-sheet     # a page id
loadin24: /crew/call-sheet/   # NOT a path
```

Same promise as every other link here: the destination can be moved, renamed or
reorganised and the route still works. A key pointing at an id that does not
exist is reported in the build report, so you find out at build time instead of
when somebody types it.

## Why the keys are not in this repo

This repo is public and has a **Download ZIP** button. A key committed here
ships with the documents, to anyone, forever.

So keys live with the engine, one file per site, and that file is the single
place to edit them.

It also lands on the split this whole family uses: the **table name** (`crew`)
is shared vocabulary and belongs with the content, the **keys** are local and
belong with the site config. Two sites can both have a `crew` table with
different codes, which is correct, because they are different people.

## Pair it with `status: unlisted`

A router pointing at a page that is already in the sidebar is a router with
nothing to do. Set the destination to [unlisted](@publication) so it has a live
URL but does not appear in navigation or search.

Not enforced -- sometimes a destination is deliberately public -- but it is the
normal case.

## What this is for, and what it is not

!!! warning "A router is not a lock"

    It does not restrict anything. This site is public, the markdown is one
    click away in a public repo, and every destination is reachable by URL
    whether or not anybody typed a key.

    **Nothing belongs behind a router that would matter if a stranger read
    it.** If that is the requirement, this is the wrong tool, and the answer
    is a host with real authentication in front of it.

What it is genuinely good for:

- keeping a casual reader out of a work-in-progress corner
- handing one person a code that drops them on the page they need
- a soft *stay out of here* that costs nothing to maintain

The name is deliberate. It is a **router**, not a gate, and the keys are
**keys**, not passwords -- because "gate" implies a wall, and somebody would
eventually trust it as one.

## Why the destination is encrypted anyway

Given all that, the destination is still encrypted with the key rather than
sitting in the page as a plain string. One reason: **a plaintext destination is
not a router, it is a list of links with an input box in front of it.** Anyone
reading source would see every destination and skip the field, which defeats
the only thing the feature does.

A wrong code decrypts nothing, rather than failing a comparison, so there is no
plaintext destination in the page to read around. The wrapped destinations are
unlabelled and shuffled at build time, so their order says nothing about which
is which.

That is a real mechanism doing a modest job. It is not a security boundary, and
being honest about that is the point.

## Related

- [Publication states](@publication) -- `unlisted`, and the honest limits
- [Markers](@markers) -- the other inline tool, for confidence rather than routing
