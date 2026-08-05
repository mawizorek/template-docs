---
id: writing
title: Writing a page
type: page
status: public
order: 5
revised: 2026-08
summary: The markdown that does something beyond plain prose - callouts, department tabs, tables, and the one indentation rule that causes most of the trouble.
---

# Writing a page

## Where this syntax actually comes from

Worth knowing before the examples, because it explains why a typo behaves the
way it does. Three separate layers have to agree:

| Layer | What it decides | Where it lives |
| --- | --- | --- |
| Python-Markdown extensions | whether `!!!` and `===` mean anything at all | the engine's `mkdocs.yml`, under `markdown_extensions` |
| Material's stylesheet | the callout ICONS, and the fallback look for a name nobody has declared | the `mkdocs-material` dependency |
| Our theme | which callout families exist and what COLOUR each one takes | the engine's `theme/blocks.tsv`, one row per family |

Nothing in this repository defines any of it, which is the whole arrangement:
content repos hold documents, the engine holds machinery.

**Recolouring a callout family is one row in `theme/blocks.tsv`.** It used to be
a hardcoded hex in Material's own stylesheet, which is why no theme change ever
reached a callout before 2026-08-05. Ask for the row, not a stylesheet edit.

The other practical consequence is that **a callout type nobody has declared
still renders.** Python-Markdown matches any word after `!!!` and lowercases it
straight into a class, with no validation of any kind. It does not error. What
you get is a box in Material's default colour rather than one of ours, **wearing
the note pencil** -- because Material's base rule sets that icon unconditionally
and only a declared family overrides it.

⚠️ **So a mistyped family name does not look broken, it looks like a `note`.**
That is worse than an obvious failure and it is the reason to stick to the list
below.

## Callouts

**The body must be indented four spaces.** That is the whole trick, and it is
the single most common reason a callout renders as literal text with `!!!`
sitting there in the middle of the page.

```markdown
!!! warning "Load-in is tighter than it looks"

    The dock door is 2.4m. Anything taller comes in through the house,
    which costs about an hour.
```

!!! warning "Load-in is tighter than it looks"

    The dock door is 2.4m. Anything taller comes in through the house,
    which costs about an hour.

⚠️ **An unindented body does not fail loudly either.** It renders as a
title-only box with your text sitting underneath it as a loose paragraph, which
reads as a styling bug and is an authoring one.

### The thirteen families

Every one of these takes its colour from the site's theme, so they change
together when the theme does. In the engine's own row order:

| Type | What it means | Colour |
| --- | --- | --- |
| `note` | context, a gap, a placeholder | the site's identity colour |
| `abstract` | a summary or TL;DR at the top of a long page | secondary identity |
| `info` | an informational aside | blue |
| `tip` | advice that helps | green |
| `success` | something worked, or is confirmed | green |
| `question` | an open question or an FAQ entry | blue |
| `warning` | proceed carefully | amber |
| `failure` | something did not work | red |
| `danger` | a genuine safety stop | red |
| `bug` | a known defect | red |
| `example` | a worked example | quiet grey |
| `quote` | a quotation | quiet grey |
| `good` | a positive pointer -- *look here for this* | green |

**Six families share three colours, on purpose.** `tip`, `success` and `good`
are all green; `failure`, `danger` and `bug` are all red. Words that mean the
same thing to a reader should not be different colours, and **the icon is what
tells them apart.** If you see two green boxes on a page, nothing is broken.

⚠️ **The list is a house convention, not a constraint.** Nothing validates the
word you type -- see above. Reach for a fourteenth only when you can say in one
sentence what it means that none of these does, because a vocabulary nobody can
recite is decoration.

### The three that carry weight

Most pages need `note`, `warning` and `danger` and nothing else. They are a
ladder, and the ladder only works if the top rung is rare.

**`note`** -- context, a gap, a placeholder. Something worth knowing that costs
nothing if you miss it.

!!! note "Capacity is pre-renovation"

    This figure predates the 2019 seating work and has not been re-counted.

**`warning`** -- this costs money, time, or a wasted trip. The reader is about
to make a decision and this changes it.

!!! warning "No fly access without a second technician"

    The grid is single-purchase and the house rule is two people on the
    rail. Budget for it or the call does not happen.

**`danger`** -- a genuine safety stop. Someone gets hurt. Use it for that and
nothing else, because a `danger` box used for a scheduling annoyance teaches
readers to scroll past the one that mattered.

!!! danger "Do not load the upstage traps"

    The traps are decked but not rated. There is no load figure for them
    and nobody has inspected them since installation.

### `good` -- the positive pointer

The newest family, and the only one that is ours rather than inherited. Green,
with a check. It is for **where a thing is** rather than what to be careful of:
the useful door, the working outlet, the person who has the key.

```markdown
!!! good "Look here for First Aid"

    Box Office has a kit behind the counter, and the house manager
    carries the second one.
```

!!! good "Look here for First Aid"

    Box Office has a kit behind the counter, and the house manager
    carries the second one.

**`good` versus `tip` versus `success`.** They share a colour and they are not
interchangeable: `tip` is advice, `success` is a thing that worked, `good` is a
location or a resource worth knowing about. If you cannot tell which one you
want, you want `tip`.

### Collapsible

`???` instead of `!!!` makes it a disclosure that starts closed. Add a `+` to
start it open. Good for a long aside that most readers will skip. **Works with
all thirteen families.**

```markdown
??? note "Full circuit schedule"

    ... forty lines nobody needs on first read ...
```

??? note "Full circuit schedule"

    Collapsed by default. This is the whole reason to use it: the detail is
    present and findable without pushing everything else off the screen.

## Department tabs

For the same information split by who needs it. One block, several audiences,
no duplicated page.

**Same four-space indent rule.** Blank line between tabs.

```markdown
=== "Lighting"

    Two 400A company switches, stage left. House plot hangs on 1-12.

=== "Sound"

    FOH position is row H, centre. Six seats killed when it is in.

=== "Wardrobe"

    Two-station quick change stage right. No running water.
```

=== "Lighting"

    Two 400A company switches, stage left. House plot hangs on 1-12.

=== "Sound"

    FOH position is row H, centre. Six seats killed when it is in.

=== "Wardrobe"

    Two-station quick change stage right. No running water.

**When not to use tabs.** If a reader needs to compare two of them side by
side, tabs are the wrong shape and a table is the right one -- tabs hide
everything except the one you are looking at. And anything inside a tab is
invisible to a reader who never clicks it, so nothing safety-critical goes in
one.

## Tables

Write them by hand. Nothing generates a table from frontmatter any more -- the
type-drawn spec table was removed on 2026-08-03 along with the fields that fed
it, because a capacity or a grid height is a fact about the subject and belongs
in the document, not in its header. See [Frontmatter](@frontmatter).

```markdown
| Position | Seats lost | Notes |
| --- | --- | --- |
| Row H centre | 6 | Standard FOH |
| Rear house | 0 | Sight line is poor |
```

| Position | Seats lost | Notes |
| --- | --- | --- |
| Row H centre | 6 | Standard FOH |
| Rear house | 0 | Sight line is poor |

**When a hand-written table gets big, it wants to be a data file.** Not a type.
A hundred rows of dimmer circuits is unreadable as markdown and unmaintainable
by anybody without a text editor open. Put it in a TSV beside the page, declare
it with `data:`, and place it with a `<!-- dr:table -->` marker: it stays
editable in a spreadsheet, diffable in git, and the reader gets a download link
to the exact file it was drawn from.

## The rules that prevent most surprises

1. **Four-space indent** for callout and tab bodies. Most reported "formatting
   bugs" are this.

2. **Blank line between every block.** Paragraphs, lists, headings, tables,
   callouts.

    ⚠️ **GitHub's preview is more forgiving than this site, and that is a trap
    rather than a convenience.** GitHub-Flavoured Markdown lets a list
    interrupt a paragraph; Python-Markdown, which builds this site, does not.
    So a list with no blank line above it renders perfectly in the preview and
    arrives here as one run-on paragraph. The preview is not evidence about
    the render.

3. **The lede is `summary:` in the frontmatter, not a paragraph you type.**

    ⚠️ **This changed on 2026-08-03 and it used to say the opposite.** The
    first paragraph under the H1 WAS the lede: it rendered large and light and
    it was what a search result showed. It is a field now, and a paragraph
    left under the H1 is reported by the build. See
    [Frontmatter](@frontmatter).

4. **One H1 per page, and it must match `title:`.** Everything else is `##` or
   deeper. The two are separate strings that nothing reconciles for you: the
   sidebar, the browser tab, the search-result heading and `doc-index.json`
   all follow the FIELD, so a page whose H1 disagrees is called two different
   things depending on where you meet it.

5. **Facts about the subject go in the body.** A capacity, an address, an
   owner, a phone number. There is no header field for any of them, and adding
   one back is the mistake that was just undone.

6. **Do not paste raw HTML** to force a look. If a thing needs to look
   different, it needs a stylesheet change in the engine, and that fix helps
   every site instead of one paragraph.

## Related

- [Frontmatter](@frontmatter) -- the block at the top, and what may go in it
- [Links](@links) -- `@id` links and cross-site references
- [Publication states](@publication) -- who can see it
