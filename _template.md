---
id: template
title: Page template
type: page
status: public
order: 5
revised: 2026-08
---

# Page template

Copy a block, delete the lines you do not need, write the page.

Nothing here explains itself. The reasons live in [Authoring](@authoring), on
purpose: a second copy of an explanation is a second copy free to go stale, and
this file is meant to be short enough to keep on a clipboard.

## 1. The frontmatter

**The order of these keys is the spec.** Required at the top, optional at the
bottom. Delete upward from the end and you can never delete something
mandatory.

```yaml
---
# ── REQUIRED ── no status means the page is NOT BUILT ──
id: kebab-case-name
title: Human Readable Title
type: page
status: hidden

# ── REQUIRED IF type: space ── an id, never a path ──
parent: smith-theatre

# ── OPTIONAL ── delete any line you are not using ──
order: 10
revised: 2026-08
theme: utility
indexed: false
related: [smith-theatre, todd-theatre]
source: Measured on site, Aug 2026

# ── ROUTERS ── all optional, but they depend on each other ──
router: pm                    # engine table. One, or [a, b]
router_code: temp26           # code in THIS file. One, or [a, b]
router_prompt: Got a code?    # needs one of the two lines above
router_inherit: false         # only if a parent folder declares one
---
```

### What each tier means

| Tier | Rule |
| --- | --- |
| **Required** | Missing `id` or `title` is reported. Missing `status` means the page does not build and every `@link` to it breaks. |
| **Conditional on type** | The type decides. See the table below. |
| **Optional** | Absent is a valid answer. `order` absent sorts alphabetically. |
| **Interdependent** | `router_prompt` with no `router`/`router_code` labels nothing and is reported. `router_inherit` with no ancestor router does nothing. |

⚠️ **Never write a key twice to give it two values.** YAML keeps the LAST one
silently and the earlier line vanishes with no on-page symptom. Use a list:
`router: [pm, crew]`.

## 2. Pick a type

| `type:` | Also requires | Fields it draws into a table for you |
| --- | --- | --- |
| `page` | — | none |
| `index` | — | contents list of the pages below it, at the foot |
| `venue` | — | `address` `city` `operator` · also takes `access_notes` |
| `space` | **`parent`** | `capacity` `dimensions` `grid_height` `power` `seating` `rigging` |
| `standard` | — | `applies_to` `authority` `review_cycle` |
| `procedure` | — | `owner` `frequency` `trigger` `systems` |
| `reference` | — | `maintainer` `updated_by` |

Add those fields to the frontmatter and the renderer draws the table. **Never
type the table by hand** — thirty hand-typed tables are thirty tables that
disagree.

An undeclared type falls back to `page` and is reported. `index` is about
POSITION, so use it when pointing at the pages below is the whole job; if the
landing page is *about* something, type it as that.

## 3. The body

```markdown
# Human Readable Title

What this is and who needs it. One or two lines. This is the lede and it is
also what a search result shows.

## Whatever this page actually needs

Body. Blank line between every block.

## Related

- [Smith Theatre](@smith-theatre)
```

**Not every page needs every section.** Only the H1 and the lede are expected
everywhere. Add what the page needs and nothing else.

What IS fixed is the shape of a section once you use it:

| Section | Rule |
| --- | --- |
| H1 | Exactly one, first line, matches `title:` in meaning |
| Lede | The paragraph straight after the H1. Never a list, never a callout |
| `## Related` | Named exactly that, **last section**, bullet list, `@id` links only |
| Callouts | `!!! note` · `!!! warning` · `!!! danger`. Body indented four spaces |
| Links | `@id`, never a path, never a full URL to a page on this site |
| Markers | `{.tbc}` `{.verify}` `{.gap}` `{.conf}` `{.est}` `{.was}` |

Syntax and meanings: [Writing a page](@writing) · [Links](@links) ·
[Markers](@markers).

## 4. Audit checklist

Run a page against this. **MUST** is a defect; **IF PRESENT** only applies when
the page has that thing at all.

**MUST**

- [ ] Frontmatter is the very first thing in the file — no blank line above `---`
- [ ] `id`, `title`, `status` all present
- [ ] No key appears twice
- [ ] `id` is kebab-case and unique across the site
- [ ] `type:` written explicitly
- [ ] `parent:` present if `type: space`
- [ ] Exactly one H1, and it is the first line of the body
- [ ] A lede paragraph directly under the H1
- [ ] No leftover template placeholder text

**IF PRESENT**

- [ ] `## Related` is named exactly that and is the last section
- [ ] Every internal link is `@id`
- [ ] Every `@id` resolves — check the build report, not by eye
- [ ] Type fields are in the frontmatter, not typed into the body as a table
- [ ] Uncertain values carry a marker instead of sitting there bare
- [ ] Callout bodies are indented four spaces
- [ ] Authoring commentary meant for you is a `<!-- comment -->`, or deleted

!!! warning "Open question, not a rule: the revision date"
    `revised:` in the frontmatter is currently rendered **nowhere** — it is in
    no type's table — so the only visible date is a hand-typed `*Revised Aug
    2026.*` line at the foot of some pages. That is two hand-maintained copies
    of one fact, which is exactly what this file exists to prevent.

    Either the renderer should draw `revised:`, or the footer line is the real
    source and the frontmatter key is decoration. **Undecided**, so the
    checklist does not test for either.
