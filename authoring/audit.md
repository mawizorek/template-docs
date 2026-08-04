---
id: audit
title: The gold standard
type: page
status: public
order: 5
revised: 2026-08
summary: One block to copy into a new page, and one checklist to audit an old one.
---

# The gold standard

Everything here is a pointer: the rules live in the guides this page links to,
never in two places.

## The block

Paste it, **delete every line you do not need**, delete the comments.
Order is the spec: what is above the first divider is mandatory, everything
below is not.

```yaml
---
# REQUIRED. No status, no page. No id, no links. No summary, no search result.
id: kebab-case-forever          # set once, NEVER change it
title: What A Human Reads
status: hidden                  # hidden -> unlisted -> public
type: page                      # page index venue space standard procedure reference
summary: One or two lines. THE LEDE. Not a paragraph under the H1 any more

# REQUIRED BY TYPE. Delete unless the type above needs it.
parent: building-id             # `space` only

# OPTIONAL. Any of these, in any combination, or none.
order: 10                       # plain integer, unquoted, NO leading zero
revised: 2026-08
theme: eos
related: [some-id, another-id]
source: https://where-the-facts-came-from
also_known_as: [genie, personnel lift, MEWP]   # renders visibly at the foot

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

## First real section
```

The four kinds of field, and why the tables under them are generated, are in
[Frontmatter](@frontmatter). Do not re-derive them here.

## Body shape

Not every page has every part. When a page **does** have one, it looks like this
and sits in this order:

| Order | Section | Rule |
| --- | --- | --- |
| 1 | `# Title` | Exactly one H1. **No paragraph under it** -- that is `summary:` |
| 2 | *generated* | The lede, then any spec table. Do not type either |
| 3 | Body `##` sections | Whatever the page is for |
| 4 | `## Related` | Last section. Bare list of `@id` links, one line each |
| 5 | *generated* | An index page's contents list, then the aka line |

Two things that are always true and cause most of the trouble:

- **Blank line between every block.** Paragraphs, lists, headings, tables.
  GitHub's preview is more forgiving than the renderer here: a list that
  interrupts a paragraph works there and silently does not work on the site.
- **Callout bodies indent four spaces.** See [Writing a page](@writing).

## Audit checklist

Ten questions per file. Anything that fails is in the build report by name, so
the report is the fast version of this list.

1. `id`, `title`, `status`, `summary` all present? A page missing `status` **is
   not built**; a page missing `summary` has no text in its search result.
2. Is the lede in `summary:` and NOT also sitting as a paragraph under the H1?
   Both is worse than either -- the page says the same thing twice, once large
   and once normal.
3. Is `id` kebab-case, and unchanged since it shipped?
4. Any key written **twice**? YAML keeps the last one silently. This is the
   single nastiest failure available here.
5. Does `type` match what the page is *about* -- not where the file sits? An
   `index.md` that is a building is a `venue`. See [Frontmatter](@frontmatter).
6. `space` pages: is `parent` set, and is it an **id**?
7. Every internal link an `@id`, never a path or an `https://` to our own site?
   See [Links](@links).
8. `order:` an unquoted integer **with no leading zero**? `"10"` and `1.5` both
   sort as absent. So does `08`: YAML reads a leading zero as octal, `08` is
   not valid octal, and it silently becomes the string `"08"`. `01` through
   `07` work by accident, which is what makes the habit dangerous.
9. Uncertain values carrying a [marker](@markers) rather than a bare TBD?
10. Any of the dead keys below still in the header?

## Keys that look real and do nothing

Delete on sight. None of these is read by any code in the engine, so a page
using one behaves exactly as though the line were absent -- which is
indistinguishable from the feature being broken.

| Dead | What to write instead |
| --- | --- |
| `gate:` | Nothing. It was never implemented. Use `router:` |
| `listed:` | `indexed:` |
| `keywords:` | `also_known_as:` |
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
