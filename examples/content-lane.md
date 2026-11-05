# Example cartridge: a founder content lane

This is a worked cartridge for a lane that turns a founder's real experience and the complaints of one target reader into short public posts on one platform, with the founder's involvement kept to a few minutes a week. It is rewritten from a real lane's spec with every name removed. Use it as a pattern, not a script.

## Final output

Five posts a week on one platform in the owner's own voice, each traced to a mined complaint from the target reader or to the owner's own words, approved by the owner with one click each, posted from the owner's account by the owner's own local assistant, with an email list growing from day one and a weekly score of qualified followers, profile visits, inbound messages and sign-ups.

## The reader and the order

The lane serves the company's products one at a time, in the order the owner sets, with one reader and one platform each. The first product's reader is the owner or managing partner of a small firm who would buy the product's catalog. Four posts in five are about the reader's problem and the fix. One in five is about the catalog, and prices come only from the catalog of record. The lane stays on the first product until two clean weeks: ten posts accepted and posted, the posting task running, and no declined post. For each later product, the lane first proposes the reader and the platform as a decision on the board, argued from the product's own discovery reports, before a single post is drafted.

## Cadence and trigger

Scheduled, one run each weekday at a quiet hour. Monday plans and drafts the week. Tuesday to Thursday process the board and the queues. Friday is the improver run. No run at the weekend.

## Nodes

| Node | Who | Reads | Writes |
|---|---|---|---|
| Architect | the lane session, biggest model | charter, log, board | the weekly plan, the board, the log line |
| Scout, public | mid-model subagent, call cap stated | the mining source list | complaints in the reader's own words, each with URL and date |
| Scout, owner | the lane itself | the owner's corpus and conversation notes | the owner's stories, mistakes, opinions and numbers, each quoted |
| Drafter | mid-model subagent, call cap stated | plan, mined complaints, owner material, copy rules, lessons | one file per post with a claim ledger |
| Verifier | biggest-model subagent, never the drafter | the draft, ledger, copy rules, the AI-tell list | the verdict in the post file; a fail loops once |
| Publisher | the owner's local assistant, on the owner's machine and account | the approved file | the post; "posted <date>" on the entry |
| Measurer | a read-only local task | the job queue | a results file |
| Improver | the lane, Fridays | results, the owner's edits, the posted set | lessons, five variations of a post that worked, one lesson marked for promotion |

There is no merger. A single lane folds it into the architect.

## Edges

Monday: the two scouts run in sequence, then the plan goes on the board (gate 1), then five drafts go through the verifier loop, then the five posts go on the board (gate 2), dated Tuesday to the next Monday. Later days: an accepted post is copied into the approved file with its date. An edit note from the owner becomes a revision and a lessons entry. A declined post is logged with its reason. Weekly mining and analytics jobs are written to the queue when due.

## Owner gates

Gate 1, the week's plan: zero minutes when the owner lets it default to Accept after 24 hours. Gate 2, each post: about ten minutes a week, five accepts or an edit in the owner's own words, with no default in the first two weeks. An optional weekly conversation of up to an hour in the lane's chat gives the scout real material; the lane runs without it.

## State files

A folder per week with the plan, the mined complaints, the owner's material and the metrics. One file per post, holding an id, a date, a slot, a status, the claim ledger, the draft, the verdict and the final. Conversation notes by date. A lessons file of the owner's edits, verbatim, each with the rule it implies. The log. Nothing in the folder is posted by the lane.

## Failure modes the verifier hunts

An invented anecdote, number or client. A claim with no ledger row. AI tells, above all the em dash. A post that talks to a crowd instead of one reader. Advice or a promised outcome on a regulated topic, where the framing must stay educational. A product post that names a price not in the catalog of record. A hook copied from the method source instead of from the reader's own words. A post that reads as engagement bait: a question for its own sake, a hashtag, an emoji.

## Deployment level

L2 from the first day, with gate 2 strict. Nothing reaches the approved file without the owner's accept on that exact text. Promotion to a 24-hour default on gate 2 only after two weeks with no declined post and the owner's word. Posting is the owner's own machine and account under the owner's standing instruction, which is what makes it the owner's send and not the lane's.

## Improver hooks

Each Friday the improver records what worked, from the results file. It records what the owner changed, verbatim, into the lessons file. It queues five variations of the best post for the next week. It marks one lesson for promotion in the log, so the chief of staff can carry it to the other lanes.
