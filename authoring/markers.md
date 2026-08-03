---
id: markers
title: Markers
type: page
status: public
order: 45
revised: 2026-08
---

# Markers

Inline tags that say how much to **trust** the thing beside them. They sit
inside a sentence, because the doubt usually belongs to one value rather than
to the whole paragraph.

```markdown
The second altered curtain is not named: [To be confirmed]{.tbc}
Cyc width [40'-0"]{.conf}, previously [48'-0"]{.was}
Grid height [18'-0"]{.est} above deck
```

Used bare, a marker prints its own label:

```markdown
Grid height: {.gap}
```

## The six

| Marker | Means | Use it when |
| --- | --- | --- |
| `{.tbc}` | To be confirmed | You wrote it down but have not checked it against a source |
| `{.verify}` | Verify on site | Recorded once, never re-checked. Measure before building to it |
| `{.gap}` | Not recorded | This fact should exist and does not. The absence is **known** |
| `{.conf}` | Confirmed | Double-checked against the real thing. Trust it |
| `{.est}` | Estimate | Approximate. Plan with it, do not cut to it |
| `{.was}` | Superseded | The old value, kept so old paperwork can still be matched up |

Hover any of them on the live site for the same explanation.

## They are all one category, on purpose

Every marker answers *how much should I trust this?* — nothing else. They are
not highlighters and they are not decoration.

That constraint is what keeps the set small enough to learn in ten seconds. If
you want a seventh, the question to answer first is whether a reader could
confuse it with one of these six. **Six distinguishable markers beat twelve
that all vaguely mean "careful".**

## Why `.was` earns its place

The obvious move when a number changes is to overwrite it. Do not, when older
paperwork is still in circulation:

```markdown
| 1 | Cyc | [40'-0"]{.conf} | previously [48'-0"]{.was} |
```

Somebody holding the old sheet can now match what they have against what is
true, which they cannot do if the old figure simply vanished.

## Why `.gap` is not the same as leaving it blank

A blank cell is ambiguous: it could mean *this does not exist* or *nobody has
written it down*. `{.gap}` says the second one out loud.

That matters more than it sounds. A space with no recorded grid height looks
identical to a space with no grid, and a reader will draw the wrong conclusion
and never know they did.

## Every marker is counted

This is the part that makes them worth using rather than just typing TBD.

Every marker on the site is **listed in the build report**, grouped by type and
named by page. So *what is still unconfirmed across this entire site* is a
question with an answer, and it shows up every time you [preview](@publishing).

It is listed as inventory, not as an error — a page full of markers is still a
clean build. Marking your doubts is good practice, not a defect.

It also means a verification pass is **finishable**: walk the space, mark things
`{.conf}`, and the report tells you what is left.

## Adding one

Markers are defined in `theme/markers.tsv` in the engine — one row each, with a
label, a shape (`box`, `plain`, `strike`, `soft`), a colour, and the tooltip. No
code change.

Colour can be any theme token or a literal value. **Prefer a token**: it follows
the theme into light mode and across every site, where a hardcoded colour is
frozen where you typed it and will be wrong on the scheme you were not looking
at.

## Related

- [Frontmatter](@frontmatter) — where required fields are declared
- [Publishing](@publishing) — where the marker report appears
- [Routers](@routers) — the other inline tool, for routing rather than confidence
