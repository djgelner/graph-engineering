---
name: graph-engineering
description: Turn any recurring workflow into the smallest agentic graph that improves the work. Use whenever someone asks to "graph" a workflow, design how a set of AI agents should be organized, systematize a recurring process (content, outbound, fulfillment, research, client deliverables, a build), or produce a graph-architecture recommendation. Designs and specs the graph; it does not run unattended jobs without a supervised first run.
---

# Graph Engineering: the Basic Shape

Engine and cartridge. The **Basic Shape** is the engine: a fixed set of roles with a fixed direction of flow and two human gates. Each workflow is a **cartridge**: a short spec naming the roles it actually needs, the files they pass, the gates, and the failure modes the skeptic hunts for. New workflows get a new cartridge, never a new engine.

```
                CHIEF OF STAFF  (across projects; keeps the board; escalates to the owner)
                      |
                 ARCHITECT  (one per project; plans the runs; adversarial to drift)
                      |
        RESEARCHER  (gathers context; spawns parallel lanes when the job splits)
                      |
            -- OWNER GATE 1 --  (approve the direction before build effort is spent)
                      |
             DRAFTER/BUILDER <--> VERIFIER/ADVERSARY   (loop until it passes)
                      |
                   MERGER  (only when lanes fan out; otherwise folded into the Builder)
                      |
            -- OWNER GATE 2 --  (approve the output before it ships, posts, sends or pays)
                      |
                  IMPROVER  (improves the graph; writes the lessons down; pings the Architect)
                      +--------> back to ARCHITECT (the next run is smarter)
```

## Role cards (what great looks like)

**Chief of staff.** Reports on every active project from one board; keeps priorities as the owner sets them; escalates only what needs the owner's judgment; makes the owner's day easier, not busier. The only role that talks to the owner.

**Architect.** Owns one project. Plans each run, delegates with clear goals and written instructions, is adversarial to drift, keeps workers on task, verifies the Verifier's and Improver's deliverables, and owns the project's second brain (its files).

**Researcher.** Gathers context before anything is built: golden examples of the exact deliverable, ranked by stated metrics, with the archetype the S-tier shares; the owner's own prior work and voice where relevant; the facts a skeptic would ask for. Writes a report the Builder can work from. Splits into parallel lanes (a customer lane, a competitor lane, a distribution lane) when the job splits.

**Drafter or Builder.** Executes from the research. If the roles above did their jobs, this job is easy. Loops with the Verifier until the output passes. If it does not improve with context over time, fix the graph, not just the prompt.

**Verifier or Adversary.** The skeptic. Checks that the Builder did the job, that the Architect's assumptions hold, and that the research is grounded. Same access as the Builder, so it checks the work directly instead of trusting the summary. For outward copy it checks truth and voice. Never the lane that wrote the answer.

**Merger.** A distinct step only when the graph fans out into parallel lanes; it consolidates surviving, verified evidence into one deliverable. In a single-lane graph it folds into the Builder. Never staff a Merger a graph does not need.

**Improver.** Improves the graph itself. Assumes the Builder will make mistakes and the Researcher will make things up, and designs both out. Extracts the lessons from each run, writes them to the project's files, pings the Architect, and marks the lessons every graph should inherit.

**The owner.** Exactly two standing gates: approve the direction before build effort is spent; approve the output before it leaves. Gate strictness scales with blast radius.

## Design procedure

1. **State the final output in one sentence.** No graph until that sentence exists.
2. **List the jobs a great human team would do** to produce it. Verbs, not tools.
3. **Draw the dependencies; parallelize the rest.** Jobs that do not depend on each other run as parallel Researcher lanes. Delete fake waiting.
4. **Place the skeptic.** The Verifier gets its own lane with the same access as the Builder.
5. **Place the owner's gates by blast radius.** An internal draft: a light gate or none. A public post, a client deliverable, money moving, production data, anything sent to a person: a strict gate. Never remove gate 2 on externally visible output in a graph's first two weeks.
6. **Apply the smallest-graph rule.** Merge or delete any node that does not measurably improve quality. More agents is not better output; sometimes it is five workers confidently repeating the same wrong idea.
7. **Define the state.** Every node reads and writes named files in the run's folder (plan, research per lane, draft, review, final, lessons). The paper trail is the product's memory; the Improver commits the durable parts to the project's files.
8. **Run it by hand three times before automating.** If the manual runs do not beat the old way, automating produces mediocre work faster. Fix the graph first.
9. **Write the graph spec** (below) and register the cartridge.

## The graph spec (the cartridge document)

One document per graph, `GRAPH-<letter>-<name>.md`, with these sections:

- **Final output**: the one sentence.
- **Cadence and trigger**: on demand, scheduled, or event.
- **Nodes**: a table of role, who runs it (a session, a subagent, a script, a person), inputs, outputs, and the least set of tools and connectors it needs.
- **Edges**: who feeds whom; which lanes are parallel.
- **Owner gates**: where, how strict, what the owner sees, and the owner's minutes per run.
- **State files**: names, locations, what gets committed.
- **Failure modes**: what the Verifier hunts for in this graph specifically.
- **Deployment level** (below) and the promotion criteria.
- **Improver hooks**: what gets mined and where the lessons land.

The template is in `templates/GRAPH-SPEC-TEMPLATE.md`.

## Deployment ladder

- **L1, manual lanes.** Separate chats or sessions per role; the owner ferries state between them. Every new graph starts here. Promotion after three clean runs.
- **L2, sessions plus repo state.** Roles are agent sessions sharing a repository; nodes hand off through files in a run folder; git is the shared state; the log file is the channel to the chief of staff. Most graphs live here.
- **L3, orchestrated.** Scheduled runs plus glue for outside APIs. Only for graphs with a boring L2 record. Money-moving or send-capable connectors are never attached to unattended nodes, and the first scheduled run is supervised.

## Rules

- Workers and checkers are always separate lanes. No self-grading.
- Verification rigor is never traded for speed; prose in a log is not a gate; least privilege on every node; push and confirm; anything touching a live system gets a read of what is there first.
- A marketing graph's Verifier checks voice against the owner's own corpus and an AI-tell list, and allows no fabricated expertise, results or anecdotes.
- Content on regulated topics inherits the heavy-disclaimer rules of that field.
- Lessons marked for promotion flow up to the shared library so every graph inherits them.
- This skill designs and specs graphs. Instantiating one is a separate step (see `docs/HOW-GRAPHS-RUN.md`), and neither runs unattended jobs without the supervised first run.
- When asked to graph a brand-new workflow, interview only for what cannot be inferred: the final-output sentence, the cadence, the blast radius of the output, and which existing files it feeds. Batch the questions; respect velocity.

## Where to read next

- `docs/HOW-GRAPHS-RUN.md`: the runtime, from one chat to a scheduled fleet.
- `docs/PROMPTING.md`: how to prompt each role so the graph behaves.
- `docs/TIPS.md`: what we learned running these, including the expensive mistakes.
- `templates/`: the spec, the charter, the tick prompt, the setup turn, the log line.
- `examples/`: two worked cartridges.
