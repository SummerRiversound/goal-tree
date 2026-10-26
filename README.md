# goal-tree

**Your coding agent starts a big job by charging at the first task it sees.** Ask it to "launch the app" or "move the wiki off Notion" and it writes code before anyone has agreed what done looks like, which pieces are truly needed, or what comes first. This skill makes it stop and build the plan *with you*: a top goal, the goals under it, and an ordered list of milestones you can check.

![skill](https://img.shields.io/badge/type-agent%20skill-3d5a99) ![works with](https://img.shields.io/badge/works%20with-Claude%20Code%20%C2%B7%20any%20agent-2f8f5b) ![license](https://img.shields.io/badge/license-MIT-555) [![Ko-fi](https://img.shields.io/badge/Ko--fi-Buy%20me%20a%20coffee-FF5E5B?logo=ko-fi&logoColor=white)](https://ko-fi.com/riversound)

---

## What it looks like

You say: *"I want to build a habit-tracking app and get it on the Play Store."*

The agent doesn't start coding. It reads the repo, sees the goal is clear, and proposes a draft:

```
Top goal: Habit app live on the Play Store — done signal: installable from a store link

- in order to: 1. A user can track one habit end to end
    - in order to: 1.1 Create a habit and check it off      (guess: local storage only)
    - in order to: 1.2 See a streak for the last 7 days
- in order to: 2. The build passes Play Store review
    - in order to: 2.1 Privacy policy page at a public URL
    - in order to: 2.2 Signed release build uploaded to internal testing

Milestones, in order:
- [ ] M1. Create and check off a habit — done when: the flow runs on an emulator
- [ ] M2. ...
```

Then it asks only about what it guessed: *"Is local-only storage fine for the first release, or do you need sync?"* You answer, the tree changes, and nothing gets built until you say go.

When the goal is foggy (*"we should do something about onboarding"*), it asks questions first instead of drafting. When there are two or three reasonable directions, it offers them as choices with a recommendation.

## How it decides what belongs in the tree

The agent checks every goal two ways, and tells you which check it is using:

1. **Top-down, "in order to":** to reach the parent, *must* we have this? If not, it moves to "later". This test comes from the Intermediate Objectives map in Goldratt's Theory of Constraints, as described by H. William Dettmer.
2. **Bottom-up, "so that":** if every child is done, is the parent actually done? A gap means a goal is missing.
3. **Who:** when a goal depends on people changing what they do (users, a team, an approver), it asks about them before naming features. This comes from Gojko Adzic's Impact Mapping.

It keeps each goal to 3–5 children and at most three levels. Each lowest goal becomes a milestone with a check you can run (a command, a test, a screenshot, a live URL), never just "implemented". Milestones start unchecked and are ticked off only with evidence. Anthropic's write-up on long-running agents found the same pattern keeps agents from declaring victory early.

The result is saved as `goal-tree.md` next to your other planning docs, so the next session picks up from the first open milestone.

## When it runs

The agent reaches for it on its own when a request names an **outcome** that will take several sessions or three or more ordered deliverables, for example launching, migrating, replacing a system, or building a new product. It also runs when you ask for goals, milestones, a roadmap, or "where do I start". Korean phrasing (목표, 마일스톤, 로드맵, 어디서부터) triggers it too.

It stays out of the way for a one-line change, a bug fix, or work that a spec already decides.

## Install

**Claude Code / Claude agents**: clone it into your skills directory.

```bash
# personal (all projects)
git clone https://github.com/SummerRiversound/goal-tree ~/.claude/skills/goal-tree

# or shared with a project
git clone https://github.com/SummerRiversound/goal-tree .claude/skills/goal-tree
```

**Cursor / other agents**: paste the steps from [`SKILL.md`](./SKILL.md) into your rules file. Nothing in them depends on a specific tool.

## References

- H. William Dettmer, *The Logical Thinking Process*: the Intermediate Objectives (IO) map, a goal tree built on "in order to have A, we must have B". See also [Thinking processes (theory of constraints)](https://en.wikipedia.org/wiki/Thinking_processes_(theory_of_constraints)).
- Gojko Adzic, [*Impact Mapping*](https://www.impactmapping.org/): goals linked to the people whose behaviour must change.
- Anthropic, [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents): a full task list that starts as failing, worked one item at a time, ticked off only after real verification.
- Matt Pocock's [`grilling`](https://github.com/mattpocock/skills) skill: the numbered question rounds with a recommended answer under each.

## Contributing

Issues and PRs are welcome, especially example requests where the agent should have used the skill and didn't (or did and shouldn't have).

## Support

If this skill saves you time, you can [buy me a coffee](https://ko-fi.com/riversound). Thank you!

<a href="https://ko-fi.com/riversound"><img src="https://ko-fi.com/img/githubbutton_sm.svg" alt="Support me on Ko-fi" height="36"></a>

## License

MIT, see [`LICENSE`](./LICENSE).
