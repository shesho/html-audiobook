---
name: html-audiobook
description: Generate long-form HTML explainers, tours, summaries or reports that hold up when read aloud by a screen reader or listened to as narration. Use this skill whenever asked to produce an HTML page, artifact, or standalone .html file that explains a codebase, repository, architecture, set of documents, research findings, or any complex subject to a reader, especially for onboarding, handover, a strategic review, or a non-technical audience. Also use it whenever the user mentions accessibility, screen readers, narration, listening instead of reading, ADHD or divided attention, listeners who pause and resume, or asks for a self-contained single HTML file with no external dependencies. Apply it even when the user never says "audiobook", as long as the deliverable is an explainer page someone will listen to or read from start to finish.
---

# HTML Audiobook

Documents written for the eye and documents written for the ear fail differently. On screen, a reader who loses the thread scans back up the page in half a second. A listener cannot. They hear one sentence at a time, in order, with no way to glance at a heading, and they pause and resume hours later with nothing on screen to reorient them.

Everything below follows from that single constraint, and from two things that are true of most of the people who listen.

The first is divided attention. Many listeners have ADHD, and many others are walking, cooking or commuting while the document plays. Attention drops out for ten or twenty seconds at a time and then comes back. A document written for sustained attention loses these listeners at the first drop and never gets them back.

The second is the pause. People listen to a long document in pieces, over days. They stop mid-section and resume with no memory of the previous sentence and nothing on screen to remind them. Every section, and to a large extent every paragraph, has to work for someone who arrives at it cold.

Both realities point the same way: keep the units short, name the subject constantly, and never make a sentence depend on a sentence the listener may not have heard.

One counterweight governs all of it. Simplicity is a property of the explanation, never of the facts. A sentence gets simpler by putting a plain gloss beside a real name, not by deleting the name, and a document that says "an outside service" where the source says LangSmith has not been simplified. It has been made less true. Rule 18 draws that line, and every other rule below is read subject to it.

Note on scope: these rules govern the HTML document you produce. They do not govern your chat replies, your notes, or any skill files you write.

Note on language: the examples below are written in English because that is the shortest way to show each point, but none of the rules are about English. They are about what survives being spoken. Write the document in whatever language the reader needs, and apply the principle rather than matching the phrasing. Every language has its own vague pronoun, its own interrupting parenthesis, and its own heading that sounds clever and says nothing.

Some languages make a rule matter more, not less. Spanish and Italian normally drop the subject pronoun altogether, so a sentence can run for a whole clause before the listener learns who is being discussed. Naming the subject explicitly matters more there than it does in English, not less.

## Workflow

1. Gather the real material first. Read the repository, the documents, the data. An explainer built on guesses reads fluently and teaches nothing. While gathering, keep a private note of where each fact came from: which report, which file, which dashboard, which search. Rule 19 asks the document to say how each verdict is known, and the fact-checker in the review pass verifies those pointers. A ledger kept during gathering costs nothing. Reconstructing one afterwards costs a great deal.
2. Decide the through-line: what the reader should understand by the end, and in what order the pieces have to arrive for that to happen.
3. Write the first draft following the document structure and the rules below.
4. Run the adversarial review described in "The adversarial review" and fold everything it surfaces back into the draft.
5. Reread the revised draft as a listener rather than as a reader. The last section below describes what to listen for.

`references/page-template.html` is a starting skeleton with the theme handling and typographic scale already set up. Copy it and replace the content rather than deriving the CSS again.

## Document structure

### The executive summary

The document opens with a section titled "Executive Summary": one summary of the entire document, around 300 words. Write it for a 17-year-old intern in their first week: non-technical language, clear, friendly, educational. No silly or childish metaphors, and no dumbing down of the facts. Just say plainly what the document covers, what the main findings or mechanisms are, and why they matter. Name the products, vendors and figures in the summary exactly as the body does. A summary that says "an outside company" where the body says LangSmith has hidden the finding from the one reader who stops there.

A reader who stops after the executive summary should still leave with a correct, complete picture of what the whole document says. Summarise the subject, never the document: "our platform stores every job application in one database" carries content, "this document walks through our architecture" does not.

A verdict in the summary still says how it is known, under rule 19, and the summary has room for only one shape: the forward pointer. "The reservation data is often wrong, and section 7 shows why." The reader who stops here still hears that the evidence exists and where it sits.

### The opening summary of each section

Every section opens with a summary of about 40 words in the simplest language the subject allows. The summary says what the section covers and what the listener should take away from it.

This summary carries no label and no visual frame. It is not titled "Summary", it is not set in a box, it is not given a border or a tinted background, and it is not marked with any wrapper that a screen reader would announce. It is the first paragraph of the section, and it has to read as the natural opening of the prose, so that a listener hears one continuous piece of writing rather than a preamble followed by the real thing.

The summary is what rescues the listener who paused for a day and resumed here, so it has to be self-contained. Name the subject in full, in the first sentence, with no pronoun reaching back to an earlier section.

The summary follows every other rule in this document, and the metacopy rule especially. "This section explains the job queue" is about the document and is wasted breath. "The job queue is where slow work waits so the website can answer people instantly" is about the subject, and it is the one to write.

DON'T:
```html
<div class="summary">
  <p class="label">Section summary</p>
  <p>In this section we will look at how the job queue works.</p>
</div>
```

DO:
```html
<p>The job queue is where slow work waits so the website can answer people instantly.
   When somebody uploads a file, the website hands the work to the queue and replies
   straight away, and a separate program picks the work up a moment later and finishes
   it in the background.</p>
```

### Section length, and telling the listener where they are

Keep sections short enough to finish in one sitting: roughly 400 to 700 words, which is about four minutes of narration. A section that runs longer is two sections that have not been separated yet, and a listener with divided attention will lose the thread somewhere in the middle of it.

Number the sections and say the total, so a listener always knows their position in the document and can find their way back after a pause. The template puts this in a small line above the section title, reading "Section 3 of 9". This line and the bridge described next are the only copy about the document itself that earns its place. Keep it to that one short line and let the metacopy rule govern everything else.

### The bridge into the next section

Every section ends with a single short line that hands the listener into the next one, the way a podcast host does before a break. The listener hears the pause, then the heading, and the bridge is what makes that heading land as expected rather than as a jump. Write it from the beginning, as the natural last sentence or two of the section. A bridge added afterwards reads as bolted on.

Keep it casual, short, and about the subject rather than about the document. A question the listener is already forming works well, and so does a plain turn of thought: what is left to cover, or what the section just described leaves unresolved. "The next section covers the tools" announces the document. "So what tools are actually available for this? Not many, and one of them is broken." announces the subject and gives the listener a reason to keep going.

Vary the shape from section to section. A listener notices when every section ends with the same words, and the bridge stops sounding like a person and starts sounding like a template. Sometimes a question, sometimes a statement, sometimes half a sentence of what comes next, and occasionally, when a section closes on a strong line of its own, nothing at all.

The bridge is not a summary of the section that just ended. Closing recaps are still cut under rule 6. The bridge only looks forward, and it stays to one or two sentences. Where a section ends in a list of entries, the bridge goes after the last entry, as a paragraph of the section, so it is heard right before the pause.

DON'T:
```
In the next section we will look at the seven data stores.
That concludes the overview of the two kinds of data.
```

DO:
```
So where does all of this information actually live? In seven different places, and two of them quietly delete themselves.
```

## The adversarial review

After the first draft is written, launch four subagents in parallel. Each one receives the full draft, poses no edits itself, and returns findings for you to act on. The first three work from the draft alone. The fourth is different in kind: it also receives the location of the material the draft was built from, and it has tool access, because its job is to go and look.

1. **The clarity reviewer** reviews for clarity, straightforwardness and simplicity of language. It flags obscure metaphors, excessive jargon, overreliance on abstractions, and convoluted ideas, quoting each offending passage so you can find it. It never flags a product, vendor, company or environment name as jargon. A name is information, and the remedy for an unfamiliar one is a plain gloss beside it, which the reviewer may ask for, never removal.
2. **The intern** poses as a 17-year-old intern who is new to the project and asks the basic questions the document should answer but might not: what a term means, why something exists, how two parts connect, what happens when something fails, and which actual product or company is behind a phrase like "an outside service" or "a monitoring tool".
3. **The interrupted listener** reads only the first two paragraphs of each section, in isolation, with every other section hidden. It reports each section where those paragraphs do not say what the section is about, lean on a pronoun with no antecedent, refer back to something the listener would not have heard, or open with anything other than a roughly 40-word plain summary. It also flags every heading that names a thing without naming its category and position, every path or exact large number, and every paragraph longer than about four sentences.
4. **The fact-checker** receives the draft and access to the material the draft was built from. It lists every claim that carries a verdict word or a figure, and for each one reports one of four states: supported, with the pointer already in the text; supported but unanchored, with the spoken-form pointer it found for you to add; unsupported, because it searched the material and found nothing; or contradicted, quoting what the material actually says. It verifies a pointer that is already present rather than trusting it, by opening the named report or section and confirming it says what the claim says. It checks that every forward pointer lands in a section that actually holds the evidence. It never proposes evidence it did not itself find, and it reports an opinion presented as a fact as unsupported. Rule 19 defines what counts as a claim and what counts as a pointer.

The fact-checker is the slowest of the four because it opens sources, which is why it runs in the same parallel batch rather than after the others.

Then revise the draft yourself:

- Rewrite every passage the clarity reviewer flagged, or justify keeping it.
- Where the clarity reviewer wants a name softened and the intern wants to know what the name is, both are right: the name stays and a plain gloss goes beside it. Rule 18 says how.
- Answer every intern question naturally and explicitly inside the existing document structure, in the section where the answer belongs. Never bolt on a FAQ, a Q&A appendix, or a "common questions" section. If a question has no natural home, that is a sign a section is missing or the order is wrong, and the structure is what to fix.
- Fix every opening the interrupted listener could not follow. Fixing these usually means naming the subject again, which costs a few words and is always worth it.
- Add every pointer the fact-checker found, in one of the spoken shapes rule 19 allows. Downgrade or cut every claim it could not support: "we could not confirm" is an honest sentence, and an evidence-shaped sentence with nothing behind it is not. Where it found a contradiction, the source wins, and the claim is rewritten to match.
- Rewrites from the clarity reviewer tend to strip trailing clauses, and the trailing clause is where the evidence usually sits. The last pass re-checks for this.

## The rules

### 1. Write for a listener who cannot see the page

Screen readers announce structure. They do not convey layout. Anything you express through position, colour, or adjacency is lost.

Give the document a skip link to the main content, wrap the body in `<main>`, label any navigation, and let the heading outline carry the structure. Decorative characters get `aria-hidden="true"` or get deleted, because a screen reader will happily announce "times" for a stray multiplication sign used as a bullet.

DON'T:
```html
<div class="grid">
  <div class="col"><span>✕</span> Never bypass the security rule</div>
  <div class="col"><span>✕</span> Never skip the adapter</div>
</div>
```

DO:
```html
<ul>
  <li>Never bypass the security rule.</li>
  <li>Never call an outside service without going through an adapter.</li>
</ul>
```

### 2. Inline every style, reference nothing external

The document has to render identically offline, on a plane, in an email attachment, and inside a sandbox that blocks outside requests. One `<link>` to a font service is the difference between a finished artifact and a broken one.

Put the whole stylesheet in a single `<style>` block. Use system font stacks. Embed any image you truly need as a data URI, and prefer having no images at all.

Design both themes at the token level. Define the complete palette on bare `:root`, redefine only the tokens inside `@media (prefers-color-scheme: dark)` guarded as `:root:not([data-theme="light"])`, and redefine them again under `:root[data-theme="dark"]`. A colour whose only definition sits inside a media query never applies when the viewer's theme is unset, which is the single most common way these pages end up unreadable.

DON'T:
```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter">
<link rel="stylesheet" href="styles.css">
```

DO:
```html
<style>
:root { --ink: #14161D; --ground: #FBFBFD; }
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) { --ink: #E9EAF0; --ground: #0E0F14; }
}
:root[data-theme="dark"] { --ink: #E9EAF0; --ground: #0E0F14; }
body { background: var(--ground); color: var(--ink);
       font-family: ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, sans-serif; }
</style>
```

### 3. No tables, no cards

A screen reader reads a table cell by cell, announcing column headers before each value. Three columns of prose become an unlistenable stutter. Card grids are worse, because their meaning lives in visual adjacency that narration destroys entirely.

Convert both into prose or into a plain list where each item opens with a bolded lead-in. The conversion usually improves the writing, because a table lets you omit the connective reasoning that prose forces you to supply.

DON'T:
```html
<table>
  <tr><th>Queue</th><th>Carries</th><th>Why separate</th></tr>
  <tr><td>etl</td><td>Ingestion, snapshots</td><td>General lane</td></tr>
  <tr><td>pms-sync</td><td>Browser logins</td><td>Slow and fragile</td></tr>
</table>
```

DO:
```html
<ul>
  <li><b>The general lane</b> carries data ingestion and snapshot building, which are
      small database jobs that play nicely alongside each other.</li>
  <li><b>The reservation-sync lane</b> is kept separate because it drives a real web
      browser, so it is slow and prone to failure, and it must never clog the rest.</li>
</ul>
```

### 4. Name sections plainly, never cleverly

A listener hears a heading once, with no surrounding page to disambiguate it. "Here, it runs" and "Where it bites" sound knowing on screen and mean nothing in audio. The heading is a signpost, and a signpost that needs decoding is a failure.

DON'T: `Here, it runs` · `Where it bites` · `The developer's view` · `Under the hood` · `The blindfold` · `What the numbers whisper`

DO: `How this project uses it` · `Downsides` · `Why developers choose it` · `How the login check works` · `Why the AI has no database access`

The same applies to the document title. Name the subject, do not tease it.

When the heading names one of a run of similar things, it needs its category and its position as well as its name. Rule 15 covers that.

### 5. Name the subject instead of saying "it"

This is the rule that most improves narration and the one most often skipped. A listener who resumes after a break, or whose attention drifted for two sentences, has no antecedent for "it". Repeating the noun costs a few words and rescues the whole paragraph.

Open every section, and every paragraph that starts a new idea, by naming the thing being described. Inside a paragraph, "it" is fine once the subject is established and no competing noun has appeared since.

DON'T:
```
The win developers actually feel is in the editor, not the compiler.
Developers like it because the type hints they would write anyway do triple duty.
It is wired in and, as of the last update, not actually in use.
These tests run in a simulated browser rather than a real one.
```

DO:
```
The win developers actually feel with TypeScript is in the editor rather than the compiler.
Developers like FastAPI because the type hints they would write anyway do triple duty.
LaunchDarkly is wired in and, as of the last update, is not actually in use.
The Vitest tests run in a simulated browser rather than a real one.
```

Sections that list competitors need the same anchor, or the listener thinks the topic has changed: write "Instead of Redis, teams often reach for Memcached" rather than opening cold with "Memcached does caching only".

### 6. Cut copy that describes the document instead of the subject

Narration has no scroll bar, so every sentence spends the listener's time. Sentences about how to read the page, how the section is organised, or why the section exists are pure overhead. Trust the heading.

DON'T:
```
In this section, we will explore the four main components of the system. Each
component is described using a consistent structure so you can skim the ones you
need and skip the rest. Read this part even if you skip everything else.
```

DO:
```
The system is four programs, and each one exists because a different kind of work
needs a different guarantee.
```

Delete "how to use this page" sections, "what you will learn" preambles, and closing paragraphs that summarise what was just said. A short opening that establishes the subject is not metacopy. A paragraph about the document's own structure is.

There are two exceptions, and only two. The short "Section 3 of 9" line above each section title is navigation for a listener who paused the narration yesterday and needs to find their place, and it pays for its four words. The one-line bridge at the end of each section, described under document structure, hands the listener into the next heading, and it pays for itself only when it is about the subject rather than the document. Nothing else about the document earns its place.

An evidence pointer is not metacopy. "The sync data is often wrong, and section 11 shows why" is a sentence about the sync data, and the pointer tells the listener where the proof sits. Rule 19 asks for these, and this rule does not cut them.

### 7. Only `<h1>` and `<h2>`

Deep heading trees are a visual convenience. In audio, "heading level four" is noise, and listeners navigating by heading get a confusing outline. One `<h1>` for the document, `<h2>` for everything else, and let CSS classes carry any visual difference between a section title and an entry title.

DON'T:
```html
<h2>Backend</h2>
  <h3>FastAPI</h3>
    <h4>Downsides</h4>
```

DO:
```html
<h2 class="section-title">Backend</h2>
<h2 class="entry-title">FastAPI</h2>
<p class="field-label">Downsides</p>
```

Sub-labels below the entry level work better as styled paragraphs than as headings, since they are read in sequence anyway and do not deserve a slot in the navigable outline.

### 8. No em dashes

Screen readers handle the em dash inconsistently. Some announce nothing and run two clauses together, some pause oddly, some read the character name aloud. Commas, colons, semicolons and full stops all narrate predictably.

DON'T: `Celery is the default — capable, and a frequent source of quiet pain — which is why teams keep it.`

DO: `Celery is the default. Celery is capable, and also a frequent source of quiet pain, which is why teams keep it rather than migrating away.`

Often the em dash was hiding a sentence that wanted to be two sentences. Splitting it improves the writing as well as the narration.

### 9. Keep parentheses rare

A parenthesis makes the narration interrupt itself. The listener holds one thought suspended while a second one runs, then has to recover the first with no visual bracket to help.

Fold the aside into the sentence, promote it to its own sentence, or cut it.

DON'T: `The scheduler (which runs as a separate process called beat, and is configured from one shared file) drops jobs onto the queue.`

DO: `A separate process called beat acts as the alarm clock. Beat reads one shared schedule file and drops each job onto the queue when it comes due.`

Short parentheses carrying a figure or a plain gloss are acceptable in small numbers. Nested or clause-length parentheses are not.

### 10. Avoid the "one X, several Ys" construction

"One system, five layers" and "one root cause, four symptoms" read as punchy and are a tic. They arrive with a rhythm that signals cleverness rather than meaning, and a document that leans on them starts to sound generated. Say the thing plainly.

DON'T: `One database, two locks.` · `Four apps, one purpose.` · `One rule, three consequences.`

DO: `The database is protected by two separate locks that do not depend on each other.` · `There are four programs, and all four exist to serve the same job.`

A title may occasionally earn this shape when it is genuinely the subject of the document. In body prose it is almost always worth rewriting.

### 11. Avoid the "not X, but Y" construction

The corrective frame implies the listener held a wrong belief and needs correcting. Used once it lands. Used repeatedly it becomes a mannerism, and it forces the listener to process a negation before reaching the actual claim, which is harder in audio than on the page.

DON'T: `Measurement is not enforcement.` · `This is not a preference, it is what integrating with a legacy industry looks like.` · `The problem is not the tool, it's the process.`

DO: `Measurement tells you a problem exists. Enforcement is what stops the problem from shipping, and those are separate settings.` · `Driving the interface is the only option available, because that industry predates modern web standards.`

State the positive claim. Reach for the negation only when the wrong belief is genuinely widespread and worth naming.

### 12. Write in plain language, and explain every technical term in the sentence where it appears

A listener cannot hover a definition or scroll back to a glossary. Any term you use unexplained is simply lost, and the sentences after it are lost too.

Explain in ordinary words at the moment of first use, and prefer a short concrete sentence to a precise abstract one. Keep the narrative moving: a document that reads as a story is much easier to follow by ear than a list of facts, because each part gives the listener a reason to expect the next. Narrative here means causal momentum, not theatrical vocabulary; rule 13 covers where that goes wrong.

DON'T: `The API enforces RLS via a session-scoped GUC, so tenant isolation holds even if the ORM query omits the org filter.`

DO: `Before running any query, the code tells the database which customer is asking. The database then refuses to return rows belonging to anybody else. That protection holds even when the application code forgets to filter, which is the whole reason it works this way.`

Avoid file paths, function names, column names and code blocks unless the reader will type them. Describe what the code does instead, and see rule 16 for how to name a piece of code out loud. That advice is about identifiers, which are strings rather than words. The names of products, vendors, companies, environments and services are words, and they stay in the sentence with the plain explanation beside them. Rule 18 draws the line. If the user has asked for code, keep it in a clearly introduced block and say in prose what the block demonstrates, so a listener who skips it loses nothing.

### 13. Use a metaphor only to explain a mechanism, never to organise the document

A metaphor earns its place by making a mechanism easier to understand. Comparing a job queue to a kitchen ticket rail teaches something real: the waiter clips the order up and walks away instead of standing there while it cooks. The reader now understands why the request returns immediately. That comparison did work.

Naming your sections after a theatre production does no work at all. "The cast of characters", "Before the plot, meet the actors", "Act one", "Our journey through the pipeline": none of these explain anything about the subject. They dress the structure up as friendly, and friendliness is not what they deliver. The listener hears several words before any content arrives, and then has to carry an irrelevant frame in their head while trying to learn something. Decorative framing is a cost with no return.

Apply two tests before keeping any metaphor.

First, does it explain how something works? If the metaphor only labels, groups, or introduces, it is decoration. Cut it.

Second, is it clearly better than the plain sentence? Write the plain version and compare. If plain language is equally clear, plain language wins, because it costs the reader nothing to decode and it cannot be misread.

DON'T, metaphor used as structure:
```
Section heading:  The cast of characters
Subheading:       Before the plot, meet the actors. You'll see these names everywhere.
Section heading:  Act one, the front door
Section heading:  Our journey begins
```

DO, plain structure, with the metaphor saved for a mechanism that needs one:
```
Section heading:  The four programs
Subheading:       These four names appear throughout the rest of this document.

...and later, where it genuinely helps:
The queue works like a kitchen ticket rail. The waiter clips an order to the rail
and goes back to the floor, and a cook takes it down when they have a free hand.
Nobody stands waiting for anybody else.
```

Note the tension with plain-language storytelling: narrative momentum comes from causal sequence, from each part giving the listener a reason to expect the next. It does not come from theatrical vocabulary. A document can be a pleasure to follow without a single actor, stage or curtain in it.

A metaphor or a category phrase never stands in for a name. "The short-term memory" as the only label for Redis, or "the recording service" once LangSmith has been introduced, is decoration wearing the costume of simplicity, and it leaves the listener guessing which real thing is meant. Say the name, and let the phrase sit beside it if the name alone would mean nothing. Rule 18 covers this.

When a metaphor is doing real work, stay inside it. Mixing two forces the listener to build a picture and then discard it, which costs more attention than plain description would have.

DON'T, mixed: `The strategy's ceiling also acts as the belt-and-suspenders for the team.`

DON'T, over-extended: having introduced the kitchen, going on to the head chef, the menu, the health inspector and the walk-in freezer long after the comparison stopped explaining anything.

DO: introduce the metaphor deliberately, extend it only while each extension clarifies something, and drop it cleanly before starting another.

### 14. Write for a listener whose attention keeps dropping out

Assume the listener misses ten seconds here and twenty seconds there, and that they stop the narration mid-section and resume it a day later. Write so that neither of those costs them anything.

Keep paragraphs to two to four sentences, each paragraph carrying one idea. A long paragraph gives attention nothing to hold on to, and a listener who drops out in the middle of one has no way back into it.

Keep sentences short and put the subject and the verb early. A sentence that opens with three subordinate clauses has already lost the listener by the time it says what it is about.

Never make a sentence depend on a sentence the listener may not have heard. Cut "as we saw earlier", "as mentioned above", "the latter", "this approach" and "that problem". Restate the fact in four or five words instead: the cost is small and the rescue is total.

DON'T:
```
As we saw earlier, the latter approach has the problem described above, which is
why the team avoided it here as well.
```

DO:
```
Copying the data twice keeps the two databases in step, but it also means a failure
halfway through leaves the two copies disagreeing. The team avoided copying the data
twice for exactly that reason.
```

Give each idea a plainly named home, and let the listener drop out of one and rejoin at the next. Frequent short sections with honest names beat a few long sections with clever ones, every time.

A pointer back to an earlier section is allowed when the sentence restates the fact first. "The sync job writes the field twice, which section 4 covered" gives the listener the fact and then tells them where the detail lives. "As section 4 showed" on its own gives them nothing and is still cut.

### 15. Number the items in a list of things, and name the category in every heading

Whenever the document works through a set of similar things, one after another, treat it like a spoken glossary. Every entry gets its own heading, and every heading carries three parts: the category, the position, and the name.

Write "Fruit 1: Pear", "Fruit 2: Strawberry", "Fruit 3: Orange", not "Pear", "Strawberry", "Orange". A listener who hears "Orange" on its own has no idea whether the document moved to a new topic or is still working through the same set. A listener who hears "Fruit 3: Orange" knows immediately that a new entry has started, which set it belongs to, and how far along they are.

Say the total when the set is closed, because the total tells a listener how much is left: "Fruit 3 of 5: Orange". Introduce the set once in the prose above the first entry, so the category word is already meaningful when the headings start.

DON'T:
```html
<h2 class="entry-title">Postgres</h2>
<h2 class="entry-title">Redis</h2>
<h2 class="entry-title">Elasticsearch</h2>
```

DO:
```html
<p>The platform keeps its data in three separate stores, and each one exists for a
   different reason.</p>
<h2 class="entry-title">Data store 1 of 3: Postgres</h2>
<h2 class="entry-title">Data store 2 of 3: Redis</h2>
<h2 class="entry-title">Data store 3 of 3: Elasticsearch</h2>
```

Choose the category word the listener would use, not the internal one. "Background job 2 of 6" is clear; "Worker class 2 of 6" is only clear to somebody who already knows the codebase.

The name part of the heading is the real name. "Data store 2 of 3: Redis" tells the listener what is being discussed; "Data store 2 of 3: The short-term memory" makes them guess. When the name alone would mean nothing to the audience, put the gloss after the name rather than in place of it: "Data store 2 of 3: Redis, the short-term memory".

### 16. Never speak a file path or an exact large number

A screen reader reads a path character by character, slash by slash, and the listener gets a stream of syllables with no meaning in it. Large numbers are the same problem in a different shape: an exact figure takes several seconds to say and the listener remembers none of it.

Name code the way a person would say it out loud. Say "the LanguagePicker service", not the path to the file that contains it. When the name alone would mean nothing to the audience, add "the part of the site that picks the language" beside it, and keep the name. Give the path only when the reader will actually type it, and then say in prose what the path is for.

Round every large number and say how you rounded it. "More than 25 thousand lines of code" tells the listener everything the exact count told them, in a fraction of the time. Write the scale word out as a word, because "25k" narrates unpredictably across screen readers. Keep the exact figure only when the exact figure is the point, such as a price, a legal threshold or a version number.

The same applies to anything else that is a string of characters rather than a word: commit hashes, identifiers, long URLs, database column names and API keys. Describe them, or leave them out.

This rule is about strings, never about names. "LangSmith", "Sentry", "the staging environment" and "the assistant events table" are words a voice can say, and rule 18 keeps them in.

DON'T:
```
The file at app/services/language_picker.tsx contains 25,659 lines and was last
changed in commit 4f7a91c.
```

DO:
```
The LanguagePicker service is the largest single piece of the front end, at more
than 25 thousand lines, and it was last changed in the release that shipped in March.
```

### 17. Control the narration pace with break tags

Headings are signposts, and a signpost read at the same speed as the prose around it stops working as a signpost. Build the pacing for reader apps: ElevenReader, Speechify, NaturalReader, and the read-aloud features built into browsers. That is how these documents actually get listened to.

Those apps extract the article text and throw away the markup and the stylesheet. Two consequences follow, and both are easy to get wrong.

**The CSS Speech module does nothing.** Support is thin everywhere, and a reader app never sees your stylesheet in the first place. It costs nothing visually, so it can stay in the page, but never treat it as the thing delivering your pauses, and never report pacing as handled because you wrote it. If you include it, do not set `voice-stress` on `strong` or `em`: where anything does honour it, the narrator hammers every emphasised word and the reading turns shouty.

**Break tags in the text are what actually work.** Reader apps honour SSML break tags found in the page text, which gives you exact, specified pause lengths. Escape the tag in the source so it renders as text rather than parsing as an element:

```html
<p class="brk">&lt;break time="2.0s" /&gt;</p>
<h2 class="section-title">The AI interviewers</h2>
```

```css
/* Invisible to the eye, still present in the extracted text. */
.brk { opacity: 0; font-size: 6px; line-height: 1; margin: 0; user-select: none; }
```

**Hide these with `opacity` and nothing else.** `display: none`, `visibility: hidden`, zero dimensions, and the clip-rect technique all remove the element from the extracted text, and the pauses stop without any visible sign that anything broke. The element has to stay rendered and keep a real box. If pauses ever fail, raise the opacity first to confirm the tags are still being rendered, before changing anything else.

Place the break before the whole heading unit, above the "Section 3 of 9" line rather than between that line and the title, or the pause lands in the middle of the heading.

**Never let CSS carry a separation the text needs.** The reasoning that governs the break tags governs every element whose visual separation comes from the stylesheet, because a reader app throws the stylesheet away and keeps only the words. The position line is where this bites most often. Marked up inside the heading as `<span class="hpos">Section 3 of 9</span>The job queue`, it renders as two neat lines and extracts as `Section 3 of 9The job queue`, which a narrator reads aloud as "nine the job queue". Every section heading in the document is quietly corrupted, and nothing about the rendered page shows it.

Put the separator in the text itself rather than in the CSS. Ending the span with a full stop and a space is enough: `<span class="hpos">Section 3 of 9. </span>`.

Both placements of the position line are defensible, and they trade against each other. As its own paragraph above the heading, the way `references/page-template.html` does it, the line extracts cleanly with no separator needed, but a screen-reader user navigating heading to heading jumps straight to the `<h2>` and never hears their position at all. Inside the heading, the position is announced on every jump, at the cost of needing that literal separator. Pick either one deliberately, and whichever you pick, verify by stripping the tags and reading the result, never by looking at the rendered page.


Useful starting durations: 2 seconds before a section title, 1.2 seconds before an entry title. Put no break before the document title. Narration starts there anyway, and a visible tag above the title is the first thing a sighted reader sees on the page. Silence after a heading usually needs no help, because most engines pause at a heading boundary on their own.

A note for the rare case where the listener uses a real screen reader instead (VoiceOver, NVDA, JAWS). Those read the accessibility tree, so a literal break tag is just noise to them, and a visually hidden span of full stops before the heading is what produces the pause. Everything else in this file applies unchanged either way.

### 18. Simplify the explanation, never the facts

The rules above ask for plain words, no jargon, no paths, rounded numbers and few metaphors. Followed without a counterweight, they produce a document that hides exactly the things a reader needs: which company holds the customer data, which product is installed and silent, which setting defaults to fake. "Data is sent to an outside service" sounds simpler than "data is sent to LangSmith" and says less, because the reader can no longer check the claim, find the dashboard, or ask the vendor. A plain sentence that omits a material fact is not plain. It is incomplete.

The line runs between identifiers and names. An identifier is a string of characters: a path, a hash, a column name, an environment variable, a key. A voice cannot say one usefully, so rule 16 describes it instead. A name is a word: a product, a vendor, a company, an environment, a service, a table spoken as words. A voice says it fine, and it is often the single most useful fact in the sentence. Identifiers get described. Names get said.

Simplify by adding, never by removing. The first time a name appears in a section, put the plain gloss beside it, in the same sentence: "LangSmith, the outside service that records every conversation with the AI assistant". Every later mention in that section uses the name alone. The gloss is what makes the sentence easy. The name is what makes it true. Deleting the name and keeping the gloss is the failure this rule exists to prevent.

Apply one test before dropping any specific: would a reader who acts on this document, or checks it, need the specific to do so? The vendor holding customer data, the product that is connected and silent, the setting that defaults to fake, the environment that is really production, the month a table stops accepting writes, the name of the table nothing writes to: yes to all of these. Which of three internal helper functions does the work: usually no. When in doubt, keep the name and add the gloss.

Because every section is written for a listener who arrives cold, the gloss repeats at the first mention in each section, the same way the subject's name does under rule 5. A listener who joins at section 9 hears "LangSmith, the AI recording service" once more, and that is a few words well spent.

DON'T:
```
The AI recordings are held by an outside company, continuously.
The service holds records for a limited time, and nobody has written down what that period is.
An internal document said the AI service was reporting its errors to a monitoring tool.
The first round claimed no file storage service exists. The infrastructure files define two.
```

DO:
```
LangSmith, the outside service that records every conversation with the AI assistant,
holds those recordings continuously.
LangSmith deletes its records after a period nobody at the company has written down.
An internal document said the AI service was reporting its errors to Sentry, the
error-tracking service.
The first round claimed the platform uses no file storage. The infrastructure files
define two Amazon S3 buckets.
```

The DO versions are no harder to listen to. Each is one name longer and one fact richer, and each can be checked by the person who hears it.

The same standard applies to headings under rule 15, to the executive summary, and to every rewrite the clarity reviewer proposes: the fix for an unfamiliar name is a plain phrase beside it, never a plain phrase in place of it.

### 19. Every verdict says how we know

A document that says something is wrong, missing, unused, broken or misleading has made a promise: that someone looked. The listener cannot see what was looked at, so the sentence has to say it. A verdict with no evidence beside it is a hot take, and a listener who wants to dig deeper has nowhere to go.

The evidence is short and spoken. One clause, in the same sentence or the next, in one of three shapes.

- **Point to a source the reader can open.** Name it the way a person would say it, under rule 16: "the fifth audit report", "the error dashboard for the API service", "the README of the sync service", "the last three weeks of worker logs". Never a path, a hash or a bracketed citation.
- **Point to the cause.** "The smoking gun is the API service, which writes the field before it validates it." A listener who knows the cause can check it themselves.
- **Point forward in the document.** "Section 11 shows why." The sections are numbered, so a listener can hold that. A forward pointer is a debt: the named section has to actually contain the evidence, and the fact-checker confirms that it does.

DON'T: `The data stored there is quite often wrong. On the other hand...`

DO: `The data stored there is quite often wrong, as the fifth audit report shows. On the other hand...`

DO: `The data stored there is quite often wrong, and the smoking gun is the API service. On the other hand...`

DO: `The data stored there is quite often wrong, and section 11 shows why. On the other hand...`

Three kinds of claim need extra care. A negative, such as "nothing writes to this table", says how the absence was established: "a search of the whole codebase finds no writer". A figure says where it was counted: "in a sample of two hundred rows, a quarter had no city". An opinion says that it is one, and names the fact it rests on: "in my judgement the queue is the weak point, because it is the only piece with no retry".

A claim that cannot be given evidence is downgraded, never dressed up. Write "we could not confirm whether the job still runs" rather than an evidence-shaped sentence with nothing behind it. Invented evidence is worse than none, because it survives every reviewer except the reader who goes looking.

Not every sentence carries evidence. A description of how something works is its own evidence when the reader can open the thing described. Verdict words are what trigger the rule: wrong, broken, missing, unused, never, always, every, nobody, misleading, dangerous, and any figure.

The evidence lives inline or not at all. Footnotes, endnotes, superscript markers and an evidence appendix are the obvious way to satisfy this rule on screen, and every one of them fails in audio: a screen reader announces "link, one" and the listener never reaches the note. Rule 16's exception for a path the reader will type is the only door for an identifier, and this rule does not widen it.

## Making it worth listening to

Everything above keeps a listener from getting lost. It does not, on its own, make them want to keep listening. Prose that is scrupulously plain can still arrive as a flat drone, especially through a synthetic voice that adds no warmth of its own, and a listener whose attention is already divided will drift away from a drone no matter how clear it is.

When a document needs to hold attention rather than merely be followed, reach for these. None of them conflicts with the rules above, and all of them survive being read by a machine.

**Vary the sentence length deliberately.** This is the single strongest lever, because a full stop is a pause and pauses are rhythm. Run a long explanatory sentence into a short flat one and the short one lands like a verdict. "Two months. That is how fast this category is being absorbed."

**Ask the question the listener is already forming, then answer it immediately.** This is the closest thing to a conversation a one-way document can manage, and it pulls a drifting listener back because a question implies an answer is coming. "So where is the danger? Not where the money is going." Keep the questions about the subject. A question about the document itself is metacopy, and rule 6 still applies.

**Voice the obvious objection before making the claim.** "Does that make LinkedIn unbeatable in Latin America? Look at the price first." The listener who was about to disagree now hears you disagreeing with yourself, which is far more persuasive than a claim delivered flat.

**Give a number its consequence in the next sentence.** A figure alone is inert in audio. "Roughly one application in eight was fake. At a company that builds fraud detection for a living."

**Give a verdict its evidence in the next breath.** "The nightly sync is broken. The worker logs show it failing every night since March." Evidence delivered immediately reads as confidence, and confidence holds attention far better than assertion does. Rule 19 asks for the evidence anyway, and placing it this close is what makes it land.

**Let a paragraph land on a short sentence** rather than trailing off into qualification. "Right product. Unproven business."

**Address the listener directly** where it is natural. "Read that list again." "Sit with that for a second."

The failure mode to avoid is hype. Expressiveness comes from rhythm, from questions, and from stakes that are really there. It does not come from adjectives, from exclamation, or from reaching for a metaphor, and rule 13 still governs metaphors no matter how energetic the piece is meant to be. If a sentence would embarrass you read aloud in a meeting, it will embarrass the narrator too.

## The last pass

Reread the draft the way it will be heard, one pass, from the top. You are listening for the moments where a listener would be lost, and those moments are obvious once you are looking for them.

Read the opening sentence of each section on its own, with the heading covered. Someone joining the narration at that exact moment has only that sentence. If it does not tell them what is being discussed, rewrite it.

Read each section's opening summary on its own and check it against the same standard: about 40 words, plain, self-contained, unlabelled, and reading as ordinary prose rather than as a preamble.

Pick a paragraph at random, pretend the listener rejoined there after a day away, and see whether it holds up. Any paragraph that only makes sense in sequence needs the subject named again.

Notice anywhere you had to look back to know what "it" referred to. A listener cannot look back at all, so every one of those is a place to name the subject again.

Say each heading out loud. A heading that needs the page around it to make sense will not survive being spoken.

Ask of each metaphor what it explained. If the answer is that it made a section sound friendlier, cut it and name the thing plainly.

Ask of each paragraph whether it is about the subject or about the document. Paragraphs about the document are the easiest words to cut and the ones a listener most resents. The two exceptions are the short "Section 3 of 9" line, which exists so a paused listener can find their place again, and the one-line bridge that closes each section.

Read the last line of each section together with the heading that follows it. The bridge should make the heading feel expected, and it should sound like a person talking rather than a document announcing itself. If three bridges in a row use the same shape, rewrite two of them, and if a section already closes on a strong line, let it.

Look at every list of similar things and check that each heading carries its category, its position and its name, so a listener always knows a new entry has started.

Look for anything a voice cannot say usefully: a file path, an exact count in the thousands, a commit hash, a long identifier. Replace each one with the name a person would use out loud, or with a rounded figure.

Then look for the opposite failure. Find every "an outside service", "a third-party tool", "the provider", "a monitoring tool" and "the recording service", and ask what its name is. If you know the name, write it, with a plain gloss beside it the first time it appears in that section. A reader who cannot tell which company holds their customers' data has not been given a simpler document, only a less useful one.

Then find every verdict word and every figure, and ask how the sentence says we know. Wrong, broken, missing, unused, never, always, every, nobody, misleading, and any count or percentage: each one either points to a source, a cause or a later section, or it is a hot take. Confirm every forward pointer lands in a section that actually holds the evidence. Then check the sentences the clarity reviewer rewrote, because a rewrite that tightens a sentence usually drops its last clause, and the last clause is where the evidence was.

Then confirm the page stands on its own: nothing loaded from outside, colours that resolve whether the viewer's theme is light, dark or unset, and a structure a screen reader can navigate.

Say the first sentence of a few sections out loud with some energy. If there is no way to read them except flatly, the writing is doing none of the work and no amount of stylesheet will rescue it.

Confirm every heading except the document title has a break tag before it, and that nothing hiding one uses `display: none`, `visibility: hidden`, zero dimensions, or clipping.

Then strip every tag from the draft and read the plain text that falls out, which is all a reader app ever sees. Look for words run together where the page showed a line break, headings above all. If the position line sits inside the heading, confirm it ends with a full stop and a space.

None of this is a gate to pass. It is the reading you would give the draft if you cared how it sounded, and it catches what matters far better than counting characters does.
