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

## Why the keys are not in this repo

This repo is public and has a **Download ZIP** button. A key committed here
ships with the documents, to anyone, forever.

So keys live with the engine, one file per site, and that file is the single
place to edit them.

It also lands on the split this whole family uses: the **table name** (`crew`)
is shared vocabulary and belongs with the content, the **keys** are local and
belong with the site config. Two sites can both have a `crew` table with
different codes, which is correct, because they are different people.

## The value on the right is an id

```yaml
loadin24: crew-call-sheet     # a page id
loadin24: /crew/call-sheet/   # NOT a path
```

Same promise as every other link here: the destination can be moved, renamed or
reorganised and the route still works. A key pointing at an id that does not
exist is reported in the build report, so you find out at build time instead of
when somebody types it.

## Pair it with `status: unlisted`

A router pointing at a page that is already in the sidebar is a router with
nothing to do. Set the destination to [unlisted](@publication) so it has a live
URL but does not appear in navigation or search.

Not enforced — sometimes a destination is deliberately public — but it is the
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
**keys**, not passwords — because "gate" implies a wall, and somebody would
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

- [Publication states](@publication) — `unlisted`, and the honest limits
- [Markers](@markers) — the other inline tool, for confidence rather than routing
