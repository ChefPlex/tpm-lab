# What the Evidence Says

**Status:** 🚧 In progress. Researched October 2026 and checked by an adversarial review. Labels: **documented** means read in the company's or author's own text; **reported** means a credible secondhand account; **folklore** means widely repeated with no primary source found.

## The largest gap

No source found shows that program offices, in any form, improve delivery. PMO research describes structures and survey correlations, not results, and no published case found is an inherited, disliked PMO that a new leader turned around. Treat everything below as design input for an experiment.

## Amazon

**Documented:**
- **A mechanism is a tool, its adoption, and inspection of the results,** iterated over time. ([AWS Operational Readiness Reviews, Building mechanisms](https://docs.aws.amazon.com/wellarchitected/latest/operational-readiness-reviews/building-mechanisms.html))
- **Correction of Errors** focuses "on corrective actions, not just documenting failures," and "is not a process for finding whom to blame." ([AWS, 2022](https://aws.amazon.com/blogs/mt/why-you-should-develop-a-correction-of-error-coe))
- **Operational Readiness Reviews** turn lessons from incidents into self-service questions teams answer for themselves, "without slowing builders down." ([AWS whitepaper, 2022](https://docs.aws.amazon.com/wellarchitected/latest/operational-readiness-reviews/wa-operational-readiness-reviews.html))
- **One-way and two-way door decisions:** heavy process on reversible decisions leads to "slowness, unthoughtful risk aversion, failure to experiment sufficiently." ([2015 shareholder letter](https://www.sec.gov/Archives/edgar/data/1018724/000119312516530910/d168744dex991.htm))
- **Escalation as a mechanism:** without it, "the default dispute resolution mechanism for this scenario is exhaustion." ([2016 letter](https://www.aboutamazon.com/news/company-news/2016-letter-to-shareholders))
- **Narratives take time:** a good six-page memo "might take a week or more." ([2017 letter](https://www.aboutamazon.com/news/company-news/2017-letter-to-shareholders))
- **Amazon removed a central cross-team review.** Its CEO describes a body that reviewed how many people-weeks each team's work would take: "This bottleneck constrained what we accomplished." It was fixed by turning shared components into services with stable interfaces, not by a better meeting. ([2023 letter](https://www.aboutamazon.com/news/company-news/amazon-ceo-andy-jassy-2023-letter-to-shareholders))
- **Process decays:** "unneeded processes get layered on that add little value." ([2024 letter](https://www.aboutamazon.com/news/company-news/amazon-ceo-andy-jassy-2024-letter-to-shareholders))

**Reported, not documented by Amazon:** the detailed Weekly Business Review practice (hundreds of metrics, a Finance facilitator) comes through a former Amazon executive. "Good intentions don't work, mechanisms do" is an Amazon saying with no dated source and two wordings.

## eBay

- **A real central planning layer exists.** eBay has posted roles for a "Planning, Program and Operational Excellence" function and Lead TPM roles owning consolidated annual planning, capacity frameworks, intake governance and dependency governance (2025 to 2026 postings).
- **It sits beside other models.** Several eBay business units have posted roles for their own PMOs, and mid-level TPMs are embedded in teams as accountable owners.
- **A former eBay chief architect describes the planning as centralized:** "an annual multi-month company-wide planning cycle," where smaller work survives only "like a rider on a congressional bill." His account is first-hand, ended around 2022, and he describes leaving on bad terms. ([InfoQ talk](https://www.infoq.com/presentations/platform-engineering-lessons/))
- **"Scale with low overhead"** appears in only one job-board copy of an eBay posting and may not be eBay's wording. It is a good design rule anyway: every standard should have a measured cost to the teams.

## Other companies

- **One named owner per item** is documented in [GitLab's handbook](https://handbook.gitlab.com/handbook/people-group/directly-responsible-individuals/) and reported at Apple ([Fortune, 2011](https://fortune.com/2011/05/09/inside-apple/)). No outcome data exists for it.
- **GitLab is also building a central engineering PMO,** so owners and a PMO are complements in its own case.
- **No large company found deliberately runs without program management.** The real no-PMO designs (Basecamp's six-week cycles, Valve's emergent leads) are small companies.
- **Will Larson (from Stripe):** programs maintain "a property across an organization" through data, goals and nudges folded into existing forums, but they are "a bad default tactic... a tool for deliberate use only." ([lethain.com](https://lethain.com/programs-owning-the-unownable/)) He also warns against defining the TPM role as taking project tracking off engineering managers. ([lethain.com](https://lethain.com/specialized-roles/))

## Metrics

- **DORA warns that turning its metrics into targets invites gaming,** and against comparing or blending teams. ([DORA metrics guide](https://dora.dev/guides/dora-metrics/))
- **Tracker data is often wrong:** one study of five open-source projects found about a third of "bug" reports were not bugs (Herzig, Just and Zeller, ICSE 2013).
- **No validated set of leading indicators of program failure was found.** Dependency age, decision age and work in progress are hypotheses worth testing locally.
- **Folklore, do not quote:** PMO closure rates ("half close within three years"), the Standish CHAOS failure rates (tested against 1,211 projects and found not to match reality by Eveleens and Verhoef, IEEE Software 2010), "flow efficiency is 15%," and "70% of transformations fail."

## Trust

- Trust rests on three perceived traits: **ability, benevolence and integrity** (Mayer, Davis and Schoorman, 1995). Ask about them separately.
- In lab studies, an apology repaired a competence failure better than a denial, while a denial worked better for an integrity accusation (Kim et al., 2004). Match the repair to the failure.

## Cases

- **UK Government Digital Service:** a new central unit with a political sponsor and spend controls, credited by the National Audit Office with £1.3 billion of IT savings over five years, later found to have "found it difficult to redefine its role as it has grown." It was a new unit, not an inherited PMO. ([NAO, 2017](https://www.nao.org.uk/reports/digital-transformation-in-government/))
- **US Department of Veterans Affairs:** five years after launching a project accountability system, its inspector general found two offices had not completed 30 of 36 required reviews for the projects sampled, and reviews were not independent. Governance on paper decays. ([VA OIG, 2015](https://www.oversight.gov/sites/default/files/oig-reports/VAOIG-13-03324-85.pdf))
- **The "Spotify model":** a former Spotify engineer wrote that it was "only ever aspirational and never fully implemented," with alignment and accountability left unfinished. ([Jeremiah Lee, 2020](https://www.jeremiahlee.com/posts/failed-squad-goals/))

## Not yet researched

Banks and large retailers, the closest analogues to an enterprise PMO. The 17 PMO case studies in Hobbs and Aubry's PMI book. Any study of decision logs, risk representation or priority-change rules. The accuracy of throughput-based forecasting.
