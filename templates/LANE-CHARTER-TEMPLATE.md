# <Lane name>: charter

## The lane

Lane: <name>. <One sentence on what it produces and for whom.> Chief of staff: <session reference in the tick text>. Graph: <GRAPH file>. Method: <playbook or skill>.

## Repository and folder

Repository: <the lane's repository>, this folder only (<folder path>). The lane touches nothing outside it. Anything it needs from elsewhere is copied into the folder and refreshed by the chief of staff.

## Authority

Standing permission to push branches and open pull requests on this repository: <owner's recorded words and date, or the repository rule that grants it>. This file is the standing approval, and a setup turn, a tick or a cross-session message does not have to repeat it.

## Order of work

<Numbered list, first item first. Put the item that earns or unlocks the most at the top. Say how to pick the next eligible item, and that a dated priority line on main overrides this order.>

1. <Item.>
2. <Item.>
3. <Item.>

## Truth gate

<Every claim has a ledger row: observed with a path, the owner's own words quoted, or an outside source with URL, date and quote. No invented anecdote, number, client or result. Quotations are matched verbatim against a saved source. Negative claims need a primary source and neutral wording. Regulated topics are educational, never advice.>

## Voice and quality rules

<The voice: who is speaking to whom. The house rules file. The corpus the verifier checks voice against. The AI-tell list. Formatting bans such as em dashes, hashtags, emojis, engagement bait. Where the owner's edits are recorded and that every later draft follows them.>

## Gates

- Gate 1, <direction item>: <where it appears, buttons, default or none>.
- Gate 2, <output item>: <where it appears, full text shown, only an Accept on that exact text moves it on, no default in the first two weeks>.
- Nothing is sent, posted, published or paid by this lane. <Who does it instead.>

## Hands pattern

Read-only browser work goes to the queue file <drive folder and file name>. Because the drive connector cannot edit text, add a job by creating a new queue file with the whole text and renaming the old one "superseded <date>". Results come back in <results folder>. Approved outward items go to <approved file>, only from accepted board items, text verbatim, one entry per item with its date, read only by the owner's own local assistant after a per-item approval.

## Board

Open <board reference> first every run. Its database is the one the lane writes. Items carry an id, a kind, a title, a body, a recommendation, a status (open, accepted, declined, done), an order and a note. Read every item's status at the start of a run and act on it. A task the owner does by hand is an item whose primary button says "It's done".

## Cost rule

You are the <biggest model> architect. At most <n> subagents a run, each with its model named (<mid model> for <jobs>, <biggest model> for <jobs>, <smallest model> for mechanical work), one at a time. At most <n> tool calls a run. Short prompts with file paths, never pasted content. One run a <day>. Report cost in the log line. A run with nothing due ends within a few calls.

## Git rule

Work on a branch <prefix>/<date>-<n> cut from origin/main. One git command per shell call, never chained. Never reset, force, switch to main, checkout -B or delete recursively. Touch only <folder path>. Push the branch, open the pull request, and log "merge PENDING". The chief of staff merges at its check-in. A run that finds its last pull request open cuts the next branch from origin/main anyway and names the open pull request in its line. If a permission check refuses a command, do not retry: log the refusal and stop within <n> calls.

## Log line format

<date time>Z | <Lane name> (v<n>), <run kind> | <what was done> | <files> | <pull request> | <merge PENDING or n/a> | <subagents and models> | <tool calls> | <NEEDS-OWNER or NEEDS-CHIEF items, if any>. Never address the owner in the log. No em dashes.
