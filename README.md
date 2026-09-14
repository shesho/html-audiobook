# HTML Audiobook

A Claude Code skill that generates long-form HTML explainers you can *listen to*.

Point it at anything complex, a codebase, an architecture, a pile of documents, a
research question, and it writes a self-contained HTML page that holds up when a
reader app narrates it out loud. I built it to understand a large codebase while
doing something else, and it has worked better than reading the code would have.

It is optimized for [ElevenReader](https://elevenreader.io), which I recommend for
listening to any doc or page like an audiobook, and it works with Speechify,
NaturalReader, browser read-aloud, and real screen readers too.

## Why it is not just "write me an HTML doc"

Documents written for the eye and documents written for the ear fail differently.
A reader who loses the thread scans back up the page in half a second. A listener
cannot. They hear one sentence at a time, they listen while walking or cooking,
and they pause for a day and resume with nothing on screen to reorient them.

So the skill enforces a specific shape:

- **An executive summary** that leaves a reader who stops there with the whole picture.
- **Short sections**, four minutes of narration each, numbered ("Section 3 of 9") so a
  listener always knows where they are.
- **A 40-word plain opening** to every section, unlabelled and unboxed, so someone
  resuming cold is caught up in one paragraph.
- **A spoken bridge** at the end of each section, the way a podcast host hands you
  into the break.
- **Real SSML break tags** in the page text, so headings actually land as headings
  instead of running into the prose. Hidden with `opacity` only, because every other
  way of hiding them deletes them from what the reader app extracts.
- **No file paths, no hashes, no exact six-digit numbers.** A voice cannot say them
  usefully.
- **Names kept, jargon glossed.** "LangSmith, the outside service that records every
  conversation with the AI assistant" rather than "an outside service". Simplify the
  explanation, never the facts.
- **One self-contained file.** Everything inline, nothing loaded from outside, works
  offline and as an email attachment.

There is also an adversarial review pass: three subagents read the draft as a clarity
reviewer, as a 17-year-old intern asking the basic questions, and as a listener who
only ever hears the first two paragraphs of each section.

## Install

Clone it into your personal skills directory:

```bash
git clone https://github.com/shesho/html-audiobook.git ~/.claude/skills/html-audiobook
```

Or into a single project, at `.claude/skills/html-audiobook`.

Pull for updates:

```bash
git -C ~/.claude/skills/html-audiobook pull
```

## Use

Just ask for the thing. Claude picks the skill up on its own:

> Explain how the payments service works, as an HTML page I can listen to.

> Walk me through this repo for a new engineer. Audiobook-friendly HTML.

Or invoke it directly with `/html-audiobook`.

Then open the file in ElevenReader and go for a walk.

## What is in here

| File | What it is |
| --- | --- |
| `SKILL.md` | The skill: workflow, document structure, the review pass, and 18 rules. |
| `references/page-template.html` | Starting skeleton with the theme handling and type scale already set up. |

## Feedback

Comments, issues and PRs welcome. If a document it produced lost you somewhere,
that is the most useful bug report there is.
