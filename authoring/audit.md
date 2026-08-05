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
keywords: [genie, personnel lift, MEWP]   # renders visibly at the foot
data: [circuits.tsv]            # TSVs beside this page, placed with a marker

# CONDITIONAL - routers. All four are one feature; see the guide.
router: [staff, pm]             # engine tables. LIST, never a repeated key
router_code: [tryme]            # written here, so public. throwaway only
router_prompt: Got a code?      # DEAD unless one of the two above is present
router_inherit: false           # only if a parent folder declares a router

# CONDITIONAL - index lists. Opposite ends of one relationship.
contents: auto                  # THIS page lists its children (non-index types)
indexed: false                  # keep THIS page out of its parent's list

# CONDITIONAL - the sidebar. index.md ONLY, and nowhere else.
nav: collapse                   # collapse | expand | hide (or the -ed forms)
---

# Page Title

## First real section
```

**That is every field there is.** There is deliberately no key for a fact about
the subject -- no capacity, no address, no owner. The rule that decides what
may be added, and the seventeen fields removed for failing it, are in
[Frontmatter](@frontmatter). Do not re-derive them here.

## Body shape

Not every page has every part. When a page **does** have one, it looks like this
and sits in this order:

| Order | Section | Rule |
| --- | --- | --- |
| 1 | `# Title` | Exactly one H1, matching `title:` |
| 2 | *generated* | The lede, from `summary:`. Do not type it |
| 3 | Body `##` sections | Whatever the page is for, including its facts |
| 4 | `## Related` | Last section. Bare list of `@id` links, one line each |
| 5 | *generated* | An index page's contents list, then the keywords line |

Two things that are always true and cause most of the trouble:

- **Blank line between every block.** Paragraphs, lists, headings, tables.
  GitHub's preview is more forgiving than the renderer here: a list that
  interrupts a paragraph works there and silently does not work on the site.
- **Callout bodies indent four spaces.** See [Writing a page](@writing).

## Audit checklist

One pass per file. Anything that fails is in the build report by name, so the
report is the fast version of this list.

1. `id`, `title`, `status`, `summary` all present? A page missing `status` **is
   not built**; a page missing `summary` has no text in its search result.
2. Is the lede in `summary:` and NOT also sitting as a paragraph under the H1?
   Both is worse than either -- the page says the same thing twice, once large
   and once normal.
3. Does the H1 match `title:`? Nothing reconciles them for you, so a page that
   disagrees is called two different things depending on where you meet it.
4. Is `id` kebab-case, and unchanged since it shipped?
5. Any key written **twice**? YAML keeps the last one silently. This is the
   single nastiest failure available here.
6. **Any key holding a FACT ABOUT THE SUBJECT?** A capacity, an address, a
   phone number, an owner. It does not belong in the header, no matter how
   tidy it looks there. It is unread by everything and invisible to readers.
7. Does `type` match what the page is *about* -- not where the file sits? An
   `index.md` that is a building is a `venue`. See [Frontmatter](@frontmatter).
8. `space` pages: is `parent` set, and is it an **id**?
9. Every internal link an `@id`, never a path or an `https://` to our own site?
   See [Links](@links).
10. `order:` an unquoted integer **with no leading zero**? `"10"` and `1.5`
    both sort as absent. So does `08`: YAML reads a leading zero as octal, `08`
    is not valid octal, and it silently becomes the string `"08"`. `01`
    through `07` work by accident, which is what makes the habit dangerous.
11. Uncertain values carrying a [marker](@markers) rather than a bare TBD, and
    no dead keys from the table below still in the header?
12. Any `nav:` on a page that is **not** an `index.md`? It does nothing there
    and the build says so. See [Frontmatter](@frontmatter).

!!! note "This list does not say how long it is"

    It used to open *"Nine questions per file,"* then *"Ten,"* then *"Eleven."*
    Two of those were wrong on the day they were written, because a sentence
    and a list are two places to state one fact and the list is the one that
    gets edited.

    A numbered list already carries its own count, correctly, forever. Anything
    above it restating that number is a second claimant -- on the page whose
    entire job is catching exactly this.

## Keys that look real and do nothing

Delete on sight. None of these is read by any code in the engine, so a page
using one behaves exactly as though the line were absent -- which is
indistinguishable from the feature being broken.

| Dead | What to write instead |
| --- | --- |
| `gate:` | Nothing. It was never implemented. Use `router:` |
| `listed:` | `indexed:` |
| `also_known_as:` | `keywords:` |
| `capacity:` `dimensions:` `grid_height:` `power:` `seating:` `rigging:` | Write them in the body, or a TSV via `data:` |
| `address:` `city:` `operator:` `access_notes:` | Same. Body or data file |
| `owner:` `frequency:` `trigger:` `systems:` | Same |
| `applies_to:` `authority:` `review_cycle:` | Same |
| `maintainer:` `updated_by:` | Same |
| `hide:` | Nothing. It is a Material page property and this engine ignores it |
| `search:` | Nothing. `status: unlisted` removes a page from search |
| `parent:` on a non-`space` | Nothing. Use `related:` |

!!! warning "`nav:` was on this list until 2026-08-05, and it is now REAL"

    It is a live key: it decides what a folder does in the sidebar, on an
    `index.md` and nowhere else. See [Frontmatter](@frontmatter).

    It is named here rather than quietly removed because this table said
    *delete on sight* about a working feature for part of a day, and anybody
    who followed that advice deleted a line that was doing something. A row
    that disappears teaches nobody why they were wrong.

!!! note "The removed fields are listed individually on purpose"

    They were real until 2026-08-03 and pages in this family still carry them.
    A retired key parses as valid YAML and is silently ignored, which looks
    exactly like the feature being broken -- so each one stays named here until
    nobody is using it.

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
