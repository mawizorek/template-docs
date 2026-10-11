---
id: authoring-images
title: Images
type: page
status: public
order: 5
summary: Putting an image on a page, naming it so it can be found from anywhere, and the difference between a caption and the text in the brackets.
revised: 2026-10
keywords: [image, figure, caption, alt text, screenshot, photo, plot, img]
---

# Images

```
![<what the image shows>](@img:<file-name>){ caption="<what the reader needs told>" }
```

**The filename without its extension is the name.** `h5-front.png` is `@img:h5-front`.
Nothing is declared, nothing is registered, there is no block to add to the
frontmatter. Drop the file in and reference it.

## The four parts

| Part | What it is | Who sees it |
|---|---|---|
| `!` | the bang | nobody — it is what makes this an image and not a link |
| `[ … ]` | **alt text** | screen readers, and anyone whose image failed to load |
| `( … )` | **the name of the picture** | nobody |
| `{ caption="…" }` | **the caption** | everybody, printed under the image |

Drop the brace and you get a plain uncaptioned image.

## Where the file goes

**Beside the page it belongs to.** That is the default and it is almost always
right. A venue's photos live in that venue's folder; they move when the page
moves and they are deleted when it is.

**A shared-media folder for anything with no single owner** — a logo, a symbol
key, a diagram several departments point at. Each site names its own; the rule
is that one exists, not what it is called.

⚠️ **`@img:` does not care which you chose.** The reference is identical either
way, and it keeps working if you move the file later. That is the whole reason
to use a name instead of a path.

### You can still use a plain relative path

```
![The H5 record screen](h5-record-screen.png)
```

Still valid, still correct for an image sitting right beside the page, and
shorter to type. **It breaks the moment either end moves**, and it needs
counting — from a page four folders deep, reaching the shared-media folder is
`../../../../media/logo.png`, and nothing checks that you counted right.

Prefer `@img:`. Use a bare filename when the picture is in the same folder and
you are not going to think about it again.

## 🔴 A name has to be unique across the whole repository

The name is global, so the collision is too. **Two files called `menu.png`
anywhere in the tree make `@img:menu` ambiguous, and the build refuses it rather
than guessing** — every reference to it renders as a visible broken marker until
one is renamed.

That refusal is deliberate. Two pictures with one name are two different
pictures, and choosing one would put the wrong photograph on a page with nothing
looking wrong.

So name for the thing, not for the folder it sits in:

| 🚫 | ✅ |
|---|---|
| `menu.png` | `h5-menu.png` |
| `front.png` | `h5-front.png` |
| `screen-2.png` | `h5-record-screen.png` |

**The extension is not part of the name.** That is what lets a `.png` become a
`.webp` later without touching a single page.

## The brackets are not a title

!!! warning "This is the one that catches everybody"

    The text in the square brackets has always been there and has **never been
    displayed**. It is what a screen reader says *instead of* showing the
    picture. Until captions existed there was nowhere else to put a label, so
    labels went in the brackets — and they have been sitting there ever since,
    doing a job they were never doing.

**Alt replaces the image. A caption accompanies it.** Different sentences, both
worth writing.

```
![Rep plot](@img:rep-plot)
```

A badly alt-texted image, not a titled one. It names the file and describes
nothing, so a reader who cannot see it learns nothing at all.

```
![Light plot, 42 instruments over three electrics](@img:rep-plot){ caption="Rep plot, 2026 season" }
```

Alt says what is in the picture. The caption says what you would say standing
next to it.

⚠️ **If the caption genuinely says everything, write `alt=""`** — an empty alt is
a real and correct value for a decorative image. What is wrong is repeating the
caption in the brackets, which makes a screen reader announce the same sentence
twice in a row.

## A caption can wrap

```
![Rep plot, three electrics and two box booms](@img:rep-plot){ caption="Rep
plot as hung for the 2026 season. Supersedes the plot in the
[venue binder](@example-binder)." }
```

How you wrap it cannot change what renders — the line breaks collapse to single
spaces and the caption prints as one line of prose.

⚠️ **A blank line ends a caption.** Same rule as every other block in markdown.
If you leave the closing quote off, the caption stops at the end of the
paragraph rather than eating the rest of the page, and the build reports it.

A caption takes anything a sentence takes: `@` references, confidence markers,
bold, code.

## The image has to be alone on its line

At zero indent, nothing else on the line. A figure is a block, so an indented
image inside a list item would be lifted out of the list, and one mid-sentence
would split the paragraph in half.

Both cases render the image normally, drop the caption, and **say so in the
build report**. An image mid-sentence is perfectly legal — it just cannot carry
a caption.

## An image that lives in a different repository

**Copy it into this one.** That is the whole answer, and it is a decision rather
than a missing feature.

`@img:` reaches every image in *this* repository from every page in it, which is
the case that actually comes up. Reaching into a sibling site was considered and
rejected:

- **Linking their published address looks free and is not.** If they replace the
  file and keep the filename, your page shows **a different picture under your
  caption**. Not broken — wrong. No 404, no report, nothing to notice.
- A broken `@img:` or `@peer:id` is caught **while the site is building**. A
  broken image URL is caught by **nobody**: it fails in the reader's browser,
  months later, and appears in no report ever.

⚠️ The cost of copying is honest and small: your copy can drift from theirs and
nothing will tell you. **Prefer a stale picture you own to a live one you do
not.**

## Markdown's own title still works, and still should not be used

```
![alt text](@img:rep-plot "this is a title")
```

That quoted string becomes a tooltip on some browsers, on a mouse, sometimes. It
does not exist on a phone or tablet, it is announced inconsistently by screen
readers, and it cannot be reached from a keyboard.

The renderer does not add it and cannot remove it — it is part of markdown
itself. **Anything worth saying in a title belongs in the caption or the alt
text.**

## What the build will tell you

Named in the build report, with the page:

- an `@img:` name that matches no file
- an `@img:` name that matches **more than one** file, and both paths
- an image indented, or not alone on its line
- `caption=""` with nothing in it
- a caption whose quote or brace never closes

A missing or ambiguous `@img:` renders as a struck-through marker a reader can
see. The rest render the image and drop the caption.

**Nothing here fails a build.** A typo costs you the caption, not the page.

---

*Relocated here 2026-10-10 under DOC REVIEW 001. This rule previously lived only
in `uritp-docs/00-authoring/images.md`, which meant every site that renders an
image was governed by a file inside one consumer. The rules are unchanged; the
one named shared-media folder was generalized, because naming it is a site fact
and having one is a shared rule.*
