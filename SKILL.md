---
name: goal-tree
description: Build a goal tree with the user in conversation (top goal, then intermediate and leaf goals, then ordered milestones) before starting new work. Use when a request names an outcome rather than a task (launch, migrate, replace, build a product or service) that will span several sessions or 3+ ordered deliverables, or when the user asks for goals, milestones, a roadmap or where to start (목표, 마일스톤, 로드맵, 어디서부터). Not for a one-sentence change, a bug fix, or work a spec already decides.
---

# Goal tree

The tree is built **with** the user, not for them. Facts are yours to find; goals are theirs to own (Dettmer: only the owner of a system sets its goal). Your job is to make each choice easy: a draft when the way is clear, options when it forks, questions when it is foggy.

## 1. Read the ground

Before the first question, read what already answers some of it: the repo's CLAUDE.md or AGENTS.md, design and planning docs, linked issues, recent git log. Never ask the user for a fact a file or command can give.

Done when you can say, in one line each, what exists today and what the user asked for.

## 2. Settle the top goal

Gauge the fog on the top goal, then pick the matching move:

| Fog | Signal | Move |
|---|---|---|
| Clear | The outcome and a way to see it is reached are stated or obvious from the repo | Propose a full draft tree (steps 3–4) in one message; mark every node you guessed `guess:` and ask only about those |
| Forked | Two or three reasonable framings, and the choice changes the branches | Offer the framings as a multiple-choice question (AskUserQuestion in Claude Code), your recommendation first, one line of cost each |
| Foggy | Purpose, beneficiary or "done" signal unknown | Question rounds: number each question, put your recommended answer under it, phrase it so "yes" accepts the recommendation, and wait for answers before the next round. Top-down: why now, who benefits, what is observably true when it is done |

The top goal is one sentence plus its **done signal** (what someone could observe). Done when the user has confirmed both.

## 3. Grow the tree, one level per round

Under each confirmed node, propose its children, then put each node through the lenses below. Settle a level before opening the next; a child of an unconfirmed node is a later round. Keep the move from step 2 per branch: a clear branch gets a draft, a forked one gets options, a foggy one gets questions.

Lenses: name the one you are using in a short parenthetical the first time, so the user sees the method, not just the verdict.

- **In order to (necessity, Goldratt/Dettmer IO map):** "To have the parent, must we have this?" A no moves the node to Later / Out of scope, with the user's agreement.
- **So that (sufficiency):** read upward, "If all children are true, is the parent true?" A gap is a missing child; ask what fills it.
- **Who (Impact Mapping, Adzic):** when the goal depends on people (users, a team, an approver), ask whose behaviour must change and how, before naming features.
- **Shape:** 3–5 children per node, at most three levels under the top goal. Wider or deeper means a node is really two goals or a task disguised as a goal.

Done when every node is confirmed by the user or explicitly accepted as `guess:`, and both readings (top-down "in order to", bottom-up "so that") hold for every parent.

## 4. Turn leaves into milestones

Each leaf becomes a milestone:

- `done when:` an observable check (a command, a test, a screenshot, a live URL), never "implemented". It starts unchecked and flips only with evidence.
- `target:` where the check runs (local, simulator, staging, the live service).
- Order by prerequisite (Goldratt's prerequisite tree): what must be true before each can start. Put first the smallest milestone that proves the path end to end (a tracer bullet), even when it is not the most valuable.

Show the ordered list. Done when the user confirms the order and every leaf has a `done when:` they agree they could check.

## 5. Write it down

Write `goal-tree.md` where the repo keeps planning docs (ask once if there is no such place), in the conversation's language:

```markdown
# <effort> goal tree

Top goal: <one sentence> — done signal: <observable>

## Tree
- <top goal>
  - in order to: 1. <intermediate goal>
    - in order to: 1.1 <leaf goal>

## Milestones
- [ ] M1. <leaf> — done when: <check> — target: <where>

## Later / out of scope
- <node> — <why it was moved>

## Open questions
- <question> — <who answers>
```

Then point whatever the next session reads first (a progress note, the repo's agent instructions) at the first milestone.

## 6. Hand off and keep it true

Start building only after the user says to. Hand each milestone to the flow that fits it: an open design question to a design discussion or spec, a clear task straight to implementation.

In later sessions on this effort, read the tree first. Flip a milestone to `[x]` with `— evidence: <path or output>` on the same line. When reality contradicts a node, propose the edit to the user before changing the tree; goals stay theirs.
