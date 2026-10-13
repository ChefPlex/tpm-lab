# Net Present Value, Step by Step

**Status:** 🚧 In progress

The [first principles](first-principles.md) say to put a net present value on everything in flight. This is rarely part of a project or program manager's role today, so the PMO gives them a clear method to follow. This is that method. It is written for the person who owns the work, not for Finance, and it asks one question: **from today, is continuing this work worth more than stopping it?**

## What NPV means, in one line

Money later is worth less than money now. NPV adds up every future cost and benefit after shrinking each one by how far away it is, so that a dollar in year three counts for less than a dollar today. If the total is above zero, the work returns more than the organization's minimum rate. If it is below zero, the money would do better elsewhere.

The formula, for the curious: NPV = the sum, over each year *t*, of (benefits − costs in year *t*) ÷ (1 + *r*)<sup>*t*</sup>, where *r* is the discount rate and *t* = 0 is this year.

## Step 1: Get three numbers from Finance

Take these from Finance, not from an estimate. Use the same ones for every program, so that programs can be compared fairly.

- **The discount rate.** Finance may call it the hurdle rate or the cost of capital. The examples below use 10 percent.
- **The horizon.** How many years of benefit to count. Three to five years after go-live is common for technology work.
- **The loaded cost of a person.** Salary plus benefits and overhead, per year or per hour, so every program costs its people the same way.

## Step 2: Forget what has already been spent

Money already spent is gone whichever way you decide. It does not go in the calculation. A program that has spent $1.2 million and needs $400,000 more is judged on the $400,000. This step is the hardest to apply, because walking away from a large spend feels like waste. The question is only whether the next dollar is worth spending.

## Step 3: List the remaining costs, year by year

- People: the full-time equivalents still needed, at the loaded cost from step 1.
- Vendors, licences and infrastructure still to be paid.
- The cost to run it after go-live: support, hosting, maintenance. This cost is easy to miss, so check for it.

## Step 4: List the benefits, year by year, each with an owner

Every benefit line needs a named owner outside the PMO who agrees the number, usually the [benefit owner](stakeholders.md) for the program. Include a benefit only when its owner has agreed to the number.

- **Revenue:** new sales, or sales protected.
- **Costs avoided:** a system retired, a vendor contract ended, headcount not hired.
- **Time saved:** hours saved × loaded hourly cost × the share of people who will actually use it. Count it only if the saved time is used for something.
- **Risk reduced:** the expected loss avoided, which is likelihood × impact before, minus likelihood × impact after.

Benefits start when the work goes live, not when it is approved, and they usually ramp up over the first year.

## Step 5: Run three cases, not one

A single number looks more certain than its inputs are. Run:

- **Base:** the plan as it stands.
- **Low:** late by the amount your history says is likely, adoption lower, costs higher.
- **High:** the plan delivered with good adoption.

## Step 6: Price stopping, too

Stopping is not free. List what it would cost to stop now: contract termination fees, write-offs, a commitment to a customer or regulator that would have to be met another way. That gives the value of stopping, usually a small negative number. Compare continuing with stopping, not with zero.

## Step 7: Discount and add up

Multiply each year's net figure (benefits minus costs) by that year's discount factor, then add the results. At 10 percent the factors are:

| Year | 0 (this year) | 1 | 2 | 3 | 4 | 5 |
|:---|:---|:---|:---|:---|:---|:---|
| Factor | 1.000 | 0.909 | 0.826 | 0.751 | 0.683 | 0.621 |

⚠️ **The spreadsheet trap.** The `NPV` function in Excel and Google Sheets treats the first value as one year away, so it discounts this year's figure too. Put this year's figure outside the function: `= year0 + NPV(rate, year1:yearN)`. Getting this wrong understates the result, by about 9 percent in the example below.

## Worked example

A program has already spent $1.2 million (ignored, step 2). It needs $400,000 more this year to finish. It then costs $100,000 a year to run. The benefit owner signs for $300,000 in its first year live, rising to $500,000. Stopping now would cost $50,000 in contract fees. Figures in thousands:

| | Year 0 | Year 1 | Year 2 | Year 3 | NPV |
|:---|:---|:---|:---|:---|:---|
| **Base:** net figure | −400 | 200 | 400 | 400 | |
| Discounted | −400.0 | 181.8 | 330.6 | 300.5 | **+412.9** |
| **Low:** a year late, 60% adoption | −400 | −200 | 80 | 200 | |
| Discounted | −400.0 | −181.8 | 66.1 | 150.3 | **−365.4** |
| **High:** good adoption | −400 | 250 | 500 | 500 | **+616.2** |
| **Stop now** | −50 | | | | **−50** |

The base and high cases beat stopping by a wide margin. The low case is worse than stopping. Being a year late with 60 percent adoption turns this program from a good investment into a poor one.

## Step 8: Decide, and write down the trigger

| What the cases show | What to recommend |
|:---|:---|
| Even the low case beats stopping | Continue |
| Even the base case loses to stopping | Stop, or cut the scope and run it again |
| Base beats stopping, low does not (the example) | Continue, with a named checkpoint: the date and the signal that would mean the low case is happening. In the example: if go-live slips past a set date, bring the stop decision back. |

The NPV is one input to the portfolio decision, not the decision. The portfolio review weighs it with strategic fit and risk in a scoring model. [First Principles](first-principles.md#net-present-value-for-everything-in-flight) explains why.

## What does not get an NPV

Security, regulatory and run-the-business work that must be done anyway. Do not force a revenue story onto it. Make its case with the cost of doing nothing, using the [Executive Investment Framework](https://github.com/ChefPlex/program-reporting-frameworks/blob/main/executive-investment-framework.md), and compare ways of meeting the obligation on cost.

## Keep it current

Record every NPV in the portfolio's inventory of work, with its owner, the date, and the assumptions behind each line. Redo it each quarter, and whenever a program re-baselines. An NPV that is a year old describes a program that has since changed.
