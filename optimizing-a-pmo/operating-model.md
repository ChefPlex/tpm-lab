# Operating Model

**Status:** 🚧 In progress

## The lever

Without a lever, a PMO can only produce reports, and reports alone do not change outcomes. Name one lever in the charter in the first month. For example: no commitment on the riskiest tier is accepted until its dependencies are signed by the teams that will deliver them, and the portfolio review can stop or delay a program on that tier. That is a gate. Call it one, and keep it to that tier. The lesson from companies that removed central review bodies is not to gate everything, not that a gate is never right.

## The money ledger

A CFO will ask what this returns. Agree a ledger with Finance and review it every quarter.

| Line | What it counts |
|:---|:---|
| PMO cost | The office's own fully loaded annual cost |
| Capacity freed | Work stopped or merged through portfolio decisions, at loaded engineering cost |
| Cost of delay | On the five biggest programs, estimated the way Finance and Product agree to |
| Spend avoided | Commitments not made, vendors not engaged, duplicate work stopped |
| Data still flowing | Capitalization and audit evidence confirmed intact |

Targets on the PMO's own measures are fine. Targets on team delivery metrics are not: once a measure becomes a target, people steer the number instead of the result. Even the PMO's own measures can be gamed, so pair each one with a definition someone outside the PMO checks.

## Governance tiers

| Tier | Typical work | Governance |
|:---|:---|:---|
| 1 | Regulatory, security-critical, payments, multi-year platform change; five or more teams; hard to reverse | Charter, sponsor, the gate, dependency records, a readiness review (also a gate), a decision log. The PMO owns the evidence trail; the control owner keeps the approval |
| 2 | Cross-functional; three or more teams, or a scarce shared team | Short charter, a named owner, a dependency list, the monthly portfolio review |
| 3 | One or two teams; easy to reverse | The team's plan, a named owner, visible in the portfolio view |
| 4 | One team, local | Nothing from the PMO |
| V | Delivered by a vendor or contractor | Contract milestones, acceptance criteria, change control and a named internal owner. Team ownership does not transfer to a fixed-price vendor |

Meet internal audit and security in the first week. Regulated change still needs documented approval by an authorized person, so self-service checklists replace approvals only where no outside party requires one.

## Dashboards and comparisons

- **Keep one portfolio view with red, amber and green.** Change what drives the colour: forecast against the team's own history, dependency age, decisions overdue. Run it beside the old dashboard for a quarter before retiring the old one. If the dashboard goes first, the people who still need that information will rebuild it in their own spreadsheets, and the data splits.
- **Compare groups on forecast reliability, not output.** Does each group hit its own forecasts, and does its stated confidence come true about as often as it says? Ranking teams on output pushes them to optimize the ranking instead of the result.
- **No targets on team delivery metrics.** Trends, owned by the teams, shown at team level.
- **Check the data before it goes upward.** Sample the tracker data and publish the error rate before any automated status reaches leadership.
- **Start with conversations, not integrations.** Build the data pipeline once you know which numbers matter.

## Capacity, dependencies and decisions

- **Capacity in layers:** run-the-business, regulatory and security, committed, discretionary, and a protected buffer for unplanned work at the team's own historical rate. Count skills on teams, not interchangeable headcount. Leave slack on purpose: wait times climb sharply as people approach full load.
- **Every new yes names what it displaces.** That turns capacity from a gate into a visible trade.
- **Dependencies as short records:** what is needed, from whom, by when, the committed date, confidence, the fallback, the decision date, and the clock for escalation. Measure what the record costs teams and drop fields no decision depends on. When the same dependency keeps failing, look for the interface or ownership split behind it.
- **Decisions with one owner and a date,** a decision log, and a rule that reopening a decision needs new information. Updates lead with the decision: what we see, what it means, the options, the recommendation, who decides and by when.

## Mechanisms

Hold every recurring ritual to one test: a tool, that people actually use, that someone inspects, with the results changing the next round. Give each one an owner and an expiry date.

| Mechanism | Purpose | Keep it light by |
|:---|:---|:---|
| Weekly delivery review | Decisions on blocked work | Only items that need a decision; written first |
| Monthly portfolio review | Trades, and the gate on the riskiest tier | Every new yes names what it displaces |
| Quarterly planning | Commit against real capacity | A fast path for small, reversible work, so it does not have to ride on a big initiative |
| Readiness review | Launch safety on the top two tiers | It is a gate; say so |
| Correction of errors | Learn from misses | Actions with an owner and a due date, never blame |
| Mechanism audit | Retire mechanisms that no longer pay for themselves | Quarterly; something gets retired every time |

The model has to pass its own test: for each mechanism it adds, it removes a meeting or a report.

## People and roles

- Define the TPM role by the outcome it keeps true across teams and the decisions it brings, rather than by tracking work on behalf of engineering managers.
- Competencies: technical fluency, written decision framing, dependency and risk reasoning, influence, financial literacy, coaching and vendor management.
- Build a career ladder for the role from the start.

## AI in the PMO

Automate summaries of validated data only, and show the source of every number. A local productivity gain is not a system gain, so measure delivery for the whole system. Fix or retire a process that is not working before automating it.

## Maturity

1. **Reporting:** collects status. Partners see it mainly as a reporting step.
2. **Coordinating:** runs dependencies and meetings. Partners work with it when they need to.
3. **Predictable:** forecasts hold and capacity is visible. Trusted for dates.
4. **Decision-making:** brings trade-offs early and owns the portfolio view. Sought out for hard programs.
5. **Learning:** finds the systemic causes of delay and removes them, including its own mechanisms.

Stopping at level 3 or 4 can be the right call when the business moves faster than optimizing pays back. These levels are a working frame, not a researched scale.
