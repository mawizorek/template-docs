---
id: audit
title: The gold standard
type: page
status: public
order: 5
revised: 2026-08
---

# The gold standard

One block to copy into a new page, and one checklist to audit an old one.
Everything here is a pointer: the rules live in the guides this page links to,
never in two places.

## The block

Paste it, **delete every line you do not need**, delete the comments.
Order is the spec: what is above the first divider is mandatory, everything
below is not.

```yaml
---
# REQUIRED. No status, no page. No id, no links.
id: kebab-case-forever          # set once, NEVER change it
title: What A Human Reads
status: hidden                  # hidden -> unlisted -> public
type: page                      # page index venue space standard procedure reference

# REQUIRED BY TYPE. Delete unless the type above needs it.
parent: building-id             # `space` only

# OPTIONAL. Any of these, in any combination, or none.
order: 10                       # plain integer, unquoted. absent = alphabetical
revised: 2026-08
theme: eos
related: [some-id, another-id]
source: https://where-the-facts-came-from

# CONDITIONAL - routers. All four are one feature; see the guide.
router: [staff, pm]             # engine tables. LIST, never a repeated key
router_code: [tryme]            # written here, so public. throwaway only
router_prompt: Got a code?      # DEAD unless one of the two above is present
router_inherit: false           # only if a parent folder declares a router

# CONDITIONAL - index lists. Opposite ends of one relationship.
contents: auto                  # THIS page lists its children (non-index types)
indexed: false                  # keep THIS page out of its parent's list
---

# Page Title

One or two lines. This is the lede: it renders large, and it is also what the
search result shows.
```

The four kinds of field, and why the tables under them are generated, are in
[Frontmatter](@frontmatter). Do not re-derive them here.

## Body shape

Not every page has every part. When a page **does** have one, it looks like this
and sits in this order:

| Order | Section | Rule |
| --- | --- | --- |
| 1 | `# Title` + lede | Exactly one H1. One paragraph under it, never a list |
| 2 | *generated* | Spec tables land here by themselves. Do not type one |
| 3 | Body `##` sections | Whatever the page is for |
| 4 | `## Related` | Last section. Bare list of `@id` links, one line each |
| 5 | *generated* | An index page's contents list lands here |

Two things that are always true and cause most of the trouble:

- **Blank line between every block.** Paragraphs, lists, headings, tables.
- **Callout bodies indent four spaces.** See [Writing a page](@writing).

## Audit checklist

Nine questions per file. Anything that fails is in the build report by name, so
the report is the fast version of this list.

1. `id`, `title`, `status` all present? A page missing `status` **is not built**.
2. Is `id` kebab-case, and unchanged since it shipped?
3. Any key written **twice**? YAML keeps the last one silently. This is the
   single nastiest failure available here.
4. Does `type` match what the page is *about* -- not where the file sits? An
   `index.md` that is a building is a `venue`. See [Frontmatter](@frontmatter).
5. `space` pages: is `parent` set, and is it an **id**?
6. Every internal link an `@id`, never a path or an `https://` to our own site?
   See [Links](@links).
7. `order:` an unquoted integer? `"10"` and `1.5` both sort as absent.
8. Uncertain values carrying a [marker](@markers) rather than a bare TBD?
9. Any of the dead keys below still in the header?

## Keys that look real and do nothing

Delete on sight. None of these is read by any code in the engine, so a page
using one behaves exactly as though the line were absent -- which is
indistinguishable from the feature being broken.

| Dead | What to write instead |
| --- | --- |
| `gate:` | Nothing. It was never implemented. Use `router:` |
| `listed:` | `indexed:` |
| `hide:` / `nav:` | Nothing. `status: unlisted` removes a page from the sidebar |
| `search:` | Nothing. `status: unlisted` removes a page from search |
| `parent:` on a non-`space` | Nothing. Use `related:` |

!!! danger "`status: gated` is not a gate"
    It is **not implemented**. A page declaring it is published as `unlisted`
    with a warning in the build log: a live URL, absent from the sidebar, and
    not protected in any way. A `gate:` key beside it does nothing at all.

    If a stranger reading the page would matter, it does not belong in a doc
    repo. Read [Publication states](@publication) before deciding otherwise.

## Related

- [Frontmatter](@frontmatter)
- [Writing a page](@writing)
- [Links](@links)
- [Markers](@markers)
- [Publication states](@publication)
- [Routers](@routers)
