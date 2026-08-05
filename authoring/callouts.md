---
id: callouts
title: Callout gallery
type: page
status: public
order: 6
revised: 2026-08
summary: Every callout family, rendered, so you can pick one by looking instead of guessing from a name.
---

# Callout gallery

Every family below is **rendered, not described.** Colour is not a thing prose is
good at, so this page shows you rather than telling you.

What each one *means* is on [Writing a page](@writing). This page is for picking
one by eye.

!!! note "Everything here follows the theme"

    Not one of these colours is written into this page, or into the renderer.
    They come from the site's theme, so all of them change together when the
    theme does. Recolouring a family is one row in one table in the engine.

## The three that carry weight

Most pages need only these. They are a ladder, and it only works if the top rung
stays rare.

!!! note "note -- context, a gap, a placeholder"

    Something worth knowing that costs nothing if you miss it. This takes the
    site's own identity colour rather than a semantic one, because a note is the
    house speaking.

!!! warning "warning -- this costs money, time, or a wasted trip"

    The reader is about to make a decision and this changes it.

!!! danger "danger -- a genuine safety stop"

    Someone gets hurt. Use it for that and nothing else: a danger box spent on a
    scheduling annoyance teaches readers to scroll past the one that mattered.

## Positive

Three families, **one colour, three glyphs.** Look at them together -- the colour
is identical and the icon is the only thing telling them apart. That is
deliberate: words that mean the same thing to a reader should not be different
colours.

!!! tip "tip -- advice that helps"

    A shortcut, a better way round, something worth knowing before you start.

!!! success "success -- something worked, or is confirmed"

    A check that passed, a value verified against the real thing.

!!! good "good -- a positive pointer"

    *Look here for this.* The useful door, the working outlet, the person who has
    the key. Box Office has the First Aid kit behind the counter.

**If you cannot tell which of the three you want, you want tip.**

## Informational

!!! info "info -- an informational aside"

    Neither advice nor a warning. Something the page wants said off to one side.

!!! question "question -- an open question, or an FAQ entry"

    Shares its colour with info, because a question and an informational aside
    are the same register to a reader. The glyph is the difference.

!!! abstract "abstract -- a summary or TL;DR"

    The secondary identity colour. Good at the top of a long page, for readers
    who will not reach the bottom.

## Things that went wrong

Three families sharing the alarm colour, for the same reason the positive three
share theirs.

!!! failure "failure -- something did not work"

    A test that failed, a fixture that did not come up, an approach that was
    tried and abandoned.

!!! bug "bug -- a known defect"

    A record of something broken, rather than a warning about something risky.

!!! danger "danger -- here again on purpose"

    So you can see it sitting in the same colour as failure and bug. If a hazard
    did not read as the same alarm as a failure, the ladder would not work.

## Quiet

No hue at all. These are quieter than the page rather than a category of alert.

!!! example "example -- a worked example"

    A specific case, spelled out. Quiet because the content is the point and the
    box is only holding it.

!!! quote "quote -- a quotation"

    The muted text colour. A quote is somebody else talking, not an alert.

## Collapsible

Swap `!!!` for `???` and the box becomes a disclosure. Add a `+` to start it
open. **Works with every family above.**

??? note "??? -- starts closed"

    This is the whole reason to use it: forty lines of detail stay present and
    findable without pushing everything else off the screen.

???+ tip "???+ -- starts open, still collapsible"

    For something most readers want, and a few will want out of the way.

## The one thing this page cannot show you

**Press Tab.** Every box takes a focus ring in its own colour when a keyboard
reaches it, which is the one governed surface a page cannot demonstrate by
sitting still.

It was hardcoded blue until 2026-08-05, so a green box flashed a blue ring -- and
the ring was also far too faint to count as a focus indicator at all. Both fixed.

## The mistake everybody makes once

**Indent the body four spaces.** Not a style preference: it is what tells the
parser the body belongs to the box.

```markdown
!!! warning "Load-in is tighter than it looks"

The dock door is 2.4m.
```

That renders as a **title-only box with the text loose underneath it**, which
looks like a rendering bug and is an authoring one. The parser hands anything
unindented back as a separate paragraph.

```markdown
!!! warning "Load-in is tighter than it looks"

    The dock door is 2.4m.
```

## Using a word that is not on this page

It will still render. Nothing validates the word you type after `!!!` -- it goes
straight into the page as written.

!!! sparkle "sparkle -- a family nobody declared"

    This box is what an undeclared word looks like. The renderer has no colour
    for it, and it inherits the **note pencil** from the framework underneath,
    because that icon is set for every box and only a declared family replaces
    it.

    So a typo does not look broken. It looks like a note. That is the reason to
    stay with the families above.

## Related

- [Writing a page](@writing) -- what each family means, and when to reach for it
- [Markers](@markers) -- the inline version, for confidence in one value
- [The gold standard](@audit) -- the frontmatter block and the audit checklist
