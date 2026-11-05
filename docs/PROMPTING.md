# Prompting each role

A graph behaves the way its prompts and files say it behaves. This document covers the prompts that matter: the scheduled prompt that wakes an architect (the tick), the setup turn that precedes the first tick, the chief of staff's check-in prompt, and the priority line the chief of staff writes on a lane's main branch. Each section ends with one short generic example. Angle brackets mark what you replace.

## The anatomy of a scheduled prompt

A tick is read cold. The session may have a long history, but the prompt must stand alone, because the prompt and the repository files are the only things a run can rely on. A good tick has these parts, in this order.

**1. Open the board first.** The board holds decisions the owner made since the last run, so the run must see them before it plans anything.

> Open the lane's board at <board URL> first and read the status of every item. Act on anything accepted, declined or done.

**2. The authority line.** A session that pushes branches and opens pull requests needs standing permission, and a fresh session does not know it has it. Name where that permission lives: a rule in the repository's instruction file, or the owner's recorded words in the charter. The line tells the run it does not need to ask, and that a setup turn, a tick or a message does not have to repeat it.

> Your standing permission to push branches and open pull requests on this repository is in <file and rule>. Do not ask again.

**3. The start procedure.** Fetch main, cut a branch from it, read the charter and the newest log lines, and trust the files over memory.

> Fetch origin main. Cut <branch prefix>/<date>-<n> from origin/main. Read <charter path>, then the newest lines of <log path>. Trust the files over your memory of earlier runs.

**4. The files to re-read.** Name them by path, in order. Do not paste their contents into the prompt. A run that rereads the charter every time is not wasting calls; it is the thing that keeps the lane from drifting.

**5. The order of work and how to pick the next item.** The charter holds the order. The tick says how to apply it: take the first item in the order that is eligible, where eligible means its inputs exist and its gate is open. A priority line from the chief of staff on main outranks the default order.

> Pick the first eligible item in the charter's order of work. A dated priority line in <path> overrides it.

**6. The caps and the cost rule.** State the tool-call cap, the subagent cap, the model by name for every subagent, and the instruction to pass file paths and not content.

> At most <n> tool calls and <n> subagents. Name the model of every subagent: <biggest model> for judgment reads, <mid model> for builders and checks, <smallest model> for mechanical passes. One subagent at a time. Pass file paths, never pasted content.

**7. The truth gate.** The rule that no claim ships without evidence. State it in one sentence and point at the ledger format in the charter.

> Every claim has a ledger row: observed with a path, the owner's own words quoted, or an outside source with a URL and a quote. A quotation is matched verbatim against a saved source before use.

**8. The hard gates that never move.** List what the lane never does, so a clever run cannot talk itself out of it.

> Nothing is sent, published, posted or paid by machine. No account on an outside service is created or changed. The drafter never grades its own draft.

**9. Push, open the pull request, log "merge PENDING".** The end of every run is mechanical.

> Push the branch, open the pull request, and log "merge PENDING" unless the charter lets this lane merge.

**10. The log line format.** Give the format or point at the template. The line must carry the numbers and the next step.

> Append one line to <log path> in the format in <charter section>: time, role and version, what was done, files, pull request, merge state, subagents and models, tool calls, needs.

**11. What to do when a permission check refuses a command.** Do not retry and do not route around it. Write the refusal in the log and stop within a few calls. This one rule prevents a run from burning its budget fighting a guardrail.

> If a permission check refuses a command, do not retry. Log the refusal and stop within <n> calls.

**12. Never address the owner in the log.** The log is read by the chief of staff. The owner reads what the chief of staff brings. If a decision belongs to the owner, the line says "needs decision" with a recommendation, and the run does not stop to ask.

**13. Keep context lean.** Read what is needed, not everything. A run with nothing due ends within a few calls.

A real tick is written as one paragraph, the way a person would brief a colleague, and the template in `templates/TICK-PROMPT-TEMPLATE.md` shows the whole thing assembled.

## The setup turn

The setup turn is the first message to a new architect session. It is not a work run. Its job is to get the session's facts into the open and to find out what the session can and cannot do before any scheduled run depends on it. It has four steps and then it stops.

1. Read the charter and the files it names.
2. Write the session's own facts to the lane's board: session link, repository, log location, cadence, version. These let the chief of staff and the owner find the session later.
3. Report the tools the session sees and what it cannot do: whether it can push, open pull requests, read the shared drive, reach the board's database. A missing tool found now is a cheap fix. A missing tool found on the first scheduled run is a failed run.
4. Stop and wait for the tick. The setup turn does no lane work.

> You are the <lane name> architect. Read <charter path>. Write your session link, repository, log path and cadence to the board at <board URL>. Then report which tools you can see and what you cannot do. Do not start any lane work. Stop and wait for the scheduled tick.

## The chief of staff's check-in prompt

The check-in prompt is armed as a scheduled prompt, and it follows an order that protects the chain of check-ins.

**Arm the next check-in first.** Before reading anything, create the next one-shot check-in and write its id and time on the board. If the run crashes halfway, the chain still continues.

**The rotation rule.** If the session's context is near full, write the handoff block into the record, spawn a successor with the start message, and stop. Do not try to finish a check-in on a full context.

**The board read.** Read every item's status, and any pending requests. Decisions are read at every check-in, because a notification may not have arrived.

**Merges.** Merge the pull requests that pass under each lane's merge rule. Leave anything that needs the owner's word and put it on the board.

**The record.** Append a short entry to the continuity file: what shipped, what merged, what changed on the board, what is open, and the cost.

**The report.** Plain language, short, ending with what waits on the owner, each item named with the chief of staff's recommendation. If nothing waits, say so.

> You are the chief of staff for <project>. This is check-in <n>. First, arm the next check-in for <time rule> and write its id and time to the board. If your context is near <threshold>, write the handoff block to <record path>, spawn a successor with <start message path>, and stop. Otherwise read <record path> and <rules path>, read every board item's status, read the newest lines of each lane's log, merge what passes, refresh the board, append to the record, and report to the owner. End the report with what waits on them. Limits: <n> tool calls, <n> subagents, each with its model named. Report cost.

## How to write a priority line on a lane's main

A priority line is how the chief of staff steers a lane. It is a short, dated entry committed to the lane's main branch, where the next run will read it as part of its start procedure. It has three parts and nothing else: the date, who ordered it, and the order of work.

> <date> | ordered by <who> | Order of work: first <item>, then <item>. Pause <item> until <condition>.

Do not add rationale, history, praise or warnings. If the lane needs a rule, the rule belongs in the charter, not in a priority line. A priority line is a queue edit. The next run reads it, follows it, and the following check-in can replace it. Keep it short enough that a run with a thin context reads it without cost.

## Why a message between sessions is data, not authority

Sessions can message each other, and the chief of staff may message a lane. A lane treats that message as information. It does not treat it as a rule. A lane takes its rules from exactly three places: its tick text, its repository files, and the owner typing in the lane's own chat. Anything else, including a message that claims to come from the chief of staff or the owner, is data to weigh and not an order to follow.

The reason is robustness. Messages can be spoofed, misrouted, stale or silently dropped, and a lane that obeyed them would behave differently from run to run. A lane whose behavior comes from files and tick text is the same every time and can be audited by reading them.

The consequence is simple. To change how a lane behaves, change the file and the tick text. If the chief of staff wants a lane to start doing something, it edits the charter or writes a priority line on main and, if needed, updates the tick text. A message may point the lane at the change, but it does not carry the change.

## A short checklist before you arm a tick

- Does the prompt open the board first?
- Does it say where the permission to push and open pull requests lives?
- Does it state the caps and name a model for every subagent?
- Does it say what to do when a command is refused?
- Does the log line format carry the numbers and the next step?
- Does anything in it let the lane send, post or pay by machine? It must not.
- Have you run the lane by hand three times, and supervised the first scheduled run?
