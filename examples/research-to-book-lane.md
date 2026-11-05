# Example cartridge: a research-to-book lane

A worked cartridge for a temporary, low-priority lane that researches a classic text, maps its lessons onto modern life, and plans and drafts a series of short books. It is rewritten from a real lane's spec with every name removed.

## Final output

An application map, lesson by lesson, from what the classic text tells its original reader to what a modern reader in that seat should do, and a series of short books that each take one lesson and apply it to modern life. The books are written from a context bank of the text, the scholarship, the talks and the essays, with every quotation checked against a public-domain translation, and with the owner's gate on the map, on the series plan and on each book's outline.

## The goal

The owner clarified the goal after the first draft of the spec: the point is how to apply the lessons to modern life, not a description of the text. The text is advice to one busy, successful man who complains that the years go fast. His modern counterpart is the overworked professional, founder or firm owner. The lane's work is the map between the two, and books that walk one lesson at a time across it.

## Cadence and trigger

Scheduled, one run a day at a quiet hour, with the smallest cap in the fleet. The chief of staff pauses the tick first whenever the weekly usage allowance is tight. A run that would exceed its cap stops and logs where it got to. The lane ends when the series plan is approved and the first book is drafted, or when the owner says stop.

## The three phases

Each phase is a gate for the owner before the next.

**Phase 1, the context graph (weeks 1 to 2).** One researcher lane per run, in this order: the text (a public-domain translation saved whole, chapter by chapter, with a copy of the original language for checking); the scholarship (each claim with URL and quote); video (the most-watched talks and readings, by saved transcript, with channel, date and view count as shown); modern applications (essays and threads, quoted with URL); the market (the books already sold on the text, what their reviews praise and miss, with no number invented). Each lane writes one context file. The fifth run puts a one-page summary on the board, with a 48-hour default to Accept.

**Phase 2, the application map (week 3).** The lane writes a file of nuggets, the author's words quoted from the saved translation with chapter number. Then the map: one node per lesson the text gives (not one per category of waste), and each node has five fields. The situation the text names, in its words. Its modern form, named concretely. The practice or decision that applies it now, specific enough to do this week. What it costs the reader. The objection a modern reader raises, answered from the text or conceded. Then a thesis file with the one argument the series makes, and a plain diagram of the map. Gate: map and diagram on the board, 48-hour default to Accept.

**Phase 3, the series.** A series file with five to eight short books, one lesson applied each, with a title, a one-paragraph promise, a chapter outline, the reader and the format, plus the first book's outline in full. Gate: the series file on the board with no default, the owner's accept required. Then one book at a time, one chapter a run, each chapter verified before the next.

## Nodes

| Node | Who | Reads | Writes |
|---|---|---|---|
| Architect | the lane session, biggest model | charter, log, context, map, series, board | the run note, the board, the log line |
| Researchers (phase 1) | mid-model subagent, one a run, call cap stated | the context map | one context file per lane |
| Mapper (phase 2) | the lane itself | context files, the saved text | nuggets, the map, the thesis, the diagram |
| Planner (phase 3) | the lane itself | the commonplace files | the series file |
| Drafter (phase 3) | mid-model subagent, call cap stated | the series file, nuggets, the chapter brief | one chapter file |
| Verifier | mid-model subagent for the mechanical check; one biggest-model read for a finished book | the chapter, the saved text | the verdict in the chapter file |
| Owner gates | the board | the phase summaries, the series plan, each outline | accept, something else, decline |

There is no merger; the architect folds it in.

## Edges

Researchers feed the mapper, then the planner, then the drafter, which loops with the verifier chapter by chapter. Video transcripts the session cannot reach go to the read-only job queue for the owner's local assistant. Nothing is posted, sent or bought.

## Owner gates

Phases 1 and 2 default to Accept after 48 hours. The series plan has no default, and each book's outline is a gate. The byline or a pen name is the owner's call at the series gate.

## State files

A context folder, a commonplace folder (nuggets, map, thesis), a series folder, a books folder with one file per chapter, the saved translation and the log.

## Failure modes the verifier hunts

A quotation not in the saved translation (models invent lines from famous texts, so every quote is matched verbatim and carries its chapter). A modern statistic with no URL and quote. A video claim with no transcript on disk. An anecdote about a named living person. A structure borrowed from an existing book. Em dashes. A book that restates the text instead of applying it. A vague map node: a practice the reader cannot do this week is not a practice.

## Deployment level

L2, a scheduled session with repository state. No promotion is planned, because the lane is temporary.
