# GRAPH-<letter>: <name>

Status: <draft | live from <date> | paused>. Engine: the Basic Shape. Cartridge: this file plus the lane charter.

## Final output

<One sentence. What exists at the end of a run, for whom, in whose voice, approved by whom. No graph until this sentence exists.>

## Cadence and trigger

<On demand, scheduled (give the cron in words), or event. Say which day and hour, and why that hour.>

## Nodes

| Node | Who runs it | Reads | Writes | Tools and connectors (least set) |
|---|---|---|---|---|
| Chief of staff | <session> | <logs, board> | <priority lines, board, record> | <repo, board database> |
| Architect | <lane session, biggest model> | <charter, log, board> | <plan, log line> | <repo, board database> |
| Researcher | <subagent, model, call cap> | <source list> | <research file per lane> | <read-only web, shared drive read> |
| Builder | <subagent, model, call cap> | <plan, research, rules> | <draft with claim ledger> | <repo> |
| Verifier | <subagent, model, call cap, never the builder> | <draft, ledger, rules> | <verdict in the draft file> | <repo, same access as builder> |
| Merger | <only if lanes fan out; otherwise none> | <verified lane outputs> | <one deliverable> | <repo> |
| Improver | <the lane, on a set day> | <results, owner edits, posted set> | <lessons, one promoted lesson> | <repo> |

## Edges

<Who feeds whom, in order. Mark which researcher lanes run in parallel and which steps wait on another. Delete fake waiting.>

## Owner gates

- Gate 1, direction: <where, what the owner sees, how strict, default after how many hours or none>.
- Gate 2, output: <where, what the owner sees, how strict, no default for the first two weeks if outward>.
- Owner minutes per run: <number and what they are spent on>.

## State files

<Names and locations: plan, research per lane, draft, review, final, lessons, log. Say what is committed and what stays local.>

## Failure modes

<List what the verifier hunts in this graph specifically: invented facts, claims with no ledger row, AI tells, wrong reader, regulated-topic advice, wrong price, quotation not in the saved source.>

## Deployment level

<L1, L2 or L3. The promotion criteria: for example three clean runs, or two weeks with no declined output.>

## Improver hooks

<What gets mined from each run (results, owner edits, declines). Where the lessons land. Which lesson is marked for promotion to the shared library.>
