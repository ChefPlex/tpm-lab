# What One More Change Costs, Step by Step

**Status:** 🚧 In progress

A sponsor or a client asks for "one more small change". The usual answer is a guess: it sounds small, so it probably is. This method replaces the guess with two numbers, worked out before anyone says yes: **how far the change moves the finish date, and what it costs.** It needs a schedule with dependencies, a loaded cost per person, and the program's fixed dates. Most programs have the first two. Few have the third written down, and the third is where most of the money is.

The standard calls this step Perform Integrated Change Control. It sits beside Control Schedule and Control Costs because a change touches both at once. This page is the working version.

## Step 1: Write the change down

One paragraph, before any analysis:

- **What** changes: new work, more of existing work, or work done again.
- **Who asked**, and **why**: the business reason in their words.
- **By when** they need it. "Before go-live" and "eventually" lead to very different answers.

A change that cannot be written down in one paragraph is two changes, or it is not yet understood.

## Step 2: Find the tasks it touches

Map the change onto the schedule. For each task it touches, record the extra duration and who does the work. Look past the obvious task: more data to migrate also means more data to test, and a new interface also means a new security review.

## Step 3: Check the float on each task

Float is how many days a task can slip before it moves the finish date. Tasks with zero float form the critical path.

- **Extra days ≤ float:** the finish date does not move. But the float is spent, and it was protecting the program against every other surprise on that path. Record that it is gone.
- **Extra days > float:** the finish date moves by the difference, **extra days minus float**.
- **The critical path can change.** A path with a few days of float becomes the critical path once those days are used. Re-run the schedule. Do not reason about it from memory.

## Step 4: Check the people, not only the tasks

A change can avoid every critical task and still delay the program, because it needs a person who is on the critical path. If the same engineer builds the critical item and the change, the change waits or the critical item does. Check each named resource on the change against the critical path.

## Step 5: Price it, in three parts

1. **Direct cost:** the extra person-days × the loaded daily cost, plus any vendor, licence or infrastructure cost.
2. **Time cost:** the days the finish date moves × the daily run rate of the team that stays on the program while it is late. This part is usually larger than the direct cost, and it is the part that gets left out.
3. **Fixed dates the slip crosses:** a contract or licence that ends, a change freeze, a booked training week, a customer or regulator commitment, a person who leaves on a known date. Crossing one of these is not a cost per day. It is a step: one more day past the date can cost a month's extension.

⭐ **Put the fixed dates in the schedule as milestones.** In the cutover plans I have run, the end-of-contract date for each system being replaced sat in the plan as its own milestone, some weeks after go-live. The gap between go-live and that milestone is a buffer kept on purpose: it pays for running the old and new systems side by side. A change that eats the buffer shows on the schedule, not in an invoice after the fact.

## Step 6: Offer options, not only yes or no

| Option | What it means | What to price |
|:---|:---|:---|
| **Add** | Take the change and re-baseline the date and budget | The full cost from step 5 |
| **Add people** | Do the change in parallel so the date moves less | The added people, and whether the work really splits |
| **Swap** | Take the change and drop scope of equal size | What the dropped scope was worth, and to whom |
| **Defer** | Do it in the next release | The cost of a workaround until then |

## Step 7: Decide at the right level

Set the levels at kickoff, in the charter, so that nobody has to ask who decides.

| The change | Who decides |
|:---|:---|
| Stays inside float and the program's contingency | The program manager, who logs it |
| Moves a milestone or uses more than the agreed share of contingency | The sponsor |
| Crosses a fixed date from step 5, or changes what was promised to a customer or regulator | The steering group or change board |

## Step 8: Re-baseline and record it

Record every change in the change log, approved or not: the request, the impact found, the option chosen, who decided, and the date. Then update the baseline. A program that takes changes without re-baselining reports variance against a plan that no longer exists.

## Worked example

Illustrative figures. A system replacement, in working days. Loaded cost: $800 a day per person. Six people stay on the program while it runs, so the run rate is $4,800 a day.

| Task | Days | After |
|:---|:---|:---|
| A. Requirements | 10 | |
| B. Build | 15 | A |
| C. Data mapping | 8 | A |
| D. Data load | 5 | C |
| E. Test | 10 | B and D |
| Go-live | 0 | E |
| Old system's contract ends | milestone, day 50 | |

The critical path is A → B → E, so go-live is **day 35**. The data path (A → C → D → E) takes 33 days, so it has **2 days of float**. The old contract ends on day 50, which leaves a **15-day buffer** for running both systems side by side.

**Change 1: one more data set to migrate.** Data mapping grows by 6 days. It is not a critical task, so it sounds safe.

- Float on C is 2 days. 6 − 2 = **4 days late: go-live moves to day 39.**
- The data path is now the critical path, and Build has 4 days of float. The critical path moved.
- Direct cost: 6 days × $800 = $4,800. Time cost: 4 days × $4,800 = $19,200. **Total: $24,000**, five times the direct cost alone.
- The buffer to the contract end drops from 15 days to 11.

**Change 2, a month later: a new interface to test.** Test grows by 12 days, with two testers. Test has no float.

- **12 days late: go-live moves to day 51, one day past the contract end.**
- Direct cost: 12 days × 2 testers × $800 = $19,200. Time cost: 12 × $4,800 = $57,600. Contract extension (illustrative): $40,000. **Total: $116,800.**
- The buffer is gone. There is now no time to run both systems side by side.

The second change has twice the days of the first and costs almost five times as much, because it crosses a fixed date. The options:

| Option | Go-live | Cost | Note |
|:---|:---|:---|:---|
| Add | day 51 | $116,800 | Pays for the extension and gives up the parallel run |
| Add two testers | day 45 | $48,000 | 24 tester-days in 6 calendar days: $19,200 + 6 × $4,800. Keeps a 5-day buffer, if the test work really splits |
| Defer the interface to release 2 | day 39 | The workaround | Price the manual workaround until release 2 |

Change 2 crosses a fixed date, so it goes to the steering group under step 7, with these three options and a recommendation.

## What an AI tool can and cannot do here

If the schedule holds its dependencies, durations and named resources, steps 2 to 5 are arithmetic. A tool, AI or not, can run them in seconds and draft the options table. What a tool cannot do is know about a fixed date that is not in the plan. The contract end, the freeze and the leave dates have to be milestones first. A program that keeps them only in someone's head gets a confident answer that leaves out the largest cost.

## Keep it current

Run this for every change request, even the ones that look small. Change 1 looked small. Review the fixed dates each month: contracts get extended, freezes get announced, people change roles. A fixed date that is out of date is worse than none, because the analysis trusts it.
