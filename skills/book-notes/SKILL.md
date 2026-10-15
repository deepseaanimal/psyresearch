---
name: book-notes
description: "Write up a book, chapter or article into Diana's Notion reading system (Reading Sources, Book Chapters, Concepts). Claude writes the condensed theory and concept notes; Diana only answers two short reflection questions per chapter. Also files Highlights-app exports (Markdown or .textbundle) under the right chapter. Replaces highlights-to-reading-claims."
---

# Book notes: Claude writes, Diana reflects

## Who this is for
Diana is a head of digital and a leadership coach with chronic fatigue. She reads psychology and management books to reuse in her work, writing and coaching. She does **not** have time to write notes. Claude writes the notes; Diana adds only her own reflections and, optionally, highlights.

Everything must be short, concrete and on point. No filler, no study-guide tone.

## Triggers
- "Write up <book>" / "do the whole book" / "summarise this chapter for my notes".
- A Highlights-app export (pasted text, .md file, or .textbundle on Dropbox).
- An article, post or note she wants kept for reuse.

## Databases (Diana's Library → Reading Notes)
Fetch each data source first to confirm the current schema.
- **Reading Sources**: `collection://5a71f428-ae8c-826e-b016-0778dcf36ee4`. One row per book or article. Relations: `Chapters`, `Concepts`.
- **Book Chapters**: `collection://88a837f6-4539-4a88-9bd8-e6e706e323ef`. Properties: `Chapter` (title, "N · Title"), `Book` (relation), `No.`, `Status` (Claude draft / Reading / Read), `Theme`, `Concepts` (relation).
- **Concepts**: `collection://eacdff85-ac5c-4fd7-8bc2-c745f95ecfc2`. Properties: `Concept` (title), `One line`, `Kind` (Theory / Finding / Model / framework / Term / Practice), `Evidence` (Strong / replicated, Mixed / contested, Weak / failed replication, Lens / model, Practitioner view), `Sources`, `Chapter`, `Used in` (Playbooks), `Theme`, `Origin` (Claude synthesis / From my reading), `Checked by me`.
- **Playbooks**: `collection://2d81f428-ae8c-83a2-a2b7-07953bf80a7b`. `Concepts` relation backlinks from Concepts.`Used in`.
- **Reading Claims (archived Oct 2026)**: `collection://bf41f428-ae8c-8285-92d6-0767c9a488ce`. Read-only history. Never write new rows here.

Reference example of the finished format: the book page "Social Psychology (8th Ed)" (Hogg & Vaughan) and its 16 chapter pages.

## A. Writing up a whole book
1. **Resolve the Source row.** Fuzzy-match the title in Reading Sources. If missing, create it (Type = Book, Status = Reading). Fill Author, Year and Citation only from facts you have verified (the person, the export, or a web search of the publisher or a library catalogue). Mark anything unverified "(check)". Never invent a publisher, year or edition.
2. **Get the real table of contents.** Search the web for the edition's chapter list before writing. If you can't confirm it, say so and ask.
3. **Write one Book Chapters page per chapter** with this exact structure:
   - Grey callout 🤖: "Claude's condensed theory, organised by this chapter. Written from the field, not copied from the book: check the book before quoting a definition word for word."
   - `## In 30 seconds`: 3 bullets, the chapter's point.
   - `## The theory, condensed`: the core models and arguments, bold lead-ins, short bullets. Roughly 300–600 words.
   - `## Key terms`: a 2-column table (Term | Meaning), 6–10 rows.
   - `## Studies worth knowing`: 3–5 bullets, "**Author (year)**: what they did → what they found", with an italic caveat where replication is weak.
   - `## At work`: 4–6 bullets that translate the theory into leading teams, digital delivery, coaching or her own energy. Concrete, not generic.
   - Yellow callout ✍️ "**For you: two questions, two minutes**" with exactly two sharp, personal questions and a `→ ` line. Never answer them.
   - `## Your highlights`: "*Empty. Filled from your Highlights exports as you read.*"
   - Properties: `Status` = Claude draft (Reading for the chapter she's on), `Book`, `No.`, `Theme`.
4. **Write 4–7 Concepts per chapter**, only ideas worth reusing. Body:
   - **What it is.** 2–4 sentences.
   - **Evidence.** The honest state of the evidence, including failed replications and the size of the effect.
   - **At work.** 1–3 sentences.
   - **Connects to:** names of related concepts.
   - Yellow callout ✍️ "**Your take:** one pointed question → ". Leave it blank.
   - Properties: `Origin` = Claude synthesis, `Sources`, `Chapter` (one or more), `Evidence`, `Kind`, `Theme`.
   Before creating, search Concepts for an existing note on the same idea. If one exists, add this source and chapter to it and extend the Evidence paragraph instead of duplicating.
5. **Update the book page** (the Source row's page): a blue 🧭 "How to use this" callout, `## The book in one paragraph`, `## Ten ideas to keep` (mentions of the most useful concepts, each with a few words on why), `## A note on evidence`, then linked views of Chapters (filter Book, sort No.) and Concepts from this book (filter Sources, group by Evidence).

## B. Filing a Highlights export
Input shapes:
- **Markdown**: `# Title`, `## Author`, `#### [Page N](highlights://…)`, `>` quotes. Lines without `>` are Diana's own notes.
- **TextBundle** on Dropbox: a single zip file. Use Dropbox `fetch` on the path to read `text.markdown`. Images (`![](assets/…)`) can't be extracted: get a fresh Dropbox `download_link` and attach the whole package to the chapter page with Notion `create-attachment` (filename `<Book> p<N>.zip`), and note the internal image path. Never describe or guess image content.

Steps:
1. **Repair** print hyphenation ("behav-" + "iours") and obviously fragmented selections within one page heading, preserving every word. Never merge across page headings. If something is ambiguous, flag it rather than guessing.
2. **Map each page to its chapter** using the book's chapter page ranges (ask once if unknown, then note the ranges on the book page).
3. **Skip duplicates**: exports are cumulative, so skip any quote already present on the chapter page.
4. **Append** under `## Your highlights` on that chapter page: each quote as a `>` block, verbatim, ending "(p. N)". Diana's own notes go in as "**Your note (p. N):** …". If her note is a question, add a short blue 💬 "Claude's answer to your note" callout below it.
5. If a highlight is a definition or finding not yet in Concepts, create or update the concept (Origin = From my reading if it comes from her highlight), and quote the highlight in the concept body.
6. Set that chapter's `Status` to Reading.

## C. Articles, posts and notes
Create or update the Reading Sources row (Type = Article or Report), then write 1–3 Concepts directly (no chapter pages), Origin = From my reading. Keep her original text accessible: quote the key line, and link the source.

## Rules
- **Claude writes the theory; Diana writes only reflections.** Never fill the yellow callouts, `Checked by me` or any reflection field.
- **Be honest about evidence.** Use the Evidence label and say plainly when a famous study failed to replicate or is debated. Mark popular books and frameworks as lenses, not findings.
- **Label Claude's writing.** Chapter pages carry the grey 🤖 callout; concepts carry Origin = Claude synthesis unless they came from her reading.
- **No invented specifics.** No made-up page numbers, quotes, statistics, DOIs or bibliographic details. Page numbers only from her exports.
- **Themes**: use existing Theme options. Propose new ones in the report back, and don't add them silently.
- **Plain, short English.** British spelling (behaviour, organisation). Bold lead-ins, short bullets.
- **Scale**: for a whole book, create pages in batches (about 4 chapters or 20 concepts per call) and fetch one page afterwards to check the formatting renders.

## Report back
Tell her briefly: chapters written, concepts created or updated, highlights filed (and skipped as duplicates), anything flagged as ambiguous, any Theme suggestions, and the book page link.
