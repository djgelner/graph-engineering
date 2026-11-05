# Log line template

The log file is the only channel from a lane up to the chief of staff. Each run appends exactly one line. The chief of staff reads it with thirty seconds and no context, so the line carries the numbers and the next step. Never address the owner in the log. No em dashes.

## Format

```
<date time>Z | <Lane name> (v<n>), <run kind> | <what was done> | <files> | <pull request> | <merge PENDING or n/a> | <subagents and models> | <tool calls> | <NEEDS-OWNER or NEEDS-CHIEF items, if any>
```

Fields, in order:

1. The time of the run in UTC.
2. The lane, its version and the kind of run (for example weekly plan, daily run, improver run).
3. What was done, with counts: items drafted, verified, accepted, queued, merged.
4. The files written or changed.
5. The pull request number, or n/a.
6. The merge state: "merge PENDING" or n/a.
7. Subagents launched and the model of each, or "none".
8. Tool calls used.
9. Anything that needs the owner or the chief of staff, each with a recommendation. Leave empty if nothing.

## Filled example

The values below are invented to show the shape. They are not real results.

```
2026-03-14 09:05Z | Content Architect (v4), weekly plan | 5 posts drafted and verified (4 pass, 1 revised once), 5 posted to the board for gate 2, 2 earlier posts accepted and copied to the approved file, 1 declined with reason logged | posts/p-0141.md to p-0145.md, runs/2026-W11/plan.md, lessons/VOICE-LESSONS.md | PR 212 | merge PENDING | 3 subagents: 1 mid model (researcher, 22 calls), 1 mid model (drafter, 26 calls), 1 biggest model (verifier, 14 calls) | 41 | NEEDS-CHIEF: merge PR 212; the queue file needs a new analytics job, written and ready. NEEDS-OWNER: none.
```

## What a good line does

- It states counts, not adjectives.
- It names the open pull request so the chief of staff can merge it without searching.
- It carries the cost, so the chief of staff can slow a lane that is expensive.
- It says what the lane is waiting on, so nobody has to open the session to find out.
- When a command was refused, it says which one and that the run stopped, with "PENDING, refused by permission check" in the needs field.
