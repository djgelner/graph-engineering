# Tips, tricks and lessons

Each item below came from running graphs for real. Several of them were learned by paying for the mistake.

## A lane sees only the branch it was cloned from

A lane's session works on a clone of one branch. It cannot see files on another branch or in another repository. If a lane needs a rule, a catalog, a style guide or a list of prices from somewhere else, copy that file into the lane's own folder and say where the original lives. Refresh the copy when the original changes. A lane that reaches for something it cannot see will either fail or guess, and guessing breaks the truth gate.

## A shared-drive connector that cannot edit text

Some drive connectors can create and rename files but cannot edit the text of an existing one. For a queue file, recreate it: write a new file with the whole text, and rename the old one "superseded" with the date. Never reference a file by its id, because the id changes each time you recreate it. Reference it only by name, and keep the name exact, so the local assistant always finds the current one.

## One git command per shell call

In a lane, run one git command per shell call and never chain them. Never reset, never force, never delete recursively. A chained command can hide which step a permission check refused, and a destructive command in an unattended session has no one watching. Single commands also make the log readable when something fails.

## Merging two branches that both append to a log

When two branches both append to the same log file, a normal merge conflicts at the end of the file. Merge with a union strategy on that file, in a scratch worktree so main stays clean, and then sort the trailing dated lines into time order. The log is append-only and each line stands alone, so a union is safe, and the sort restores the order a reader expects.

## A permission classifier can refuse an action that looks like interference

A permission classifier may refuse an action that looks like it interferes with a running workload: archiving a session, editing a permissions file. Do not look for a workaround. The chief of staff logs the refusal and puts the click on the owner's board, so the owner does it by hand. The refusal is the guardrail working. A workaround would turn it into a hole.

## Model by job

Use the biggest model for architects and for judgment reads, such as the verifier on an outward surface. Use a mid model for builders and for ordinary verification. Use the smallest for mechanical passes: renders, hash checks, file moves. Match the model to the job and not to the importance of the project. Most of the work in a graph is not judgment.

## Name the model on every worker

Name the model on every worker you launch. If you do not, the worker inherits the parent's model, and inheritance is the expensive default. In one half-day, a parent on the biggest model launched many workers with no model named, every one of them inherited the biggest model, and the bill was far larger than the work justified. A model name in every prompt is cheap insurance.

## No fan-out

Run one worker at a time, and at most two in a block. Never run parallel checker rounds across assets. Every tool call re-reads the whole context, so a checker on a 300K context making 80 calls reads 24 million tokens. Parallel checkers multiply that. One round with a stated call cap beats four rounds without one.

## Default to Accept on low-blast-radius gates, and keep outward gates strict

A 24-hour or 48-hour default to Accept on a gate keeps the owner's involvement near zero. Use it where a wrong call is cheap to undo: an internal plan, a research summary, a direction. The gate on anything outward, such as a post, an email or a deliverable to a client, stays strict, with no default, for the first two weeks. After two clean weeks, the owner can decide whether to promote it.

## The primary button on a prompt item says "It's done"

When an item is a task the owner does by hand, such as pasting a prompt into a local tool, the primary button should read "It's done" and record the status done, not accepted. The chief of staff needs to know the hand task happened. Accepted means "I agree." Done means "I did it." Mixing them leaves the chief of staff guessing.

## The drafter never grades its own draft

The model that wrote a draft is the worst judge of it. It reads its own reasoning into the text and passes it. Give the verifier its own lane, the same access as the builder, and a different prompt. For outward copy, the verifier checks truth and voice against the owner's own corpus and an AI-tell list. If the verifier fails the draft, loop once to the drafter, and then escalate.

## Verify live after a merge

After a merge that changes a live page, do one fetch of the page and record what it showed. A merge is not a deploy, and a deploy is not a working page. One fetch costs a call and catches the cases where the page is stale, broken or showing last week's content. Put what the page showed in the log line.

## The log line is the channel, so make it carry the numbers and the next step

The chief of staff reads the log line and nothing else. A line that says "done" tells it nothing. A line with the files changed, the pull request, the merge state, the counts, the cost and what comes next lets the chief of staff decide without opening the session. Write the line for a reader who has thirty seconds and no context.

## Do not trust a notification

Cross-session messages may fail silently or be refused. A button click may record a decision and not wake anyone. So the board's decisions are read at every check-in, whether or not a notification arrived. Treat a notification as a hint and the database as the record.

## A scheduled session with nothing to do refills its own queue

A scheduled session that finds nothing to do should not idle. It refills its own queue, by starting the next discovery cycle the charter names, and reports what is waiting for review. A lane that idles costs a run and produces nothing. A lane that refills gives the next run something to do.

## Cut every run's branch from main

Cut every run's branch from main, even when the last pull request is still open, and name the open pull request in the log line. A run that stacks on an unmerged branch inherits that branch's problems and makes the chain of merges fragile. A branch from main is independent and can be merged or dropped on its own.

## Every claim has a ledger row

The truth gate means every claim has a row in a ledger. A row is one of three kinds: observed, with a path to the artifact; the owner's own words, quoted; or an outside source, with a URL and a quote. A claim with no row does not ship. A negative claim about a person or company needs a primary source and neutral wording.

## Match every quotation against a saved source

Models invent quotations from famous texts. They produce fluent lines that sound right and appear nowhere in the book. Save the source text first, then match every quotation verbatim against the saved copy, with its chapter or page, before the quotation is used. A line that cannot be found is not used, however good it sounds.

## Report cost in every log line and every report

Put the cost in every log line and every report: subagents launched, their models, tool calls used. Cost that is written down gets managed. Cost that is not written down arrives as a surprise at the end of the week. It also tells the chief of staff which lanes to slow down.

## Start every new graph by hand three times

Run a new graph by hand three times before you automate it. If the manual runs do not beat the old way, automating them produces mediocre work faster. The manual runs also tell you which files and gates the graph really needs, and which roles can be deleted. Fix the graph first, and promote it when three runs come out clean.

## The context diet

The problem. A scheduled check-in prompt grows by accretion. Every id, lane order and rule gets pasted into it so the prompt can stand alone, and the handoff note grows the same way, with each successor adding a paragraph of history. Soon the prompt is thousands of words, rewritten in full at every check-in, and the handoff note is tens of thousands of tokens that every takeover reads. Output tokens are the expensive ones, and about nine tenths of each rewrite is identical to the last.

The pattern. Split the one big blob into four files. The check-in prompt becomes a short fixed procedure, a few hundred words, written once and copied unchanged. It points at one small state file, under about 1,500 words, that holds everything current and is rewritten in place as a diff. Standing rules go in a separate rules file, each with its date and the owner's own words, read once and searched after. Old history goes in an append-only history file that is never read at a takeover. The handoff note shrinks to a pointer plus numbered takeover steps. Record entries get a cap of about 150 words, carry only the facts an audit needs, and are batched: lane events between check-ins share one entry at the next check-in, and only a rule or gate change gets its own commit.

What it saves. In one measured case, a third of the chief of staff's own daily spend and most of a takeover's cost. The prompt write drops from thousands of output tokens to a few hundred, a takeover reads a few thousand tokens instead of tens of thousands, and event records stop costing a commit and a push each.

Risk one: a compaction in the middle of a check-in, with a prompt that no longer carries the facts. Mitigation: the procedure's first step is "read the state file", the board carries the same ids, and a successor is told the same three files.

Risk two: a rule lost in the move. Mitigation: do the move by diff, with every rule accounted for in the record, and keep the old block verbatim in the history file.
