---
id: template
title: The gold standard TEMPLATE
type: page
status: public
order: 99
revised: 2026-08
summary: The block, ready to copy, with every real key in the order the spec puts them.
---

# The gold standard TEMPLATE

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
xref: [peer-site:their-page-id] # a page on a SIBLING site
source: https://where-the-facts-came-from
keywords: [genie, personnel lift, MEWP, LX]    # renders visibly at the foot

# CONDITIONAL - data tables. The slot NAME must be legal for the type above.
data:
  schedule:                     # reference: schedule survey inventory_table
    file: circuit-schedule.tsv  #            revision_log catalog
    caption: Circuit schedule   # optional

# CONDITIONAL - routers. All four are one feature; see the guide.
router: [staff, pm]             # engine tables. LIST, never a repeated key
router_code: [tryme]            # written here, so public. throwaway only
router_prompt: Got a code?      # DEAD unless one of the two above is present
router_inherit: false           # only if a parent folder declares a router

# CONDITIONAL - index lists. Opposite ends of one relationship.
contents: auto                  # THIS page lists its children (non-index types)
indexed: false                  # keep THIS page out of its parent's list

# CONDITIONAL - the sidebar. index.md ONLY. Anywhere else it is reported.
nav: collapse                   # collapse | expand | hide (-ed forms also work)
                                # the ROOT index.md sets the site-wide default
---

# Page Title

## First real section
```

## What is NOT a header key

The shortest way to get this right. **A key earns its place only if the value is
needed AWAY from the page it appears on.** Everything else is prose, or a column
in a TSV.

Removed on 2026-08-03 for failing that test, and listed here because they read
like obvious metadata and are not: `capacity` `dimensions` `grid_height` `power`
`seating` `rigging` (a room's facts) · `address` `city` `operator`
`access_notes` (a building's) · `owner` `frequency` `trigger` `systems` (a
procedure's) · `applies_to` `authority` `review_cycle` (a standard's) ·
`maintainer` `updated_by`.

Nothing off the page ever read them. They were prose wearing a header's clothes.

## Renamed keys still get reported

| Old | New | When |
|---|---|---|
| `listed` | `indexed` | 2026-08-03 |
| `also_known_as` | `keywords` | 2026-08-04 |

A rename is the one change a reader of the page cannot see: the old key is valid
YAML, so it parses, gets ignored, and the behaviour silently reverts. **Every
retired key is named in the build report until nobody uses it.**

Two things that are always true and cause most of the trouble:

- **Blank line between every block.** Paragraphs, lists, headings, tables.
- **Callout bodies indent four spaces.** See [Writing a page](@writing).

!!! danger "`status: gated` is not a gate"

    It is **not implemented**. A page declaring it is published as `unlisted`
    with a warning in the build log: a live URL, absent from the sidebar, and
    not protected in any way. A `gate:` key beside it does nothing at all.

!!! warning "`nav:` is not a gate either"

    `nav: hide` takes a folder's pages out of the sidebar and leaves them
    built, live, linkable and **searchable**. It is a curtain over one surface.
    See [Publication states](@publication) for which lever costs what.

## Related

- [The gold standard](@audit)
- [Frontmatter](@frontmatter)
