# How graphs run

A graph spec says which roles a workflow needs. This document says how those roles actually run, from one person pasting text between chat windows to a fleet of scheduled sessions reporting to one board. It follows the deployment ladder in SKILL.md: L1, L2 and L3. Every graph starts at L1 and moves up only on a clean record.

## L1: separate chats, the owner ferries state

At L1 each role is its own chat or session. The researcher is one window, the builder another, the verifier a third. Nothing is shared except what the owner copies from one window to the next.

This sounds primitive, and it is the right place to start for three reasons. The owner sees every handoff, so a bad assumption shows up at once. The files that will later carry state (plan, research, draft, review, final, lessons) get invented by hand, so you learn which ones the graph really needs. And the cost of a mistake is one wasted chat, not a week of scheduled runs.

Run every new graph by hand three times. Compare the output against the way the work was done before. If the graph does not beat the old way by the third run, fix the graph, not the prompts. Promotion to L2 needs three clean runs, and "clean" means the verifier passed the work without the owner rewriting it from scratch.

## L2: agent sessions sharing a repository

At L2 the roles are agent sessions (Claude Code or a similar tool) that share a repository. Git is the shared state. Nodes hand off through files in a run folder, and the owner stops ferrying text.

### One session per role or per lane

A session is long-lived. It keeps a conversation open, so a person can open it and talk to it, and it holds its rules in files it re-reads. There is one chief of staff session for the whole operation, and one architect session per lane. A lane is one recurring workflow: a content stream, a research thread, a product build. The architect owns the lane's folder in the repository and the lane's second brain, which is the set of files described below.

Workers (researchers, drafters, verifiers) are usually subagents the architect launches for a single job and then discards, not standing sessions. The architect is the only session that persists.

### The tick

A tick is a scheduled prompt that wakes the architect's session on a cron. The scheduler fires the prompt into the session at the lane's cadence, for example once a weekday at a quiet hour. The prompt carries the lane's operating rules for that run, so the behavior is set by the prompt text and the repository files, not by what the session remembers.

A run does one deliverable, opens a pull request, writes one line in the lane's log file, and stops. One deliverable per run keeps the pull request small enough to review, easy to roll back, and cheap. A run that finds nothing due ends within a few calls.

### The start procedure of a run

Every run begins the same way, and the order matters.

1. Open the owner's board first and read the status of every item, because a decision made since the last run changes what the run should do.
2. Fetch the main branch from the remote.
3. Cut a new branch from the remote main, never from the previous run's branch. Name it with the lane prefix, the date and a counter.
4. Read the lane's charter and the newest lines of the lane's log.
5. Trust the files over memory. The session may remember an earlier run, but the charter and the log are the truth. If they disagree with the session's memory, the files win.

### The files as state

Each run writes named files in the lane's folder. They are the paper trail and the lane's memory.

- **Plan**: what this run will do and why, picked from the queue by the order of work.
- **Research**: what the researchers gathered, one file per lane, each claim with its source.
- **Draft**: the builder's output, with a ledger that gives every claim its evidence.
- **Review**: the verifier's verdict, written into the draft's file or beside it.
- **Final**: the version that passed, and the version the owner approved.
- **Lessons**: what the improver mined from the run, including every edit the owner made and the rule it implies.

Alongside these sit the charter (the lane's standing rules) and the log (one line per run). The improver commits the durable parts to the lane's files so the next run starts smarter. Nothing about the lane lives only in a chat.

### The log line is the channel up

The architect never pings anyone and nobody reads its chat. The log file is the only channel upward. Each run appends one dated line that carries what was done, which files, the pull request, whether the merge is pending, what the run cost, and anything that needs the owner or the chief of staff. The format is in `templates/LOG-LINE-TEMPLATE.md`. Because the chief of staff reads the logs, the log line has to carry the numbers and the next step, not a story.

### The chief of staff and the check-ins

The chief of staff is the only role that talks to the owner. It runs scheduled check-ins, typically twice a day. At each check-in it does the same things in the same order:

1. Arms the next check-in first, so a crashed run does not break the chain.
2. Reads the owner's board for decisions made and requests pending.
3. Reads the newest lines of every lane's log, and only what changed.
4. Merges the pull requests that pass under the lane's merge rule, and leaves the rest for the owner.
5. Writes priority lines on each lane's main branch, which are the only way it steers a lane (see `docs/PROMPTING.md`).
6. Refreshes the owner's board with what now waits on the owner, each item with a recommendation.
7. Writes a short entry in its own record, including the cost of the check-in.
8. Reports to the owner in plain language, ending with what waits on the owner.

The chief of staff does not read the architects' chats unless a log line points at a problem. The logs are enough.

### Pull requests, merges and the merge rule

An architect works on a branch, pushes it, opens a pull request and logs "merge PENDING". It does not merge unless the lane's charter explicitly allows it. The chief of staff merges what passes at its next check-in. For a lane with a low blast radius the charter may let the architect merge its own pull request when the checks pass. For anything outward the architect never merges. Whichever rule applies, it is written in the charter and repeated in the tick text.

If a lane finds its last pull request still open, it cuts the next branch from main anyway and names the open pull request in its log line. It does not wait.

### The owner's board

The owner's board is one page that shows every lane and everything that waits on the owner. The chief of staff writes it; the owner reads it and decides with buttons. Each item carries the chief of staff's recommendation and three buttons:

- **Accept recommendation**: the owner agrees, and the chief of staff acts.
- **Something else**: the owner writes what should happen instead, in the owner's own words. Those words become a lesson.
- **Decline**: the item closes.

Some items are tasks the owner carries out by hand, such as pasting a prompt into a local tool, or clicking something the automation may not click. For these the primary button reads **It's done** and records the status `done`, not `accepted`. The chief of staff needs to know the hand task happened, which is different from knowing the owner agreed with it.

Each lane may have its own board with the same buttons: items, links and files for that lane. The lane's tick tells the architect to open the board first and, at the end of the run, add anything the owner needs to it.

Decisions are recorded in a database behind the board, and a notification to the chief of staff may or may not arrive. The chief of staff therefore reads every item's status at every check-in. A notification is a convenience. The record is the truth.

Gates default by blast radius. A low-blast-radius gate can default to Accept after 24 or 48 hours of silence, which keeps the owner's involvement close to zero. A gate on anything outward has no default.

### The hands pattern

Some work needs a real browser: a site that blocks automated fetches, a page that renders only in the owner's signed-in session, a download behind a click. A cloud session cannot do it. The hands pattern gives the lane a browser without putting a person in the loop on every job.

It has two queues, and the separation is the point.

**The read-only job queue.** In a shared drive, each lane has an inbox folder holding one queue file. The architect writes jobs into it: open these public pages, download these public files, read and summarize. Each job has a slug, a status of ready, a results folder name and exact steps. A local assistant on the owner's machine runs on a schedule, a few times a day. It opens an index file that lists every lane's queue, runs every ready job, saves results in the job's folder inside that lane's inbox, and marks the job done or blocked with a reason. A later architect run reads the results from the drive and writes what it learned into its repository under its usual truth gate. The rule that keeps this safe is that only read-only work enters the queue. The task prompt says so, every queue file says so at the top, and a job that asks for more is marked blocked and skipped.

**The approved-queue.** Anything that posts, sends, signs in, buys or submits is different. The architect never puts it in the read-only queue. It goes on the lane's board as an item for the owner to decide. Only after the owner accepts that exact text does the architect copy it, verbatim, into a separate approved file, one entry per item with its date. That file is read only by the owner's own local assistant, on the owner's machine and account, under the owner's standing instruction, and only after a per-item approval. That is what makes the send the owner's send and not the lane's. The lane never touches the outside service itself.

The tick carries one paragraph describing both queues. If the drive tools are missing from a session, the architect writes the job in the same form as a line in its log, and the chief of staff copies it into the queue.

### Rotation of the chief of staff

The chief of staff session reads a lot, so its context fills. When it nears the limit, it rotates instead of degrading. It writes a handoff block into its record: the standing rules, the state of every lane, the open decisions, the armed check-in and anything half done. Then it spawns a successor session and gives it the start message, which points at the record and the standing rules file and says to trust them over any memory. The successor opens the board on its first turn, re-arms the check-in chain, and carries on. The record is what survives, so the record must be complete enough that the successor needs nothing from the old session.

### Cost control

Cost is a design property of the graph, not an afterthought. Every tool call re-reads the whole context, so a large context times many calls is the bill. The controls are:

- Name the model of every worker explicitly. The biggest model goes to architects and judgment reads, a mid model to builders and ordinary verification, the smallest to mechanical passes. Never rely on inheritance, because inheritance is the expensive default.
- Run one worker at a time. At most two in a block. No parallel checker rounds across assets.
- State a tool-call cap in every prompt, and a cap for every subagent.
- Give workers file paths, not pasted content. Keep prompts short.
- Report the cost in every log line and every report: subagents launched, their models, tool calls used.

A run with nothing to do should end in a few calls. If a lane has nothing to do, it refills its own queue and reports, and the chief of staff lowers its cadence.

## L3: orchestrated

L3 adds scheduled runs wired together with glue code for outside APIs. It is only for graphs with a boring L2 record, meaning many runs in which nothing surprising happened. Two rules do not bend.

First, never attach a send-capable or money-moving connector to an unattended node. An unattended node can draft, queue and propose. A person, or the person's own local assistant acting on a per-item approval, sends and pays. If a connector can send mail, post publicly or move money, it does not belong in a session that runs on a cron.

Second, supervise the first scheduled run. Watch it start, read every file it writes, and confirm the log line is accurate before you let the schedule run alone. Most failures of a new schedule show up in the first run, and a supervised failure costs minutes.

## What to take from this

Keep the shape small. One architect per lane, one deliverable per run, one line per log, two owner gates, and a board that turns decisions into buttons. The rest of this repository shows how to prompt each role (`docs/PROMPTING.md`) and what went wrong along the way (`docs/TIPS.md`).
