---
id: writing
title: Writing a page
type: page
status: public
order: 5
revised: 2026-08
---

# Writing a page

The markdown that does something beyond plain prose: callouts, department tabs,
tables, and the one indentation rule that causes most of the trouble.

## Where this syntax actually comes from

Worth knowing before the examples, because it explains why a typo behaves the
way it does. Three separate layers have to agree:

| Layer | What it decides | Where it lives |
| --- | --- | --- |
| Python-Markdown extensions | whether `!!!` and `===` mean anything at all | the engine's `mkdocs.yml`, under `markdown_extensions` |
| Material's stylesheet | which callout NAMES have a colour and an icon | the `mkdocs-material` dependency |
| Our stylesheet | the house look layered on top | the engine's `assets/base.css` |

Nothing in this repository defines any of it, which is the whole arrangement:
content repos hold documents, the engine holds machinery.

The practical consequence is that **a callout type Material does not know still
renders.** It gets a generic box with your word as its title and no icon. It
does not error, and nobody notices for a year. So use the three below.

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

### Only three, and each means something specific

A fourth type would not break anything, which is exactly why the list is held
to three. Once there are eight, nobody can tell you what any of them mean and
they all read as decoration.

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

### Collapsible

`???` instead of `!!!` makes it a disclosure that starts closed. Add a `+` to
start it open. Good for a long aside that most readers will skip.

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

## Tables you write by hand

For comparisons. Note the contrast with the grey spec table at the top of a
venue or space page: **that one is generated from frontmatter by the page's
type** and you never write it. See [Frontmatter](@frontmatter).

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

If a hand-written table starts appearing on page after page with the same
columns, that is the signal it wants to be a **type** instead. Say so rather
than copying it a fourth time.

## The rules that prevent most surprises

1. **Four-space indent** for callout and tab bodies. Most reported "formatting
   bugs" are this.
2. **Blank line between every block.** Paragraphs, lists, headings, tables,
   callouts. Markdown is whitespace-sensitive in ways that are easy to forget.
3. **The first paragraph is the lede.** It renders large and light, and it is
   also what a search result shows. One or two lines. Do not try to make it big
   yourself.
4. **One H1 per page**, matching the title. Everything else is `##` or deeper.
5. **Do not paste raw HTML** to force a look. If a thing needs to look
   different, it needs a stylesheet change in the engine, and that fix helps
   every site instead of one paragraph.

## Related

- [Frontmatter](@frontmatter) -- the block at the top, and generated tables
- [Links](@links) -- `@id` links and cross-site references
- [Publication states](@publication) -- who can see it
