# Graph Engineering

A Claude skill, and the documentation around it, for turning any recurring workflow into the smallest set of AI agents that improves the work: a chief of staff, one architect per project, researchers, a builder, a skeptic, and the human who approves twice. The shape is fixed; each workflow is a short cartridge on top of it.

It came out of running a fleet of agent lanes for a small company: content, outbound, research, product builds, each on its own schedule, each reporting through files, with one human approving from one board. Everything here is what survived contact with that.

## Install the skill

Copy `SKILL.md` into your project at `.claude/skills/graph-engineering/SKILL.md` (Claude Code reads it from there), or into your personal skills folder. Then ask: "graph this workflow" and name the workflow. The skill interviews you for the four things it cannot infer, designs the graph, and writes the spec.

## Read in this order

1. [SKILL.md](SKILL.md): the Basic Shape, the role cards, the design procedure, the spec format, the deployment ladder.
2. [docs/HOW-GRAPHS-RUN.md](docs/HOW-GRAPHS-RUN.md): how a graph actually runs, from a single chat to a scheduled fleet with a board.
3. [docs/PROMPTING.md](docs/PROMPTING.md): how to write the prompts that make each role behave.
4. [docs/TIPS.md](docs/TIPS.md): tips, tricks and the expensive lessons.
5. [templates/](templates/): the graph spec, the lane charter, the scheduled prompt, the setup turn, the log line.
6. [examples/](examples/): two worked cartridges, a content lane and a research-to-book lane.

The companion repository for the owner's board (one page with every lane, decisions as buttons, and a prompt the owner copies into a local assistant for anything that needs a real browser) is [whiteboard](https://github.com/djgelner/whiteboard).

## License

MIT. See [LICENSE](LICENSE).
