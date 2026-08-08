---
id: markers
title: Markers
type: page
status: public
order: 45
revised: 2026-08
---

# Markers

Inline tags. They sit inside a sentence, because what they are about is usually
one value rather than the whole paragraph.

```markdown
The second altered curtain is not named: [To be confirmed]{.tbc}
Cyc width [40'-0"]{.conf}, previously [48'-0"]{.was}
A [source 4]{.term} is an ERS fixture
The key is in [the SM office]{.hi}
```

Used bare, a marker prints its own label:

```markdown
Grid height: {.gap}
```

## Three families

Every marker belongs to a **family**, and the family is what decides the colour.
This matters more than it looks: the build report groups by family, so *what is
still unconfirmed across this site* stays answerable no matter how many terms or
highlights a page carries.

### Confidence -- how much to trust the value beside it

| Marker | Means | Use it when |
| --- | --- | --- |
| `{.tbc}` | To be confirmed | You wrote it down but have not checked it against a source |
| `{.verify}` | Verify on site | Recorded once, never re-checked. Measure before building to it |
| `{.gap}` | Not recorded | This fact should exist and does not. The absence is **known** |
| `{.conf}` | Confirmed | Double-checked against the real thing. Trust it |
| `{.est}` | Estimate | Approximate. Plan with it, do not cut to it |
| `{.was}` | Superseded | The old value, kept so old paperwork can still be matched up |

### Terminology -- a defined word

| Marker | Means |
| --- | --- |
| `{.term}` | House terminology, with or without a page behind it |

Where the word has a page, write it as a link instead and it resolves:
`[ETC](@term:etc)`. Same colour, same weight; the underline is the only
difference a reader sees, and it means what underlines always mean. See
[Links](@links).

### Highlight -- worth your attention

| Marker | Means |
| --- | --- |
| `{.hi}` | Look here. Says nothing about whether the value is right |

This one is a highlighter, and it is the only one that is. It exists because
sometimes you want an eye drawn to a sentence without making a claim about it.

⚠️ **It is not a quiet `{.tbc}`.** If you mean *I have not checked this*, say
that -- the confidence markers are counted as doubt and `{.hi}` is not, so a
highlight used to mean uncertainty is a doubt that never appears in the report.

## They are not all one category any more

They were, for a long time, and this page said so: *"every marker answers how
much should I trust this -- nothing else. They are not highlighters and they are
not decoration."*

That was true when there were six, it stopped being true when terminology
arrived, and `{.hi}` is now a highlighter in as many words. Corrected rather than
deleted, because it was a real rule and anybody who read it will remember it.

**What replaced it is the family, not a free-for-all.** The old rule was
protecting the build report -- a mixed bag of markers cannot answer one question.
Families protect the same thing better, because the report groups by family and
each family answers its own question.

The bar for a new one is unchanged in spirit: **could a reader confuse it with
something already here?** Six distinguishable markers still beat twelve that all
vaguely mean *careful*.

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

Every marker on the site is **listed in the build report, grouped by family** and
named by page. So *what is still unconfirmed across this entire site* is a
question with an answer, and it shows up every time you [preview](@publishing).

It is listed as inventory, not as an error -- a page full of markers is still a
clean build. Marking your doubts is good practice, not a defect.

It also means a verification pass is **finishable**: walk the space, mark things
`{.conf}`, and the report tells you what is left.

## Adding one

A new **marker** is a row in `theme/markers.tsv` in the engine. A whole new
**family** is a row in `theme/marker-classes.tsv`. Neither is a code change.

A family sets the default shape (`box`, `plain`, `strike`, `soft`), the colour,
and how strongly a boxed chip is tinted. A marker row inherits all of it and can
override the shape or the colour.

**Prefer a token to a literal colour.** A token follows the theme into light mode
and across every site; a hardcoded colour is frozen where you typed it and will
be wrong on the scheme you were not looking at.

⚠️ **Two markers must never share a colour**, even across families -- they turn
up in the same sentence at the same size, and paint is the only thing telling
them apart. Callouts are the opposite and reuse colour freely, because two boxes
are never side by side in one line.

## Related

- [Frontmatter](@frontmatter) -- where required fields are declared
- [Links](@links) -- `@term:`, and every other kind of reference
- [Publishing](@publishing) -- where the marker report appears
- [Routers](@routers) -- the other inline tool, for routing rather than confidence
