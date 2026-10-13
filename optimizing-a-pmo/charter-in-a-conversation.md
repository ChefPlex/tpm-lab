# A Charter in One Conversation

**Status:** 🚧 In progress

When a PMO re-baselines everything in flight, every project, program and portfolio needs a charter, and some will not have one, or will have one that has not been revisited since kickoff. Writing them all from scratch would stall the improvement work. This is the fast way: one recorded conversation, a set of questions, and an AI assistant that turns the transcript into a first draft. The draft is something to work from, not the finished charter.

It serves both cases in a re-baseline: **starting a piece of work again from the beginning,** or **checking that work already running is still the right work,** with the right people, money and time behind it.

## Before the call

- **Who:** the sponsor, the person who owns the work (project, program or portfolio manager), and the technical lead. Forty-five minutes.
- **Where:** Google Meet, Microsoft Teams or a Slack huddle, with recording and the transcript turned on. Tell everyone it is being recorded and why.
- **Which tool:** use the AI assistant your company has approved for its own material. A transcript of a charter conversation holds plans, budgets and names, so it does not go into a personal account.
- **Bring:** the existing charter or plan, if there is one, and the current status.

## The questions

Ask them in this order. They follow the sections of the [Program Charter Template](https://github.com/ChefPlex/tpm-templates/blob/main/program-charter-template.md), so the draft drops straight into it. Let people talk; the transcript will catch the detail.

**1. Why are we doing this**
- What problem does this solve, and for whom? What happens if we do nothing?
- Which company goal does it serve, and who would say so?

**2. What we are building**
- In one sentence, what will exist when this is finished that does not exist today?
- How will we know it worked? Which number moves, and by how much?
- What does "done" mean, and who decides it is done?

**3. Scope**
- What is in? What is explicitly out, even though someone will ask for it?
- Are we building this or buying it, and why?

**4. Approach and milestones**
- What are the three to five milestones that matter? When is each due, and why that date?
- Is any date fixed from outside: a regulator, a customer, a contract?

**5. Resources: the three constraints**
- **People:** who is on it, how much of their time, and who is missing?
- **Money:** what is the budget, and what has been spent so far?
- **Time:** when must it finish? If it slips, what does that cost?
- If one of the three has to give, which one?

**6. Stakeholders and communications**
- Who decides, who does the work, who must be consulted, who needs to be told?
- Who outside the team could stop or delay this, and do they know about it? Who owns the benefit after it ships?

**7. Risks, assumptions and dependencies**
- What worries you most about this?
- What are we assuming is true that we have not checked?
- What do we need from other teams, by when, and have they agreed?

**8. Compliance and reviews**
- Does security, legal, privacy or audit need to review or approve anything?

**9. Operational handoff**
- Who runs it after it ships, and do they know that yet?

**For a re-baseline, add four:**
- Is this still the right work? Would we start it today, knowing what we know now?
- What has changed since it started?
- Does it still have the people, money and time it needs, or has some of it moved elsewhere since it started?
- What new date can you commit to, and what latitude do you need while we learn?

### Adjust for the level

| Level | Spend more time on |
|:---|:---|
| **Project** | Deliverables, the definition of done, the milestones and the team |
| **Program** | The benefits, how the projects depend on each other, and who owns each benefit after delivery |
| **Portfolio** | The strategic objectives it serves, how work is chosen and stopped, the funding, and the governing body |

## The prompt

Paste the transcript after this prompt in your approved AI assistant. It is built on five parts: the role, the goal, the audience, the context and the output.

```
You are an experienced program manager helping draft a charter.

GOAL: Turn the meeting transcript below into a first-draft charter for a
[project | program | portfolio] called [NAME]. This is a starting draft for
the team to correct, not a final document.

AUDIENCE: The sponsor and the delivery team, who will review and sign it.

CONTEXT: The meeting was a charter conversation. [It is a re-baseline of work
already in flight | It is a new piece of work.]

OUTPUT: A charter with these sections, in this order:
1. Why are we doing this (problem, strategic alignment)
2. What we are building (overview, objectives, definition of done, business metrics)
3. Scope (in, out, build or buy)
4. Approach and milestones (approach, milestones with dates, fixed constraints)
5. Resources (people, budget, time; which constraint gives first)
6. Stakeholders (a RACI table and a short stakeholder map)
7. Risks, assumptions and dependencies (a table for each)
8. Compliance and reviews
9. Operational handoff

RULES:
- Use only what was said in the transcript. Never invent a number, date,
  name, budget or commitment.
- Where something was not said, write [MISSING: what is needed, and who
  should supply it].
- Where people disagreed, record both positions and who held each.
- Keep figures exactly as spoken, and note who said them.
- End with a list of open questions, most important first.

TRANSCRIPT:
[paste here]
```

## After the call

- **Read the draft against the recording,** not against memory. AI drafts get small things wrong confidently.
- **Close every [MISSING] item** with the person named, then put the draft into the charter template.
- **Get the sponsor's sign-off.** The signature is what makes the charter a commitment.
- **Feed the re-baseline:** the new date and latitude go into the [re-baseline](first-principles.md#re-baseline-once-with-a-learning-margin), the costs and benefits into the [NPV](npv-method.md), and the stakeholders into the [register](stakeholders.md).

## Related

- [First Principles](first-principles.md)
- [Program Charter Template](https://github.com/ChefPlex/tpm-templates/blob/main/program-charter-template.md)
- [Stakeholder Engagement Playbook](https://github.com/ChefPlex/tpm-templates/blob/main/stakeholder-engagement-playbook.md)
- [Meeting Notes to Actions prompt](https://github.com/ChefPlex/ai-automations/blob/main/prompts/junior-tpm/meeting-notes-to-actions.md)
