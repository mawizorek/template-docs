---
id: markers
title: Markers
type: page
status: public
order: 45
revised: 2026-08
summary: Inline tags for one value in a sentence -- how much to trust it, what kind of thing it is, and where it lives.
---

# Markers

Inline tags. They sit inside a sentence, because what they are about is usually
one value rather than the whole paragraph.

```markdown
The second altered curtain is not named: [To be confirmed]{.tbc}
Cyc width [40'-0"]{.conf}, previously [48'-0"]{.was}
A [source 4]{.term} is an ERS fixture
The key is in [the SM office]{.hi}
```

Used bare, a marker prints its own label:

```markdown
Grid height: {.gap}
```

## Two forms, and the underline is the difference

Every marker has a **span** form. Some also have a **link** form, which points at
something real:

```markdown
WORKDAYS joins [fkWeek]{.rel}                 a span -- names it
WORKDAYS joins [fkWeek](@rel:table-weeks)     a link -- points at it
```

Same family, same colour, same weight. The link is underlined, and that is the
only difference a reader has to learn, because underline already means *this goes
somewhere* everywhere else.

⭐ **The difference that actually matters is not visual.** A span records a
**mention**. A link records an **edge** -- source and target -- into the reference
graph the build publishes. That is what turns a pile of marked-up relationships
into something you can read as a map.

**Use the link form whenever the thing has a page.** Fall back to the span when it
does not, which is genuinely common and is not a failure.

## The families

Every marker belongs to a **family**, and the family decides the colour. This
matters more than it looks: the build report groups by family, so *what is still
unconfirmed across this site* stays answerable no matter how many terms, layout
objects or highlights a page carries.

### Confidence -- how much to trust the value beside it

| Marker | Means | Use it when |
| --- | --- | --- |
| `{.tbc}` | To be confirmed | You wrote it down but have not checked it against a source |
| `{.verify}` | Verify on site | Recorded once, never re-checked. Measure before building to it |
| `{.gap}` | Not recorded | This fact should exist and does not. The absence is **known** |
| `{.conf}` | Confirmed | Double-checked against the real thing. Trust it |
| `{.est}` | Estimate | Approximate. Plan with it, do not cut to it |
| `{.was}` | Superseded | The old **value**, kept so old paperwork can still be matched up |

None of these has a link form. A confidence claim is about the value in front of
you; there is nowhere for it to point.

### Terminology and highlight

| Marker | Means | Link form |
| --- | --- | --- |
| `{.term}` | House terminology, with or without a page behind it | `@term:` |
| `{.hi}` | Look here. Says nothing about whether the value is right | -- |

⚠️ **`{.hi}` is not a quiet `{.tbc}`.** If you mean *I have not checked this*, say
that -- the confidence markers are counted as doubt and `{.hi}` is not, so a
highlight used to mean uncertainty is a doubt that never appears in the report.

### Layout -- FileMaker Layout mode

Things placed on a screen. Boxed, because they turn up mid-sentence in prose and a
control being named should look like a control.

| Marker | Means | Link form |
| --- | --- | --- |
| `{.button}` | A button. Mark what the button **says** | -- |
| `{.field}` | A field placed on a layout | -- |
| `{.portal}` | A portal. The relationship feeding it is a separate mark | -- |
| `{.layout}` | A layout | `@layout:` |

### Schema -- FileMaker's Manage menu

How the data is shaped. Plain rather than boxed, because these are typed inside
table cells and a chip in every cell of a `.tsv` is a wall.

| Marker | Means | Link form |
| --- | --- | --- |
| `{.calc}` | A calculation | `@calc:` |
| `{.rel}` | A relationship between tables | `@rel:` |
| `{.script}` | A script | `@script:` |
| `{.vl}` | A value list | `@vl:` |
| `{.trigger}` | A script trigger | -- |
| `{.global}` | A global field or a `$$variable` | -- |

### Alias -- a name that used to be the name

| Marker | Means | Link form |
| --- | --- | --- |
| `{.alias}` | A retired **name**, pointing at the live one | `@alias:` |

Boxed **and** underlined, which is the one combination nothing else uses. It is
quiet on purpose: it is not the current name.

⚠️ **`{.alias}` and `{.was}` are not the same tool.** `was` supersedes a **value**
(`48'-0"` became `40'-0"`). `alias` supersedes a **name** (`fkColloquial` became
`dateFormat_Colloquial`). The practical difference is that an alias points
somewhere and a superseded value does not.

## `@rel:` -- a relationship

Point it at the page of the table on the other end.

```markdown
- [fkWeek](@rel:table-weeks) -- the parent week
- [EVENTS|span](@rel:table-events) -- a range join, not an equality
```

That is now an edge in the reference graph, so *every relationship in this doc
set* is a list you can read rather than a thing you go hunting for. The span form
`[fkWeek]{.rel}` is fine where the other table has no page yet.

## `@calc:` -- a calculation, at its own heading

A calculation has no page of its own. It lives at a **heading** on its table's
page, so the address has two halves:

```markdown
[dateFormat_Colloquial](@calc:table-workdays#calc-dateFormat_Colloquial)
                        ^^^^^^^^^^^^^^^^^^^ ^^^^^^^^^^^^^^^^^^^^^^^^^^^
                        the table's page id  the calc's own anchor
```

### Where a calc definition goes

**On its table's page, under `## Calculations`, one `###` per calculation.** Not
in a sidecar file and not in a page of its own: fewer files, same detail.

```markdown
## Calculations

### dateFormat_Colloquial {#calc-dateFormat_Colloquial}

Unstored [Text]{.calc}, from [DATE]{.field}. The human spelling on the grid.

    Let ( d = DATE ;
      DayName ( d ) & " " & MonthName ( d ) & " " & Day ( d )
    )

- Unstored on purpose. Display only; nothing joins on it.
```

🔴 **Write the `{#calc-name}` anchor explicitly. Always.** A heading gets an
automatic anchor for free, but it is derived from the heading TEXT and lowercased
-- so `## dateFormat_Colloquial` is reachable at `#dateformat_colloquial`, and
retitling the heading silently breaks every inbound link **while both ends still
look completely fine.** An explicit id is a contract, exactly like the page `id:`
is, and renaming one is then a deliberate act rather than an accident.

⚠️ **Two headings must not carry the same id.** The browser jumps to the first and
says nothing, so the second is unreachable and nothing looks wrong.

### Why the doc is the register

FileMaker has **no screen that lists every calculation in a file**. Manage >
Database shows one table at a time and hides the formula behind a button. So this
is not a description of a calc that lives somewhere else -- the page **is** where
it is written down, and the build report is the only place they can all be read at
once.

That is not true of every schema marker, and the difference is worth knowing.
Manage > Value Lists **does** enumerate value lists, so `{.vl}` is not a register
-- it is there to record **who uses one**, which is the part FileMaker cannot show
you.

## Every marker is counted

This is the part that makes them worth using rather than just typing TBD.

Every marker on the site is **listed in the build report, grouped by family** and
named by page, in both forms -- so *what is still unconfirmed across this entire
site* and *every calculation we have written down* are both questions with
answers, and they show up every time you [preview](@publishing).

It is listed as inventory, not as an error. A page full of markers is still a
clean build; marking your doubts is good practice, not a defect. It also means a
verification pass is **finishable**: walk the space, mark things `{.conf}`, and
the report tells you what is left.

## Two traps

### A marker span cannot hold a link

```markdown
[Saved [SET](@table-print-sets)]{.button}     WRONG
```

This does not fail loudly. The pattern forbids a `]` inside the text, so it
matches the **bare** form instead and renders a chip reading "Button" with the
link stranded beside it as literal text. Split them, or use the link form:

```markdown
[Saved SET]{.button} -- from [PRINT_SETS](@table-print-sets)
[SET](@layout:print-sets)
```

### An unknown marker renders as nothing

A marker that is not in the table is handed back **untouched** -- plain body text,
no error, one line in the build report. That is deliberate, because `{ .md-button }`
is somebody else's syntax and eating it would be worse.

⚠️ It also means a typo is invisible on the page. On 2026-08-09 this family of
sites was carrying twelve markers that had never rendered once, reported on every
single build. **Being reported is not the same as being seen** -- which is why
there is a render-check page, and why you should glance at it after adding a
marker.

## They are not all one category any more

They were, for a long time, and this page said so: *"every marker answers how much
should I trust this -- nothing else."*

That was true when there were six, it stopped being true when terminology arrived,
and there are now ~~three~~ **six** families. Corrected rather than deleted,
because it was a real rule and anybody who read it will remember it.

**What replaced it is the family, not a free-for-all.** The old rule was protecting
the build report -- a mixed bag of markers cannot answer one question. Families
protect the same thing better, because the report groups by family and each family
answers its own question.

## Adding one

A new **marker** is a row in `theme/markers.tsv` in the engine. A whole new
**family** is a row in `theme/marker-classes.tsv`. A **link form** is one more cell
-- the `prefix` column -- on a row that already exists. None of it is a code change.

**Prefer a token to a literal colour.** A token follows the theme into light mode
and across every site; a hardcoded colour is frozen where you typed it and will be
wrong on the scheme you were not looking at.

### ~~Two markers must never share a colour~~

~~Even across families -- they turn up in the same sentence at the same size, and
paint is the only thing telling them apart.~~ **Struck 2026-08-09**, by Michael:
*"i don't care if they're visually identical. the reporting tag is usually to be
different. the front end would begin to look like skittles if everything had its
own color at this point."*

⭐ **The corrected rule is narrower: a colour collision is a defect only where the
COLOUR IS CARRYING THE MEANING.** A reader separates `{.conf}` from `{.gap}` by
paint, so those must stay apart. Nobody reads a `{.calc}` chip and asks how
confident it is -- the **tag** carries that, the report consumes the tag, and the
paint is only saying *this is marked*.

So `layout` and `highlight` share a colour today, and so do `schema` and
`terminology`. That is deliberate. If two families ever genuinely need telling
apart mid-sentence, the answer is a different **shape** or a different tag, never a
new hue.

The old rule was written when every marker was a confidence claim, where hue **is**
the semantics, and then stated about all of them. Worth remembering as a shape: a
rule derived from one kind of case and stated about every case.

## Related

- [Links](@links) -- `@id`, headings, cross-site references, and every prefix
- [Frontmatter](@frontmatter) -- where required fields are declared
- [Publishing](@publishing) -- where the marker report appears
- [Routers](@routers) -- the other inline tool, for routing rather than confidence
