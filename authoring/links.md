---
id: links
title: Links
type: page
status: public
order: 20
revised: 2026-08
summary: Every kind of reference -- pages, headings, sibling sites, images, data tables and markers -- and why none of them name a file path.
---

# Links

Internal links name a page's `id`, never its file path. That single decision is
why reorganising this repository cannot break it.

**The same idea covers images, data tables and markers.** Everything below names
a thing; nothing below names a location.

| Write | Reaches |
| --- | --- |
| `[Main Stage](@main-stage)` | a page in this site |
| `[the notes](@main-stage#venue-notes)` | a heading on it |
| `[the rep plot](@oph:rep-plot)` | a page on a sibling site |
| `![alt](@img:h5-front)` | an image anywhere in this site |
| `[the schedule](@data:circuit_schedule)` | a data table on this page |
| `[ETC](@term:etc)` | a defined term, styled as terminology |
| `[fkWeek](@rel:table-weeks)` | a relationship, styled as schema |
| `[dateFormat](@calc:table-workdays#calc-fmt)` | a calculation, at its heading |
| `[Producers](@vl:table-value-lists)` | a value list |
| `[create_EDITION](@script:script-create-edition)` | a script |
| `[Print Menu](@layout:layout-print-menu)` | a layout |
| `[fkCal](@alias:table-workdays#calc-fkCalendar)` | a retired name for a live one |

The last six are **marker link forms**: they resolve like any other reference and
also carry their marker's colour. Each one has a plain span twin for when there
is nothing to point at. See [Markers](@markers).

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

⚠️ **A peer site may not be named after a prefix.** If a sibling were slugged
`rel`, the prefix would win and every link to that peer would stop resolving.
The build reports the collision. This is worth knowing because the list of
prefixes now **grows with a data edit** -- adding a marker link form can newly
collide with a peer that has been fine for months.

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

## Which prefixes take an `#anchor`

~~**A prefixed reference takes no `#anchor`.** It parses, it resolves, and the
anchor is silently discarded -- you get a correct-looking link to the top of the
right place. The build reports it. Only a plain `@id` to a page carries an
anchor.~~

**Struck 2026-08-09.** That was true of every prefix for four days and is now
true of only some, so it is left visible rather than rewritten: it is exactly the
kind of limitation a reader remembers and designs around, and quietly deleting it
would leave people avoiding something that works.

**It depends on what the prefix ADDRESSES**, which is the honest version of the
rule and always was:

| Prefix | Anchor | Because |
| --- | --- | --- |
| plain `@id` | ✅ carried | a page has headings |
| `@peer:` | ✅ carried | so does a page on a sibling site |
| `@calc:` `@rel:` `@vl:` `@script:` `@layout:` `@alias:` `@term:` | ✅ carried | these address a **page**, and the thing you mean may be a heading on it |
| `@data:` | 🚫 dropped, reported | addresses a whole TABLE. There is nowhere for a fragment to point |
| `@img:` | 🚫 dropped, reported | addresses a whole PICTURE. Same |

⭐ **`@calc:` is the one that NEEDS it.** A calculation has no page of its own --
it lives at a heading on its table's page -- so the fragment is not an
embellishment, it is half the address:

```markdown
[dateFormat_Colloquial](@calc:table-workdays#calc-dateFormat_Colloquial)
```

Write the target heading's anchor **explicitly** (`### name {#calc-name}`). An
automatic heading anchor is derived from the heading text and lowercased, so
retitling the heading breaks every inbound link while both ends still look fine.
See [Markers](@markers) for the convention.

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

⚠️ **A marker link that does not resolve stays a broken link.** It never quietly
falls back to the underlineless span form -- that would be a second legal way to
write a reference that failed, and *which of these still have no page* would stop
being answerable.

## Never use a full URL for an internal page

A hardcoded `https://` link to another page in this family will not be checked,
will not be reported when it breaks, and will not survive the site moving. Use
the id.

## Related

- [The gold standard](@audit) -- the frontmatter block and the audit checklist
- [Markers](@markers) -- every marker family, both forms, and where a calc
  definition goes
