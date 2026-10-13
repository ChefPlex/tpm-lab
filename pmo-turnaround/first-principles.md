# First Principles

**Status:** 🚧 In progress

To turn a PMO around, you need two things first: why it was created, and where it fell short. You cannot fix the gap until you can name it.

## Why a PMO exists

**Who.** A CTO or CIO with more programs, projects and portfolios than one person can follow, and more program, project and portfolio managers than one leader can manage directly.

**What.** The executive hands that work to an office. PMI's lexicon describes a PMO as an entity tasked with "centralizing activities related to the management of portfolios, programs, and/or projects." The office standardizes how status is reported, so every program can be read the same way. It also takes on the work of seeing and managing risk across all of them.

**Why.** It is a delegation of risk oversight. It is easy to call this a risk transfer, but PMI uses "transference" for "shifting the impact of a threat to a third party," such as an insurer or a contractor. When ownership moves inside an organization, PMI's term is escalation, and escalation moves risk up, not down. Handing risk oversight down to a PMO is delegation. The executive is still accountable. What the PMO takes on is the work: finding the risk, reporting it the same way every time, and getting it managed before it lands on the executive's desk.

**When and where.** Usually when the portfolio outgrows one leader's attention, and usually inside the technology organization the executive runs.

**How.** Through common reporting, common risk management, and a seat at the table where work is started, stopped and funded.

A turnaround starts by recovering that original mandate. Ask what the PMO was supposed to own, then ask where it stopped owning it. The gap between the two is the turnaround. The people who judge whether it closed are the PMO's [stakeholders](stakeholders.md).

## The three constraints

Every request to a PMO comes with three constraints: **time, money and people.** A team brings you people and money and asks for something organized within a certain time. The classic project triangle varies by source (scope, quality and performance all appear as the third point), but the request a PMO actually receives is usually framed in these three.

When teams are unhappy with a PMO, start with time. If work is not finishing when it was promised, that is probably the reason. There may be others, but it is the best place to begin.

## Reading red, amber and green

Red, amber and green describe the health of a portfolio, a program or a project. This is my own heuristic for reading them over time, not a published standard:

| Pattern | What it probably means |
|:---|:---|
| Green all the time | It was given more time, money or people than it needed |
| Yellow all the time | It was not given enough |
| Red | It is blocked, and needs a decision or intervention now |
| Mostly green, sometimes yellow | Healthy. The constraints are being used, not hoarded |

The aim is not a wall of green. A program that is always green is probably not using its constraints well. A program that leans yellow now and then, because someone chose to optimize for time, money or people, is doing its job.

The closest established method is Critical Chain buffer management. Its "fever chart" plots how much of a project's buffer has been used against how much of the work is complete. Using buffer is expected: green needs no action, the middle zone needs a look, and red requires corrective action ([Marris](https://www.critical-chain-projects.com/videos/theory/the-fever-chart-explained-by-philip-marris)).

**Before you read anything into the colours, check two things.**

- **Are the colours honest?** Constant green can also be misreporting: green on the outside, red on the inside. Sample the data behind the green before you conclude a program is over-resourced. The [operating model](operating-model.md) already says to check the data before it goes upward.
- **Are the thresholds objective?** If one manager calls red at a 10% slip and another at 25%, the pattern means nothing. Agree what drives each colour first. The [Program Status Reporting Framework](https://github.com/ChefPlex/program-reporting-frameworks/blob/main/program-status-reporting-framework.md) sets the definitions, requires a path to green for every yellow or red, and holds that a program should never go from green to red without a yellow in between.

## Net present value for everything in flight

During a turnaround, put a net present value on every current portfolio, program and project. The point is to prove whether each one is worth continuing.

PMI's portfolio standard frames this step as a review of the "inventory of work": work that is not aligned with strategy, or is unlikely to deliver its intended value, is closed. Its tool is a weighted scoring model, with return on investment as a measure, and it never names NPV. So use NPV as one input to a scoring model, beside strategic fit and risk, not as the only test.

Two limits to state up front:

- **Early numbers are unreliable.** In a study of new-product portfolios, Cooper, Edgett and Kleinschmidt found that "financial data are simply too unreliable during the course of a project, especially in the earlier phases when prioritization decisions are most needed" ([source](https://macsphere.mcmaster.ca/bitstream/11375/5432/1/fulltext.pdf)). Show ranges, not a single figure, and do not let a spreadsheet look more certain than its inputs.
- **Mandatory work has no revenue case.** Security, regulatory and run-the-business work is done because it must be. Put it in its own category, and make its case with the cost of doing nothing, as in the [Executive Investment Framework](https://github.com/ChefPlex/program-reporting-frameworks/blob/main/executive-investment-framework.md). For the rest, pair NPV with the cost of delay in the [money ledger](operating-model.md#the-money-ledger).

## Re-baseline once, with a learning margin

If nothing is meeting its dates, re-baseline everything. This sits in tension with the NPV section: you are proving value while also giving yourself room. That is deliberate. The re-baseline is the start of a learning period, while the PMO finds out what the work actually takes.

**Give yourself 10 to 20 percent latitude on time** while you learn. Hold it outside the baseline, as what PMI calls a management reserve: time set aside beyond the schedule baseline and released "for unforeseen work." Inside the baseline it would quietly become the plan. Then hold it to these rules:

- **Do it once, and document it.** The GAO's schedule guide treats re-baselining as rare, limited to new or reduced scope or a formal replan, and warns that it wipes out historical variance ([GAO-16-89G](https://www.gao.gov/assets/gao-16-89g.pdf)). Keep the old baseline, so the history survives.
- **Put change control on the new one.** A baseline that is revised to match whatever happened tells nobody anything.
- **Measure the latitude itself.** Track how much of the 10 to 20 percent each program uses. IT projects carry a fat tail: in Flyvbjerg and Budzier's study of 1,471 IT projects, one in six was a "Black Swan," with "a cost overrun of 200%, on average, and a schedule overrun of almost 70%" ([source](https://arxiv.org/abs/1304.0265)). A flat margin will cover the typical program and miss those.
- **End the learning period on a date.** Replace the flat percentage with ranges drawn from each team's own history. GAO sets schedule contingency the same way, from risk analysis at a chosen level of confidence rather than a fixed percentage.

## Sources

- PMI, *Lexicon of Project Management Terms*, version 5.0 (members' login), entries for project management office, risk transference, risk escalation and management reserve. Read 2026-10-13.
- PMI, *The Standard for Portfolio Management*, fourth edition (2017), sections on validating the portfolio and on evaluation.
- Flyvbjerg and Budzier, "Why Your IT Project May Be Riskier Than You Think," [abstract](https://arxiv.org/abs/1304.0265).
- Cooper, Edgett and Kleinschmidt, portfolio management in new product development, [working paper](https://macsphere.mcmaster.ca/bitstream/11375/5432/1/fulltext.pdf).
- GAO, *Schedule Assessment Guide*, [GAO-16-89G](https://www.gao.gov/assets/gao-16-89g.pdf).

## Related

- [The 90-Day Playbook](playbook.md)
- [Operating Model](operating-model.md)
- [What the Evidence Says](evidence.md)
