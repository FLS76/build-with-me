---
name: build-with-me
description: Write a "build along with me" tutorial for a project we built together - volumes, chapters, and a per-element breakdown where every element is explained, every line of code or every action is written out live with the reason it exists and the consequence of omitting it, and both the errors that actually happened and the ones the reader will hit. Works for code and for office programs, game engines, 3D programs and drawing programs. Use this whenever the user asks to write up, document, or recap how a project was built, set up, installed, configured, or debugged together; asks for a tutorial, walkthrough, or step-by-step guide for a project we worked on; asks for an element-by-element breakdown of a codebase or what breaks if a file is removed; or says "собери вместе со мной", "напиши туториал", "опиши как мы это делали", "туториал по сборке", "подробная инструкция как мы ставили", "разбери программу по элементам", "что будет если убрать этот файл". Also use it when the project is not a program, such as a spreadsheet, document or slide deck in Excel, Word, PowerPoint or LibreOffice; a level, Blueprint or asset in Unreal, Unity or Godot; a scene in Blender or Maya; a layered drawing in Krita or Photoshop - and for the Russian equivalents "разбери таблицу по элементам", "покажи как мы делали презентацию", "опиши как мы собирали сцену", "разбери рисунок по слоям", "напиши туториал по игре". Also use when the user wants mistakes preserved rather than a clean summary. Do not use for reference documentation about someone else's project.
---

# Build along with me

## Contents

This skill has two parts. **Part I is the method** and it assumes the reader is
writing code. **Part II is what changes when they are not** — four chapters, one
each for office programs, game engines, 3D programs and drawing programs.

Everything in Part I still applies in Part II. Read the Part II chapter for the
medium, then come back to Part I whenever a rule is unclear.

    Part I — Code
      What this produces
      Where the material comes from
      Paths
      Ask before writing
      Document structure
        Volumes
        Chapters
        Elements
      How much is enough
      Steps: write the code live
      Errors: what happened, and what will happen
      Abandoned approaches
      On someone else's project

    Part II — Other kinds of project
      What carries over, and what changes
      Office programs
        Spreadsheets and analysis
        Documents and plain text
        Decks and presentations
      Game engines
        Games on an engine
        Blueprints are code
      3D programs
        Blender: models, animation, render
        Beyond Blender: Maya, Houdini, ZBrush and the rest
      Drawing programs
        Raster images, layers and export
        Drawing and image work

      Checklist before handing it over

## What this produces

A tutorial in the "we built it together" genre, written for a reader who starts
from nothing and types every line themselves. At the end they have a working
program and understand every piece of it.

Three things separate this from ordinary documentation:

- **Mistakes are kept.** Not "here is the finished program explained" but "here
  is the path we walked, including where it went wrong".
- **Nothing is unjustified.** No element and no line exists without the reader
  knowing what it does and what breaks without it.
- **The reader's failures are anticipated.** They start from a different machine
  and will hit things we did not.

## Where the material comes from

**Start from the code.** Read the files, walk the structure, see what imports
what and what runs in which order. That is the foundation, and it is what the
reader will be checking their own copy against.

**Then enrich from the conversation.** The code cannot tell you that the build
failed because a file was locked, that the first approach was wrong, that three
attempts were tried before one worked. Where the work happened with someone,
that history makes the difference between documentation and a tutorial.

So: structure, dependencies and consequences come from reading the code.
Motives, dead ends and failures come from remembering the session. Verify claims
about the code against the actual files rather than from memory.

## Paths

The reader chooses their own folders. Writing their paths as if they were the
only ones that exist makes the tutorial unusable for anyone else.

**Find the boundary the reader cannot cross, and cut the path there.**

For an element inside the project, the boundary is the project folder:

```
<reader's own drive and folders>\<project folder>\src\App.tsx
└────── not fixed, theirs ──────────┘└──── exact, must be copied ────┘
```

Everything before the project folder belongs to the reader: drive letter,
intermediate folders, the folder name itself. Do not name any of it. Everything
from the project folder inward is structure you chose, and that structure is what
the reader must copy exactly, so write it in full.

For an element outside the project — an installed program, a cache, a tool — the
boundary is that program's own folder, and only if the reader genuinely cannot
change it. For Git, the reader picks where Git lives, so everything up to that
choice is theirs; from the program's folder inward the names are fixed and can
be written exactly:

```
<reader's own drive and folders>\Git\cmd\git.exe
└────── not fixed, theirs ──────────┘└──── exact ────┘
```

If the reader can influence a name even inside the program's folder, it stays a
placeholder.

**State the boundary, do not just imply it.** A reader who sees
`C:\Program Files\nodejs` in one command and a placeholder in the next cannot
tell which names matter. Say plainly which parts must be copied verbatim and
which are theirs to choose, and say why the split falls where it does.

**Give a reason that survives being copied.** "A second drive, because the first
one fills up with caches" applies to the reader. The letter of a drive on the
author's machine does not, and neither does a habit of the author's. If the
project folder happens to be named in a particular language, either leave that out
of the reasoning or give a reason that applies to anyone.

## Ask before writing

Ask these three before the first word is written. Each one changes the whole
document, and each one is cheaper to ask than to rewrite.

**Ask them as a poll with clickable options**, one question per decision, each
option saying what it buys and what it costs. A reader answering three questions
in prose spends effort composing sentences; a reader clicking an option spends
one keystroke. Offer your recommendation as the first option when you have one,
and put a concrete default in every option so that picking any of them produces a
usable document rather than a blank to fill.

1. **Scope.** A session often covers more than one program. Which part is this
   tutorial about?
2. **Start state.** What does the reader already have? A second machine needs
   prerequisites and versions. A reader who has never installed a toolchain
   needs the first stage to assume nothing at all.
3. **Format.** Ask every time, because the answer decides what you build.

   Always offer these, since they require no tooling at all:

   - Markdown (`.md`) - carries everything, including code blocks and nested
     headings
   - Plain text (`.txt`) - for a reader who will not open a markdown viewer, so
     no indentation tricks and nothing left to be implied by layout
   - Something else the user has in mind

   Then find out what this machine can actually convert to, and offer only what
   you found. Look for the usual converters: `pandoc`, LibreOffice (`soffice`),
   and the libraries `docx`, `pdfkit`, `pdf-lib`, `python-docx`, `reportlab`,
   `weasyprint`. Check the project's own dependencies first, then any package
   directories and language environments already on the machine - a library
   that is installed somewhere is usable even when nothing advertises it.

   **Presence is not capability.** A converter being installed says nothing
   about whether it works. Check each candidate by actually running it on a
   fragment that uses the same alphabet and the same structures as the real
   document, then open the result and look at it. A converter that returns a
   zero exit code and no file is a failure, and a converter that returns a file
   missing its fonts is also a failure. Offer a format only after it has
   produced something readable.

   Report what you found as a short list, for example "`.docx` - the `docx`
   library is installed and verified, `.pdf` - a converter is present but
   produced no file, so I would deliver markdown". If the user picks something
   that does not work, say so plainly and deliver markdown instead: the content
   is identical, only the wrapper differs.

   Weigh the reader over yourself. A format they can open beats one that is
   easier for you to produce, and if they will not have your tooling at all,
   plain text or markdown is the safer choice.

# Part I — Code

This part is the method, and it is written for a project whose reader is writing
code: an editor open, a file being changed, a command being run. Every later
part is a variation on it, never a replacement.

## Document structure

```markdown
# <Project> — build-along tutorial

## What we are building, and why
The goal, the end state, who this is for, what the reader will have when done.
Written before anything else: it is what makes the rest readable.

## Contents
Volume I — <name> ....... chapters
  Chapter 1 — <name>
    1.1 <element> — <path>
  ...

## Volume I — <name>
Why this volume exists.

### Chapter 1 — <name>
What this chapter accomplishes, stated as an outcome.

#### 1.1 <element name> — `<path>`
What it is. Why it exists. What breaks without it.

Then the steps, each one writing code out live.
```

### Volumes

A volume is a major part of the program: a platform layer, a runtime, a
subsystem that stands alone. For a desktop and mobile app, volume one desktop,
two mobile, three packaging and signing.

Use volumes when the program has more than about three major parts **and** more
than about forty elements. A small program reads better with chapters alone, and
inventing volumes for their own sake adds navigation noise. When unsure, chapters
alone are safer.

Count the elements before deciding this. A program with one folder and one file has
no parts to separate, so its volume is a heading with nothing under it — and the
paragraph explaining why the split is the way it is admits the split was wrong. See
*How much is enough*.

Numbering is `volume.chapter.element`, with steps as `chapter.element.step`. Keep
it stable so a reader can cite a step later.

**Volumes are one document, not several files.** While the work is in progress
write each volume as its own file, so that a single reply does not have to carry
the whole book. When the last volume is done, join them into one file: one title,
one introduction, one contents listing, continuous chapter numbers, and no
leftover per-volume headers that refer to files the reader never saw. Check for
cross-references that named a volume as a file and fix them to name the volume.

Numbering is the reader's handle. If volume two says "as in step 1.1.2" and that
step lives in volume one, the join has to keep that true.

### Chapters

A phase of work with a checkable outcome: "the app starts and shows a window",
"the build produces a signed APK". Not "part one". If a chapter cannot state what
is true when it is finished, it is two chapters.

### Elements

Elements are the pieces of the program: **files, folders, configuration entries,
registered services.** This is the unit the reader thinks in, because it is what
they will look at when something breaks later.

**Folders are elements, not containers for elements.** A folder gets the same
three questions as a file: what it is, why it exists, what breaks without it. A
reader who opens `src` and finds nothing explaining why `src` exists at all, and
why `src/platform` is a separate folder rather than more files in `src`, learns
that the document is incomplete and stops trusting the parts that *are* explained.
Name the rule that decides the split — "platform code is the only part that talks
to the phone, so it can change without touching the screens" — because the rule is
what the reader needs, not just the fact that two folders exist.

**Count before you claim anything.** Open the project root, read the real file and
folder totals, and break them down by top-level entry. Then explain the shape in
the document: how many files and folders are yours, and how many belong to
`node_modules`, generated output, and tool-created directories. A tutorial that
says "the project has a `src` folder" without saying what fraction of the 46,000
files on disk are the reader's own code teaches the wrong mental model, and the
reader cannot tell which files they may edit. Never quote a count you did not take
from the machine — an invented number here is worse than no number, because the
reader will use it to decide what is safe to touch.

**Do not skip a file because it seems obvious.** Generated files, lock files,
config files that nobody reads by hand, the folder a tool creates for itself —
they all get an element. If a file exists in the finished project, the reader
will meet it, and a reader who finds an unexplained file learns to distrust the
whole document. If a file is created by a tool rather than by hand, say which
tool and when, because then it is predictable; if it was created by hand at some
point in the work, it needs a step like any other.

**A directory that holds only generated output gets a different kind of element.**
It does not need a build step; it needs a sentence saying who writes it, when, and
that deleting it costs nothing but time. `node_modules` and `release` are the two
largest directories in most projects by file count, and both are fully explained
by "run this command, get this, never edit it by hand."

Every element answers three questions before any code appears:

- **What it is** — one or two sentences, plain language
- **Why it exists** — what problem in the program it solves
- **What breaks without it** — concretely. "The app starts but the window has no
  title bar" beats "it is required"

That third question is what makes the tutorial teachable. A reader who
understands consequences can reason about code they have never seen.

**Grouping inside one file is allowed when the lines genuinely share a single
idea, but every line inside the group must still be named.** A JSX block whose
attributes all describe one button is one idea; a state declaration next to an
effect next to a handler is three. Grouping is a reading aid, not a licence to
write "and the rest is similar" — the reader cannot check that claim, and it is
usually false.

## How much is enough

Every rule above pushes in one direction: explain more. That is right on a project
with thousands of files and ruinous on a project with one. A tutorial that runs to
880 lines about a file of eight bytes is not thorough, it is a warning.

**This section is the counterweight, and where it disagrees with the rest of the
skill, it wins.**

**Count the elements before planning any chapter.** Open the project, list what is
actually there, write the number down. This number decides volumes and the contents
listing — it does not decide how many chapters:

| Elements in the project | Volumes | Shape of the document |
|---|---|---|
| 1 to 9 | none | One flat run of chapters. No contents tree |
| 10 to 40 | none | One flat run of chapters |
| 40 and up | only if parts stand alone | Chapters, and a contents tree worth reading |

The table bounds the scaffolding, not the work. A single file can still need three
chapters if it hides three separate things worth finding; nine files still do not
need nine chapters just because there are nine of them.

**A chapter has to earn its place.** Ask what is true when it is finished. "The
reader now knows that `Out-File` rewrites the file it was given" is an outcome.
"The reader now knows about the `config` file" is not — that is an element, and
elements live inside chapters, several to a chapter when they share one idea.

**Do not compare the chapter count against the element count.** They count
different things and the ratio means nothing. A chapter is a phase; an element is
a thing. One file honestly fills four chapters — created, inspected, read,
understood — and that is four outcomes, not four ways of padding. **The only test
is whether every chapter ends somewhere true.**

**The three questions are owed to what deserves explaining, not to every byte.** A
two-line `.gitignore` does not need a paragraph. It needs one sentence inside the
chapter that mentions it, saying who reads it and what happens if it goes missing.
"Do not skip a file" means *do not leave it unmentioned*, not *give it equal
space*.

**When two rules of this skill pull opposite ways, the smaller document wins.** No
discussion, no weighing. "Explain every element with three questions" is the more
emphatic rule and it is not the more important one. Aiming at fewer words is
almost never the mistake; missing something the reader will hit is the mistake.

**Two tells that the structure has already gone wrong.** Both are cheap to check
before handing anything over:

- **A paragraph defending the structure.** If the document explains why two volumes
  were the right call, there should not be two volumes. Structure you have to argue
  for gets cut, not justified.
- **A chapter number that skips.** `1, 2, 3, 11` means chapters were planned and
  abandoned. It usually also means a section that belongs at the end of a chapter
  became a chapter — check whether that content is really *abandoned
  approaches*, which is not a chapter and never was.

**Some projects should not get a book.** When the honest answer is "there is
nothing here beyond what the artifact already shows", write the short page: what
the thing is, what was measured, the one real trap if there is one, and a plain
statement that the build history is not available. Sixty honest lines beat four
hundred padded ones. **A tutorial is not evidence that the agent worked hard.**

## Steps: write the code live

After the element's three questions, write the steps. This is the heart of the
document and it is prose, not tables. Narrate the way you would to someone
sitting next to you: here is what we type, here is why, here is what it would
cost us to leave it out.


The three questions below are asked of every step. Where the reader works in
an application rather than in code, each of the four chapters in Part II says
what changes and what does not.

Each step contains code and answers three questions, in prose, not as labels:

- **Why we write this** — the reason the line exists
- **What we are writing** — what it actually does
- **What happens to the program if we do not write it** — the consequence

**Every line gets all three, or the step is not finished.** A block of twelve
lines needs the reasoning and the consequence for all twelve. One paragraph that
gestures at the block and then names two lines is the failure this skill exists
to prevent, because that is exactly how a tutorial quietly turns back into a code
listing with captions.

Grouping is allowed when the lines genuinely share a single idea, and the group
still has to name every line inside it. "These four settings all describe the
build, and each one alone changes where the output lands: `outDir` for the
folder, `target` for the JavaScript level, `emptyOutDir` for whether stale files
survive, `base` for the paths written into the result" covers four lines. "These
are the build options" covers none.

**A file may legitimately span volumes.** When one file holds several unrelated
things and only some of them belong to this chapter, it is fine to show part of
it and stop. What is not fine is stopping silently, because the reader then meets
the untouched remainder later with no idea why it is unfamiliar. So say it, and
be specific about where the rest of the file goes:

> The menu half of this file is not ours to build yet — it exists here because the
> window creation below refers to it. We come back for the rest in Volume III,
> where the interface is designed.

A promise of that kind is a promise: if a volume announces that a file will be
finished elsewhere, that other volume has to finish it. Note promises like this
where the volumes are listed, so you can check at the end that every one was
kept.

The same rule applies to the consequence. If a file has five options, the reader
should be able to learn five different ways to break the program, because that is
what they will actually do. Two consequences for five options teaches them two.

Write it alive. Address the reader, use "we". Show the code first, then explain
it in sentences that read like speech rather than like a reference table. Group
a handful of related lines into one explanation when they serve one idea, and
split a line out on its own when it carries a decision.

Example of the shape:

> We start with the one line the whole app hangs on. In `electron/main.ts`:
>
> ```ts
> import { app, BrowserWindow } from 'electron'
>
> app.whenReady().then(() => {
>   const win = new BrowserWindow({ width: 1200, height: 800 })
> })
> ```
>
> **Why we write this.** Electron has no window until the app reports that it
> finished booting, and `whenReady` is that report. Anything visual has to wait
> for it.
>
> **What we are writing.** Three things. The import brings in the two Electron
> pieces we need. `whenReady().then` schedules work for after boot.
> `BrowserWindow` creates the window, and we hold it in a variable.
>
> **What happens if we leave it out.** Without the import, `app` is undefined
> and the app dies on startup. Create the window before `whenReady` and we get
> `ERR_ELECTRON_BEFORE_READY` and an immediate exit. Drop the `const win` and the
> window flashes for a fraction of a second and disappears — that one is nasty,
> because it looks fine the first time.

Why prose and not a table: a table of "what each line does" is reference
material, and reference material is not what teaches somebody to build. The
value is in the reasoning being visible next to the code.

## Errors: what happened, and what will happen

Two kinds, and the reader needs both. Keep them distinguishable.

**What actually happened** — errors from the work, quoted verbatim. If the
console printed `EBUSY: resource busy or locked`, write that, not "a file lock
error". A paraphrased message cannot be searched for when the reader hits it.

**What the reader will hit** — errors typical of this stack, tool or platform
that we happened not to hit. Put these in the step where they occur: a missing
native dependency, a wrong runtime version, a path separator, a permission
problem, a stale build cache.

Predicting these is reasoning, not memory, and it should read that way. Where you
are confident, say what the reader will see and why. Where you are not, say so:
"this usually fails on a machine without the toolchain, the exact message
depends on the version".

**Never invent a past error.** If a step went cleanly, write "nothing went
wrong here" and move on. A tutorial with manufactured problems is worse than no
tutorial: it trains the reader to expect failures that never occur and hides the
ones that did.

## Abandoned approaches

Briefly, with the reason they were dropped, **at the end of the relevant chapter.**
Knowing that the obvious approach does not work saves the reader exactly the time
it cost us.

**This is a section inside a chapter, never a chapter of its own.** It has no
outcome of its own to check, so it cannot satisfy the definition of a chapter — and
the moment it is promoted to one it inherits a chapter number that does not belong
to it. That is how documents end up with a chapter 11 in a four-chapter book, and
then with a paragraph explaining why the numbering looks strange.

**If you are writing about your own wrong conclusions and wondering what number to
give the section, it is not a chapter.** It goes at the end of the chapter where the
mistake was made, which is also where the reader needs it.

## On someone else's project

This still works, with one part unavailable.

**Available, and fully so**, because it is deduced from the code rather than
remembered: the structure, what each element is, why it exists, what breaks
without it, and the errors the reader will hit. Reading a function that never
checks a return value is enough to predict what happens when it fails. Nothing
about that needs the session history.

**Unavailable:** what actually went wrong while building it, and which
approaches were tried and abandoned. Nobody recorded those, so do not write
them. Where the tutorial would normally carry a real error from our own work,
say plainly that this part is reconstructed from the code rather than from the
build, and let the reader judge it.

If the user can tell you what happened — they built it, or they watched someone
build it — ask. That converts an inferred tutorial into a true one, and it is
worth one question.

# Part II — Other kinds of project

The four chapters below are for when the reader has an application open rather
than an editor. They do not restate the method — they say what stays, what
changes, and what each medium has to teach on its own.

## What carries over, and what changes

Everything above assumes elements are files and steps are lines of code. The
structure survives; only the vocabulary changes. What does not change is the
core: volumes, chapters, elements with three questions each, and steps written
live so the reader can follow along.

**What an element is.** It is the thing the reader will go back to look at when
something is wrong later. For code, a file. For a scene, an object, a rig, a
material. For a game, an asset, a Blueprint, a level. For a drawing, a layer, a
pass, a palette. For a spreadsheet, a sheet, a named range, a formula, a pivot
table, a chart. For a document, a heading level and a section. For a deck, a
slide and the master it inherits from.

**What a step is.** In code, a step writes code. Elsewhere, a step performs an
action the reader can reproduce, and names it exactly: the console command, the
menu path, the exact setting with its value, the tool with its parameters.
"Adjust the lighting" is not a step. "Viewport shading to Rendered, render
samples from 64 to 256" is a step.

**Reading the project first.** This still applies, but the project is read in
whatever form it takes. A Blender file can be opened and inspected, including
its objects, modifiers and keyframes, so much of the structure is real data. An
Unreal asset is binary, so read it through the engine's tools rather than as
text. A drawing is only an image, and the layer structure is whatever the file
format happens to keep. A workbook is a binary container whose sheet names, used
ranges, formulas and external links are all inspectable — read them rather than
guessing what the report probably contains. An image file's resolution, profile
and layer count are in its header. Where a format genuinely cannot be read
without its tool, say so instead of describing what such projects usually look
like.

**Errors look different.** Code fails loudly and quotes a message. A scene fails
quietly: the effect is present but wrong, the light is there but flat, the bone
does not deform. Name the symptom so the reader recognises it, because there is
no error text to quote.

## Office programs

Spreadsheets, documents and slide decks. The reader has the application open and
the cursor in a cell, a paragraph or a slide.

**What does not change.** Elements still answer what it is, why it exists and
what breaks without it. Steps still answer why, what, and the consequence. The
document structure, the volume rules and the stopping rule in Part I all hold.

**What changes.** Three things, and they are enough to build a chapter on.

*Nothing is a file the reader can look at.* A cell showing `1852297` is not a
value the reader can inspect; it is a value the reader has to ask about. So the
element is the **formula and the range**, and the tutorial's job is to put the
address in the reader's hands where the application did not.

*Nothing is a program that reports failure.* A spreadsheet that divides by an
empty cell does not throw. It returns an error value, or a zero, or a wrong
answer that looks entirely reasonable. So **the failure mode in this medium is a
plausible wrong value**, and every step needs its check stated as a number the
reader can compare.

*The application's own labels can be wrong.* A stored format, a word count, an
author field — these are text written once, and nothing updates them. Where a
label disagrees with a measurement, **the measurement wins and the cause is
marked as assumed.**

**A step here is what the reader does in the application.** A menu path with the
value it takes, a style being applied, a formula entered with its cell
addresses. Never an edit to the XML inside the file, because the reader was
never given that file to open and has no reason to.

**Quote menu labels from the application, not from memory.** They drift between
versions and between office suites, and a wrong path costs more than a wrong
sentence. If the application's language files are reachable — in a spreadsheet
or word processor they usually are — take the label from there and say which
version you took it from. Otherwise write the path in the language the
application actually shows and name the application and version.

**The file format keeps one job: checking what the application wrote.** Sizes,
counts, densities, and whether a stored label matches reality are all verifiable
there. Put that in a closing section — it is not padding, it is the part of the
document the reader trusts most, because the numbers came out of the artifact
rather than out of the author.

### Spreadsheets and analysis

This is the medium with the worst error-to-loudness ratio of anything documented
here. Code stops when it is wrong. A spreadsheet keeps calculating a wrong answer
confidently, and the more elaborate the analysis, the longer it stays wrong.

**What an element is.** A sheet, a named range, a single formula worth
explaining, a pivot table, a chart, a conditional formatting rule, a data
validation rule, a source sheet that feeds the others, and the file as a whole
when the file layout is itself a decision. Not the cells individually — nobody
narrates cell B4. The unit is the thing a reader would come back to when the
number is wrong.

**What a step is.** A formula, written out with its cell addresses and its
arguments, exactly as it sits in the file. This is the whole discipline:

```
D12:  =SUMIFS($D$2:$D$11; $B$2:$B$11; "приход")
```

Addresses are the variable names in this medium. `$` is the absolute reference
and its absence is the bug waiting to happen — see the failures below. "Посчитали
выручку по месяцам" is not a step, and neither is "посчитали выручку" followed by
a screenshot of the result. The reader must be able to retype it.

**Read the file before writing about it.** A workbook is a binary container, but
its contents are inspectable: sheet names, used ranges, formulas per cell, named
ranges, and external links are all recoverable. Do that before claiming anything
about its size or shape — the same rule as counting project files, and for the
same reason. If you cannot read it with tools, say so plainly rather than
describing what spreadsheets usually look like.

#### The failures worth teaching early

Every one of these produces a plausible wrong number and no message.

- **A range that did not shift.** Insert a row above `SUM(D2:D11)` and the sum
  silently skips the new row. Nothing turns red. This is the single most
  expensive failure in a spreadsheet, because the number is wrong for months.
  Mitigations worth explaining: absolute references, converting the source range
  to a table, or a named range defined over the whole column.
- **A constant typed where a reference belongs.** `=D12*1.20` instead of
  `=D12*F3`. It works on the one machine where `1.20` was right, and nobody
  knows why the report differs in another office.
- **A circular reference.** A cell that depends on a total that includes it. The
  spreadsheet either refuses, or shows a warning the analyst clicks away, and
  the value becomes zero or stale without further comment.
- **An external link to another file.** Works perfectly until someone moves or
  mails the workbook. The value stops updating and the file keeps opening
  happily with the last known numbers.
- **`#N/A` from a key that looks identical.** A lookup fails on a trailing space,
  a different dash character, a different capitalisation, or a number stored as
  text. Half the table goes blank and the total is understated.
- **A pivot table nobody refreshed.** The layout is convincing and the numbers
  are from three weeks ago. Nobody notices because the pivot still looks like
  data.
- **Floating point in money.** `0.1 + 0.2` is not `0.3` in binary. Summing
  thousands of rows drifts, and the total is off by a kopek. Anyone who has
  reconciled a report knows this feeling, and the fix (round at the point of
  display, or work in integer minor units) is worth writing down.
- **Sums that skip text.** `SUM` over a range containing stray text ignores it
  rather than complaining, so one typo in a numeric column quietly understates
  the result.
- **A hardcoded date.** `=DATE(2026;1;1)` in a report that is supposed to be
  current. Every month the same mistake is made again.

**Where the number comes from.** This question has no analogue in code and it is
the most important one in this medium. In code you can read what a formula does.
In a report you cannot see where the source figures came from, who entered them,
or when. So the tutorial has to say it: which sheet is the source, whether it is
imported or typed, how often it is refreshed, and what happens when the source is
late. A forty-sheet report where nobody can name the origin of the base figures
is worthless no matter how many formulas it contains, and this belongs in the
chapter like any other design decision.

#### Versioning, which is not what a code reader expects

A workbook is binary, so `git diff` on `.xlsx` is close to useless: every save
changes internal metadata and produces a wall of changed bytes. Two consequences
worth a short section:

- **Sheet naming is the commit history.** Naming sheets by their meaning
  (`01_Исходные`, `02_Расчёт`, `03_Отчёт`) and never reusing a name keeps the
  workbook navigable across months. Reusing a sheet name for different content
  destroys the reader's ability to compare two periods.
- **One workbook per period, or a sheet per period, but never both.** A file
  called `Отчёт_final_v3_новый.xlsx` cannot be trusted. If the reader can find
  only one file that matters, name it by period.

#### Charts and conditional formatting

A chart is an element, not decoration, and it has a "what breaks" answer: a chart
built on a fixed range stops showing new rows, and the reader keeps believing it.
Say whether the range is dynamic.

Conditional formatting is the same story — a rule applied to a fixed range quietly
stops applying below it. State the range.

### Documents and plain text

A text document is the easy case and still has one trap. Its elements are the
structure: heading levels, sections, tables, lists, references, and any template
the file follows. Its steps are the actions: which style to apply, which section
to insert, where.

**The trap is style used directly instead of a named style.** Text that was
formatted by hand looks identical to text that follows the document's styles, and
the difference only appears when someone changes the style. So: **what breaks
without the styles** is that the document can no longer be re-styled, the table of
contents cannot be regenerated, and no one can find anything by structure. If the
document has headings, an element for each heading level is warranted. If it is a
plain letter, say so and do not invent structure.

#### Where this medium and code meet

The honest and useful place to end the chapter: **a spreadsheet is a program
written in a language nobody version-controls.** That single sentence earns its
keep for the whole chapter, because every rule follows from it — absolute
references, one number per cell calculation, no hidden logic, and the obsession
with naming. Say it once, early, and the rest of the chapter reads as
consequences rather than as arbitrary advice.

### Decks and presentations

A deck is the case where the medium of the steps is decided entirely by whether
the reader is looking at the tool or at the file, and where it is very easy to
pick the wrong one.

**The rule that decides it: a step is what the reader does in the program.** Not
what happens to the file underneath. A reader making a presentation has the
application open and a slide on screen. A step that describes editing
`slideLayout7.xml` teaches them something they cannot perform, in a tool they
cannot see, on a file they were never told to open.

The file format is not the wrong subject — it is the wrong *medium for the
steps*. Keep it for the one job only it can do: **checking what the program
actually produced.** Sizes, densities, counts, and whether a label matches
reality are all verifiable there, and that verification is worth a closing
section.

This applies wherever the reader has an application open, not only here. In an
engine it is the editor and console, not the asset's import settings file. In
Blender it is the operator and its panel, not the mesh data block. In a drawing
program it is the brush and its size, not the layer's channel data.

#### What an element is, operationally

| Element | What it is | Why it exists | What breaks without it |
|---|---|---|---|
| Slide | one screen of the talk | the unit the audience sees | one screen of the talk disappears |
| Layout | the arrangement a new slide inherits | new slides come out consistent | every new slide is placed by hand |
| Master | the base all layouts descend from | theme, fonts, and footers live here | nothing global can be changed once |
| Theme | colours and fonts in one place | change it and everything follows | a font change means editing every slide |
| Notes | text beside the slide, never shown to the audience | the speaker's script | the speaker reads from the screen |
| Media file | the image, video or audio as stored | the picture data | the slide shows an empty frame |

**A slide is a phase, not a file.** "The audience sees the title and one picture"
is an outcome. "The reader knows what `slide2.xml` contains" is not — that is
teaching the format.

#### Slide size is arithmetic, and it is decided first

Slide dimensions are stored in EMU, where one inch is 914 400. The two sizes a
reader will meet:

| Preset | Stored value | In centimetres |
|---|---|---|
| Standard 4:3 | 9144000 × 6858000 | 25,4 × 19,05 |
| Widescreen 16:9 | 12192000 × 6858000 | 33,9 × 19,05 |

Show the working, and let the reader divide by 914 400 or by 360 000 themselves —
once they can do it, they can check any deck they are handed, including one
somebody else made.

**Aspect ratio is chosen before anything is placed, and changing it moves
everything.** Layouts store positions as fractions of the slide, so switching
from 4:3 to 16:9 after laying out a deck re-flows the whole thing. So the format
is step one, before the first word is typed, and the check is opening the size
dialog and reading two numbers — on screen both formats look like "a rectangle".

#### The inheritance trap, which is the real lesson in decks

A slide that only has placeholders carries **no geometry of its own.** Its shape
properties are empty, and position, size and font come from the layout. The
chain is:

```
theme  →  master  →  layout  →  slide
```

This is worth a section of its own, because it explains three things at once:
why dragging a placeholder is usually a mistake, why a font change belongs in
the theme rather than on the slide, and why a deck drifts from its template when
someone is in a hurry.

**The step that teaches it:** open the size and position panel for a placeholder
that was never dragged. It shows the layout's numbers. Drag it once, and it now
shows its own — and has stopped following the layout.

#### Rotation is stored in sixtieth-thousandths of a degree

`<a:xfrm rot="20102623">` is 335,04°. A user typing `335` gets exactly 20100000.
**So an angle that does not come out to a round number was set by dragging the
handle, not typed.** That is a free forensic read on any deck, and it is how you
tell a deliberate tilt from someone fiddling and leaving it.

Say so when you find one, and recommend walking the shapes and checking the
rotation field before saving. Non-zero rotation on ordinary body text is almost
always an accident.

#### Images: three numbers, and the third one is the problem

Any picture in a deck has three measured properties, and all three should appear:

| What | Where it comes from |
|---|---|
| Pixel size | the image file |
| Declared density | usually 96 dpi, a default nobody sets |
| Size on the slide | the placeholder or the size panel |

**The check worth doing every time** — divide the two and compare:

```
689 px ÷ 96 dpi        = 7,18 in   what it measures at its own density
12,2 cm ÷ 2,54         = 4,80 in   what it is actually given on the slide
7,18 ÷ 4,80            = 1,49      so it is enlarged by half again
```

Then divide width by height on both sides. If they agree, the image was enlarged
but not distorted — say so, because it is good news and it answers the question
the reader will ask next. If they disagree, one axis was stretched and that is a
different problem with a different fix.

An image enlarged past its native density is invisible on a laptop and obvious on
a projector or in print. That asymmetry is the reason to teach the division at
all.

#### Three deck-specific failures worth their own sections

- **A deck drifts from its own template.** Slide 40 uses a different colour
  because someone was in a hurry, and nobody notices until it is projected. The
  "what breaks" answer is consistency, and every later change costs more than the
  original did.
- **Font embedding.** A deck that looks right on the author's machine and falls
  back to a substitute everywhere else. Name the fonts and say whether they are
  embedded.
- **Print versus screen.** A dark deck printed on paper inverts into something
  unreadable, and the fix is a light variant.

#### Metadata lies, and the reader will meet it

The file carries a human-readable format label, a creation date, an author, a
word count, a revision number. **Every one of these can be wrong or empty, and
the file format stores numbers that cannot be.**

So: where a label disagrees with a measurement, believe the measurement and mark
the cause as assumed. A deck whose properties say 4:3 while its stored size is
16:9 is common, and a program that trusts the label when printing will put a
widescreen slide on a 4:3 sheet.

Empty author and title fields are the same failure in a quieter form: the deck
loses its name the moment it is emailed, and nothing reports it.

## Game engines

Unreal Engine 5, Unity, Godot, and the rest. The reader has the editor open, with
a viewport, an outliner, a console and a details panel.

**What does not change.** Everything in Part I. Elements, three questions, steps
written live, real errors quoted, and the stopping rule all apply unchanged.

**What changes.** The project is not one codebase but **two**: assets on disk,
and the engine's own data structures derived from them. So an element in an
engine project is usually a *pair*, and the pair is where the bugs live — an
import setting that contradicts the file it imports, a lightmap that was baked
before the light moved, an asset that was never reimported after the source
changed.

**The reader's editor is not the deliverable.** A UE5 project is a folder of
assets that only means anything to the engine. So **the "what breaks without it"
answer is almost always about the engine reading it wrong**, not about the file
being absent: the mesh imports at the wrong scale, the texture loads uncompressed
on a mobile target, the material falls back to a default because a shader
compiled out.

**The console is the error channel, and it is often the only one.** An import
warning does not stop the editor; it scrolls past and is never read. So errors
in this medium are **warnings, not exceptions**, and the tutorial has to say
which are safe to ignore and which are the kind that ruin the project quietly.

**A step is a tool call, a console command, or a menu path with its value.**
`Actor → Add Component → Static Mesh`, not "add a mesh component to the actor".
`stat fps` in the console, not "check the frame rate". Where an action has both a
button and a command, give the command — it is copyable, and buttons move
between versions.

**Quote menu paths from the engine's own source or its localisation files where
you can.** The editor is a program with strings in it, and those strings are the
exact labels the reader will see. Name the engine and the version.

### Games on an engine

Elements are assets and the connections between them: project settings, plugins,
Blueprints, actors placed in a level, meshes, materials, textures, animation
sequences and skeletons, interface widgets, effects, and data assets.

Two failures cost more time than the rest and are worth teaching early:

- **It works for you and for nobody else.** Replicated movement, server
  authority, networked state. A property or call that was never marked for
  replication passes the single-player test and simply does not exist for
  anyone else. No error appears anywhere.
- **A reference lost on rename.** Renaming a variable, function, asset or socket
  without catching the referencers leaves Blueprints that no longer compile,
  sometimes in files nobody touched that week.

Volumes for a game project usually fall into project setup, content, gameplay,
interface, effects, and packaging. The last one earns its keep in a tutorial,
because signing and platform packaging fail in ways that are hard to diagnose
from inside the editor and easy to prevent when written down.

### Blueprints are code

A Blueprint graph is code with the code hidden behind pictures. Treat it exactly
as you would treat a source file: write the graph out live, and for every block
answer why we added it, what it does, and what happens to the program if it is
not there.

**Writing the graph out.** A tutorial cannot show a picture of a node graph and
call that an explanation, so put the graph into text. Unreal can read a graph
and hand it back as a small S-expression language, and can write a graph from
that same text. That means the tutorial prints the actual graph instead of
describing it. In a 5.8 engine those are `read_graph_dsl` and
`get_graph_dsl_docs` for the syntax, with `write_graph_dsl` to apply a change.
Use whatever your engine exposes, but the point stands: get the graph into text
before you try to explain it.

**What is worth annotating.** The event that starts the chain, every branch that
changes what happens, every call whose return value is used, and the
connections between them. Skip node positions and cosmetic settings. The reader
is typing the graph, not reproducing a screenshot.

**What breaks, specific to graphs:**

- **A node that fails to compile takes the whole Blueprint with it.** Not just
  the node: everything that referenced it stops working, and sometimes does so
  without any visible error of its own.
- **Execution pins come first.** Connect the exec chain before the data pins. A
  graph with data wired but exec wired loosely will compile and run in an order
  nobody intended.
- **Pure nodes recalculate on every wire.** An output from a pure node feeding
  several inputs is recomputed each time it is read. Cache it into a variable
  when the value is used more than once, or the cost multiplies invisibly.
- **Look pin and node names up rather than guessing.** A plausible wrong name
  costs a failed compile and no explanation of why.

The same treatment applies to the other graph-based work in the engine: material
graphs, effect graphs, procedural graphs and rigging graphs are all code in a
different visual language. They deserve the same three questions per block.

## 3D programs

Blender, Maya, Houdini, ZBrush, Substance Painter. The reader has a viewport,
an outliner and a properties panel.

**What does not change.** Everything in Part I.

**What changes.** Three things, and all three are consequences of one fact: **the
scene is a calculation, not a record.** A mesh is not a list of points, it is the
current output of a chain of operations. A material is not a set of colours, it
is a graph being evaluated. Nothing is saved until it is applied.

*Therefore nothing is an element until it is applied.* The element the reader
will go back to is the applied result — the mesh, the UV layout, the baked map —
and the operations that produced it are steps. A tutorial that calls a modifier a
file gets the categories backwards.

*Therefore the destructive step is the one worth teaching.* Applying a modifier,
merging meshes, flattening a layer stack: each one throws away the ability to
change your mind. Every one of those steps needs what was lost named, and whether
an undo path exists.

*Therefore the numbers are the deliverable.* In 3D the only parts of the work a
reader can verify without your eyes are the measurements: vertex counts, texture
dimensions, object scale in metres, polycount budgets. **These are read off the
artifact, never estimated**, and they are what a reader who cannot see your
viewport will actually check.

**A step is an operator and its panel value.** `Object → Scale → 0.01`, not "set
the scale to 0.01". `Shift+S` with the cursor over the mesh, not "enter edit mode
and scale". Give the value, because the value is the part the reader forgets and
the part that has to be right.

**Name the tool, not the intention, and say which one you mean.** "Bevel" is a
modifier in Blender, an operation in Maya, and a tool in ZBrush, with three
different parameter names. Where a workflow moves between programs, name the
program with every action, every time.

### Blender: models, animation, render

Elements are scene data: collections, objects, modifiers, armatures, bones,
vertex groups, shape keys, actions and keyframes, materials, the camera, the
lights, the world, and render and output settings.

Three things go wrong so reliably that they are worth teaching up front rather
than as something to recover from:

- **Scale left unapplied.** An object created or rescaled in object mode carries
  a transform that was never baked into the mesh. Physics, rigid bodies,
  booleans and every exported format then disagree about its size.
- **Modifier order.** Modifiers are applied in a fixed sequence, and changing
  that order changes the result, sometimes catastrophically and without any
  warning.
- **Smooth shading across hard edges.** Rounded, melted-looking surfaces,
  tedious to undo once vertices are already deformed.

For animation, keyframe interpolation is the single setting that decides whether
motion reads as mechanical or natural. Give the value and the reason. "Smooth it
out" is not a step.

### Beyond Blender: Maya, Houdini, ZBrush and the rest

The Blender section above is specific to one tool. The rules that generalise
across 3D software are the ones worth writing down, and they are worth separating
from the tool-specific vocabulary, because a reader moving from Maya to Houdini
needs to know which of the Blender advice carries over and which does not.

#### What is the same everywhere

These four hold in every 3D package, and stating them once saves the reader from
rediscovering them per tool:

- **Applied versus unapplied transforms.** A scale left unapplied in object mode
  is a latent disagreement: physics, rigid bodies, booleans, modifiers, and every
  exporter each compute size differently. Apply before you start, not after
  something looks wrong. Blender's rule, and it is universal.
- **Non-destructive is the default where it exists.** Keep the modifier stack or
  the node graph live, apply only at export. The one exception is geometry so
  heavy it must be baked to stay workable, and that decision is worth writing down
  when made.
- **Modifier and node order is semantic.** Reordering a stack changes the result,
  silently. Same in Blender, same in ZBrush's subtools, same in a Houdini chain.
- **Naming is not cosmetic.** A scene with `Cube.003` in the outliner cannot be
  debugged by anyone including its author. Name on creation, and explain in the
  tutorial why that rule matters more in 3D than in code: in code a wrong name is
  a compile error or a searchable string, in a scene it is just confusion in a
  list.

#### Maya

The distinctive thing about Maya is its evaluation model, and it is the thing
worth teaching first.

- **DG nodes evaluate silently and globally.** Changing a value on one object
  can trigger a re-evaluation across half the scene, and a non-local connection
  between two nodes will recompute when only one of them appears to have changed.
  A tutorial about Maya that does not mention evaluation is teaching the reader a
  mental model that will lie to them.
- **Nodes vs. connections vs. plugs.** The plug system (uniform, unit, render
  type, data type) is where real bugs live, and it has no visual equivalent in
  other tools. A curve node's input order swapping silently inverts a mapping.
- **Shape vs. transform locks.** Locking the wrong one produces objects that
  cannot be posed, or worse, transforms that look applied but are not.
- **Namespace collisions on import.** Importing a second version of the same rig
  without a namespace gives you silently doubled nodes where one set of curves
  drives half the character. This is the Maya equivalent of a lost reference, and
  it is worth a warning section.

#### Houdini

Houdini is procedural code, and the honest way to document it is that way.

- **Nodes and wires are statements and data flow.** Treat a network the way the
  Blueprints section treats a graph: annotate every node that changes behaviour,
  every branch, and every parameter whose value is doing work. Node positions are
  not worth narrating.
- **The cook cache is the number one time sink.** Caching, locking, and
  invalidating are the practical knowledge; a tutorial that skips them produces
  readers who spend an hour per frame change. Say what to lock and why.
- **Time and randomness need seeding explained.** A random value that changes
  between cooks is the 3D version of a non-deterministic build: the same input
  yields a different output, and nobody can tell whether the change came from the
  scene or from the noise.
- **Parameter exposure is the real interface.** Exposing a parameter instead of
  hard-wiring it is what makes a setup reusable, and it is the Houdini analogue of
  the config options we put in `package.json`. Say which parameters were exposed
  and why.

#### ZBrush

- **Subtools, not objects.** The unit of editing is the subtool, and its
  subdivision level is part of its identity. Losing track of which subtool was
  soloed is the classic lost-work moment.
- **Polypaint is vertex colours.** Colors here are data, not display, and they
  export as textures. If a texture is being painted elsewhere, note which side
  owns it, because duplicate ownership is a real conflict.
- **Destructive by design, so back up the .ZTL before major work.** This is the
  honest exception to the non-destructive rule, and it should be stated as a rule
  rather than assumed.

#### Substance Painter and texture authoring

This sits between the drawing section below and 3D, and it deserves its own
treatment because "painting a texture" is neither of the two.

- **The stack is layers, masks and generators**, and it is non-destructive the way
  an adjustment layer is. That is the structural parallel with raster work.
- **Anchor points are the non-obvious part.** The set of anchor points determines
  the UV layout of the result, and changing them late repaints the texture. This
  is the 3D analogue of "you cannot un-blend a flattened layer", and it belongs in
  the tutorial.
- **Channel sets decide what a material can use.** Painting into a channel the
  material never reads looks fine in the tool and does nothing in the engine.

#### Engine handoff, which every 3D tutorial must cover

The asset leaves the DCC tool and enters an engine, and this is where a large
fraction of real problems come from. A 3D tutorial that ends at export has
stopped before the interesting part.

Cover, explicitly:

- **Scale at import.** One unit in the package is one unit in the engine or it is
  not, and getting it wrong makes every asset wrong in the same way, which reads
  as a lighting problem and is not.
- **LODs and their trigger distance**, and what happens if one is missing.
- **Naming collisions in the engine**, which is where the rename failure from the
  engine section arrives from the other direction.
- **A lit check in the engine**, not just a preview render. Materials that look
  right in Substance can be wrong under the engine's lighting and its missing
  texture load, and the tool that could see the difference was the wrong one.

#### Errors, which in this medium are pictures

A 3D failure does not quote a message. The symptom is a wrong image, and the
tutorial's job is to make the reader recognise it:

- black or pink-and-white checkered surface → the engine has no texture at that
  path, not a material problem
- everything shifted or scaled wrong on import → unit mismatch
- normals inverted on one object → face orientation was reversed on export
- a modifier that "does nothing" → it is below another modifier in the stack and
  its output is being overwritten
- a texture that repainted when something unrelated changed → anchor points moved,
  or the UV shell was re-laid out

## Drawing programs

Krita, Photoshop, Procreate, and the rest. The reader has a canvas, a layer
stack and a toolbar.

**What does not change.** Everything in Part I.

**What changes.** The work is **marks on a surface**, and the surface is
destructible and versionless — there is no undo across sessions unless the file
was saved as a layered document.

*So the layer stack is the element, and the history is not.* A reader coming back
to a drawing will go to the layer that is wrong, not to the stroke that made it.
That makes the layer the unit worth naming, and it makes the layer count a
measured number rather than an estimate.

*So the output size is decided before the resolution, never after.* Choosing
canvas size after painting means the brush strokes are already the wrong size.
This is the one decision that cannot be taken back, so it belongs in step one.

*So every colour value needs a profile, and every export needs settings.* The
same RGB number means different things on a screen, on paper and in print. Name
the profile wherever a colour appears, and name the destination that forced the
choice — that is what makes the number reproducible.

**A step is a tool, with its size, its angle and its colour.** "A soft round
brush at 40 px, hard pressure at 20 % flow, `#1A2330`" — not "a dark stroke".
The three settings are the step; the description of what it should look like is
the check, and the check belongs after the action, not instead of it.

**Errors here are pictures, not messages.** Nothing throws. So an error section
for a drawing is a description of the visual symptom and how to recognise it,
which is harder to write and worth more than a stack trace would have been.

**Quote tool names from the program.** They change between versions, and a
tutorial that says "the eraser" when the button says "Erase whole stroke" sends
the reader hunting through the toolbar.

### Raster images, layers and export

The drawing section above covers the idea of a deliberate mark with known
parameters. This section is the raster-editor reality behind it: non-destructive
stacking, the arithmetic of resolution, and the places where a file that looks
right on the author's screen is wrong everywhere else.

**What an element is.** The document, the canvas and its resolution, each layer
with its kind and its blend mode, each mask, each adjustment layer, each smart
object, the colour profile, and the export settings. Layers matter more than
pixels here, because layers are what makes later correction possible — and that
is the whole "what breaks" story for this medium.

#### Non-destructive is the default, and flattening is irreversible

The single rule this medium has, and everything else follows from it.

- **Adjustment layers instead of painted corrections.** A curves or levels
  adjustment can be re-tuned later; a correction painted into pixels cannot be
  undone except by rebuilding the pixels.
- **Masks instead of erasing.** A mask hides and can be revealed; an eraser
  destroys.
- **Smart objects for anything placed.** Placed artwork inside a smart object
  keeps its source and can be re-placed; placed raw, it cannot.
- **Never flatten to "clean up", never.** State the concrete cost: a single
  flattened layer means every remaining fix is permanent, and the layer names
  that carried the meaning are gone.

The "what breaks" answer for layers is therefore always the same and should be
given in these terms rather than as an aesthetic preference.

#### Blend modes are arithmetic, and they are not what they look like

A blend mode is an operation on values, not a visual style, and two things about
it are worth teaching because they produce results people cannot reproduce:

- **Multiply darkens towards the darkest layer; screen lightens towards the
  lightest.** Both preserve contrast in the opposite direction from the naive
  expectation, which is why a multiply-layered shadow layer looks like a shadow.
- **Opacity and fill opacity are different.** Fill ignores the layer's own
  transparent pixels, opacity does not. The same slider produces visibly
  different results on a layer with transparency, and the tutorial should say
  which one it used and why.
- **A mode on an empty layer does nothing**, because there is nothing underneath.
  This is the raster equivalent of a pure function fed nothing.

#### Resolution arithmetic, stated as a formula

This is the calculation readers get wrong most often, so write it as an equation
and give the worked numbers:

```
pixels = physical size × dpi
A4 (297 × 210 mm) at 300 dpi  →  3508 × 2480 px
A4 at 150 dpi                →  1754 × 1240 px
```

And the reason 300 dpi is the default for print and 72 is the screen default:
a dot is physical, a pixel is not, so "the image looks fine" means nothing until
the output size is fixed. **Say the output size first, then the resolution.** A
tutorial that opens with "set the canvas to 3508 × 2480" has taught the reader to
copy a number without the reasoning that would let them do a different paper
size.

#### Colour management, which is the closest thing here to a silent build error

- **The profile is part of the file, and it changes the pixels.** The same RGB
  values with an sRGB profile and a Display P3 profile are different colours. An
  image without a profile is assumed sRGB, which is a guess.
- **"Looks right on my screen" is exactly "works on my machine".** Screens vary in
  gamma and in profile; the file does not care what the reader's monitor shows.
- **Convert at export, not in the middle.** Assigning a profile into an image
  that is already tagged changes pixels; exporting with the right profile does
  not.
- **Pick the profile from the destination, and say which one:** sRGB for screens
  and general web, Display P3 for wide-gamut display work, CMYK only for a print
  shop that asked for it.

The analogy to a web project is exact and worth drawing: the hard-coded
`#11131a` and the mismatched `#171a22` from an Electron project are the same class
of mistake, one colour value used in a context that expects a different colour
space.

#### Formats, alpha and what gets thrown away

- **PNG** for anything with hard edges, transparency, or text. Lossless, alpha
  kept.
- **JPEG** for photographs only. It has no alpha and its artefacts are worst
  exactly where the eye goes — gradients and saturated edges.
- **WebP or AVIF** for web, and state the export settings rather than "exported
  optimised": quality setting, alpha, and the lossless flag if used.
- **Naming the export is an element.** `icon-16.png`, `icon-32.png`, and the
  folder of sizes for Linux are a decision with a reason (the platform reads the
  size from the filename), and that reason belongs in the tutorial.

#### What breaks, in this medium

- The image was flattened before export → no way to fix the one thing the
  recipient complained about
- Resolution was chosen before the print size → soft edges at the required size,
  or a file 40 times too large
- The profile was assigned in the middle of the work → every colour shifted, and
  the cause is four steps back
- Transparency lost on export → the black background is not a bug in the viewer
- A layer's mask dragged to the wrong layer → the correction appears in the wrong
  place, and its own layer is still correct, which is deeply confusing
- JPEG used for an icon → blocky edges on every flat colour

#### Reading an image file before writing about it

Resolution, colour profile, embedded colour space, and layer count are readable
from the file header, so the numbers in the tutorial can be real. Where they are
not readable — a proprietary layered format read without its editor — say so
instead of guessing, per the same rule that governs reading someone else's
codebase.

### Drawing and image work

Elements are the parts of the picture: canvas and resolution, layers, the
palette and its values, the passes of the work, and the final presentation.

There is no code to annotate, so the analogue of a line is a single deliberate
mark with known parameters: the tool, its size, its angle, its colour, the
direction and speed of the stroke. Record those. A reader who is told a form was
built from three passes, dark to light, no outline, can reproduce it. A reader
told it was "shaded a bit" learns nothing.

Layers exist so that later corrections do not destroy earlier decisions, and
that is the "what breaks without it" for this kind of work: a single flattened
layer means every fix is permanent.

## Checklist before handing it over

**Any project**

- The opening explains what is being built and why, before any detail
- The contents listing matches the actual volumes, chapters and elements
- Format was asked about, not assumed
- Every element answers what it is, why, and what breaks without it
- No table substitutes for the explanation anywhere
- Actual errors are quoted verbatim
- Anticipated errors are present and marked as predicted
- No past error is invented; clean steps say so
- Where a medium has no error message, the error names the symptom instead
- Outside code, every step names the exact action and its value, never the
  intention — "adjust the lighting" is not a step, "render samples from 64 to 256"
  is
- Abandoned approaches sit at the end of the chapter they belong to, never in a
  chapter of their own
- The first stage assumes nothing — a reader who has never touched this machine
  can begin there
- Elements are counted from the machine before chapters are planned, and named
  for the medium: assets and actors for a game, objects and modifiers for 3D,
  layers and passes for a drawing
- Every chapter ends somewhere true, stated as a check the reader can run
- No element was given a chapter of its own for being an element
- No paragraph defends the structure, and chapter numbers run without a gap
- Where two rules of this skill conflicted, the smaller document won
- If the project was too small to hold a book, the document says so and stays
  short rather than padding to fill the format

**Code**

- Code appears in steps with prose answering why, what, and the consequence
- A step that writes to disk says what lands there — that is usually the whole
  answer to "what breaks without it"
- Anticipated errors are placed next to the code that causes them, not collected
  at the end

**Office programs**

- No step asks the reader to leave the office application they have open
- Menu labels are quoted from the application and the version is named
- Spreadsheet formulas are written with their cell addresses, and the source of
  every input figure is named
- Where a stored label disagrees with a measurement, the measurement is
  presented as fact and the cause as assumed
- For a deck: the slide format is chosen and read back before anything is placed
- For a deck: where the font and colour actually live is named — theme and
  master, not the slide
- For a deck: every image has its pixel size, its declared density and its size
  on the slide, with the enlargement worked out and distortion checked

**Game engines**

- No step asks the reader to leave the engine editor, and every action is a tool
  call, a console command, or a menu path with its value
- Where a console command exists for an action, the command is given rather than
  the button
- Warnings are distinguished from fatal errors, and the project-breaking ones are
  named as such
- Import settings that must agree with the imported file are stated as a pair

**3D programs**

- Resolution arithmetic is shown as pixels = size × dpi with worked numbers, and
  the output size is decided before the resolution
- A colour profile is named wherever a colour value appears, and the destination
  that dictated the choice is stated
- Every destructive step names what was lost and whether undo or a backup exists
- Flattening, merging or applying is never presented as cleanup
- Engine handoff is covered: unit scale, LODs, naming collisions, and a lit check
  inside the engine rather than only in the tool
- Object scale is stated in real units, not as a bare multiplier

**Drawing programs**

- Counts quoted to the reader — layer counts, resolutions — were taken from the
  artifact, not estimated
- The output size is decided before the first mark is made
- Every stroke step names the tool, its size, its angle and its colour
- Export settings are written down rather than left as "save and see"

