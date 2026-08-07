---
id: links
title: Links
type: page
status: public
order: 20
revised: 2026-08
---

# Links

Internal links name a page's `id`, never its file path. That single decision is
why reorganising this repository cannot break it.

**The same idea covers images and data tables.** Everything below names a
thing; nothing below names a location.

| Write | Reaches |
| --- | --- |
| `[Main Stage](@main-stage)` | a page in this site |
| `[the notes](@main-stage#venue-notes)` | a heading on it |
| `[the rep plot](@oph:rep-plot)` | a page on a sibling site |
| `![alt](@img:h5-front)` | an image anywhere in this site |
| `[the schedule](@data:circuit_schedule)` | a data table on this page |
| `[ETC](@term:etc)` | a defined term, styled as terminology |

## Within this site

```markdown
[Main Stage](@main-stage)
[the venue notes](@main-stage#venue-notes)
```

Moving the file, renaming its folder or retitling the page cannot break either
of those, because none of those things is what the link points at.

A heading you link to needs an explicit anchor:

```markdown
## Venue notes {#venue-notes}
```

Without it the link is riding on the heading TEXT, which dies the moment
somebody rewords it. Working example: [the studio's access
notes](@studio#access).

## To a sibling site

```markdown
[the rep plot](@oph:rep-plot)
```

The part before the colon names a peer site, configured in the engine. Every
site in the family publishes a `/doc-index.json` listing its page ids, and that
is what a cross-site link resolves against.

**The honest limit:** this resolves at BUILD time, not when a reader clicks. If
a sibling renames a page, links to it stay wrong until the next build. A
nightly rebuild closes that to about a day. Closing it further would mean
running a server, which is a bad trade for a documentation archive.

⚠️ **There is no cross-site equivalent for an image.** Each site publishes a
list of its pages; nothing publishes a list of its images. Copy the file into
this repository instead of pointing at theirs -- a broken `@peer:id` is caught
while the site builds, and a broken image URL is caught by nobody.

## To an image

```markdown
![The H5 front panel](@img:h5-front){ caption="Power is on the LEFT." }
```

**The filename without its extension is the name.** `h5-front.png` is
`@img:h5-front`, wherever it sits in the tree. Nothing is declared and there is
no frontmatter key.

A plain relative path still works and is still fine for an image beside its own
page. Prefer the name once the two are apart: `../../../shared/logo.png` needs
counting that nothing checks, and it dies silently when either end moves.

⚠️ **An image name must be unique across the whole repository.** Two files with
the same name make the reference ambiguous, and the build refuses it rather
than guessing -- two pictures with one name are two different pictures. See
[The gold standard](@audit).

## To a data table

```markdown
[the circuit schedule](@data:circuit_schedule)
```

The name is the **slot** declared in this page's frontmatter, never the
filename. If the table is embedded on the page, the link jumps to it; if the
slot is declared but not placed, the link downloads the file -- which is the
honest answer, because there is nothing on the page to jump to.

## ⚠️ A prefixed reference takes no `#anchor`

```markdown
[the totals](@data:inventory#totals)     the #totals is DROPPED
```

It parses, it resolves, and the anchor is silently discarded -- you get a
correct-looking link to the top of the right place. The build reports it. Only
a plain `@id` to a page carries an anchor.

## When a link does not resolve

It renders struck through with a `[broken link]` marker and lands in the build
report. It does **not** fail the build. The same is true of an `@img:` name
that matches no file, or one that matches two.

That is a deliberate reversal of how the first version worked. Building in
strict mode meant one typo froze the entire live site -- twice in forty minutes
on one occasion -- while Pages cheerfully kept serving a stale commit and gave
no indication anything was wrong. One ugly link on one page is a far better
outcome than a site that silently stops updating.

Here is what one looks like: [a page that does not
exist](@no-such-page-anywhere).

## Never use a full URL for an internal page

A hardcoded `https://` link to another page in this family will not be checked,
will not be reported when it breaks, and will not survive the site moving. Use
the id.

## Related

- [The gold standard](@audit) -- the frontmatter block and the audit checklist
- [Markers](@markers) -- `@term:`, and confidence on a single value
