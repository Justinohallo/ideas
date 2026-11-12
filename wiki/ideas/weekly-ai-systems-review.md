# Weekly AI systems review

**Title:** Weekly AI systems review
**Thesis:** A fixed weekly review that measures whether each project is moving, and how its structure changed, is how the whole AI system gets self-improving instead of running in quicksand.
**Status:** 🔍 interviewed
**Conviction:** high
**Domains:** ai, work, life
**Related:** none yet (first idea in the wiki)
**Source:** _source/2026-11-12-weekly-ai-systems-review.md, _source/2026-11-12-weekly-ai-systems-review.interview.md

## The idea

Justin works all day on top of Claude Projects: a GitHub repo as the data layer, the Claude Project as the control layer. Some projects work and some stall, and he wants a recurring review that makes the difference visible. In his words, the system should keep providing value: "Saves me time, surfaces ideas, completes projects."

The weekly review checks whether things are moving and produces a journal of actions. It captures two kinds of change per project: movement toward its goal, and how its structure changed ("What systems were updated. What scheduled tasks?"). The monthly os-audit consumes those journals. He wants all of it documented "so we can see how we changed things."

## Why he believes it

His reference pair is Hyrox (going great) and Burrard Works (failing). Hyrox "has a fixed date, and a program in place," and "is going to happen"; it gets tweaked as it runs. Burrard Works "is an idea, and the idea is messy," with no hard deadline ("i blew it anyway") and no goal he's held accountable to. His diagnosis: "Hyrox has a cadence to it while Burrard works does not. So we always know what we are working on next."

The other trigger is Anthropic's published practice of updating your system every week, which he wants to mimic. ❓ Which piece he means isn't recorded; add the link as a new capture.

## Strongest objection

Stated by the interviewer: a review can detect that a project has no cadence but can't fix it. Burrard Works is stalled on an unmade decision, and a review becomes one more meta-task to procrastinate on.

His answer: "My only hope is that we can surface this information consistently and design a habit around addressing it."

*Agent synthesis:* that answer leans on habit, which is what's failing on Burrard Works. Hyrox runs on an external date. The review likely needs its own forcing function: a fixed weekly slot, ending in a forced choice per stalled project (set a dated next action, park, or kill). This maps onto the five-line project header, whose "Next action + date" and "Who's waiting" lines are what the review would check against reality.

## What would change his mind

"If we saw that there was no progress made after a certain amount of time, it might be time to kill the project and be realistic."

## So what

Build it: a weekly review routine that reads each project's goal movement and structural changes and writes a journal; os-audit reads the journals monthly. Earlier framing ("consistency between everything") gave way in the interview to measuring outcomes and diagnosing stalls.

## Open questions

- ❓ Tension: the kill condition above versus "But this cannot happen, we need to get this launched yesterday" about Burrard Works. If kill is off the table, the only forced choice left for it is a dated next action.
- ❓ What's the measure of "moving"? Dated next action hit or missed is the agent's proposal; not yet agreed.
- ❓ Where does the journal live, per project repo or one central log?
- ❓ Which Anthropic source triggered this?

## Extraction

Buildable. Goes through idea-boardroom before Linear. No verdict yet.
