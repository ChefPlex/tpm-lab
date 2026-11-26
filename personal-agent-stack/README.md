# A Personal Agent Stack, Run Like a Program

**Status:** 🟢 Live, in daily use. The statuses below were derived on **2026-11-26** from the system itself, not edited by hand.

**The question:** you give an AI agent your mail, calendar, files and tools. How do you run it like a program, so you know at any moment what is working, what is only on paper, and what can stop it?

A personal AI agent system on one Mac mini, with Claude Code at the center. I run it the way I would run any program: a clear request path, guardrails that can stop a step, deterministic code for anything that must come out the same twice, and a status for every part that is derived from the system, not typed by hand.

---

## How a Status Is Decided

| Status | Meaning | How it is derived |
|:---|:---|:---|
| LIVE | Wired in and working | Registered and ran clean, or used in the last 30 days |
| MIXED | Wired in, but the last run failed or it is not connected | Last exit code, or connection state |
| PILOT | Built, not in use | Exists, but nothing registered or invoked it in 30 days |
| RULE | Text only, no mechanism | The instruction says nothing enforces it |
| Not tracked | No check yet | Named honestly instead of assumed |

The point: a control that is documented and believed live can be doing nothing. A derived status catches that; a hand-typed one hides it.

---

## The Request Path

Every request runs left to right: door, brain, guardrail check, tool or script, store, output.

| Stage | Part | Status |
|:---|:---|:---|
| 1. Doors in | Terminal (Claude Code) | not tracked |
| | Voice, "Hey Frank" (local speech-to-text and voice) | LIVE |
| | Remote messages, from my own devices only | LIVE |
| | Scheduled jobs (30) | 30 LIVE |
| | Browser, for sites with no API | not tracked |
| 2. Brain | Standing instructions + 9 rules files | 3 RULE (the hand-listed instruction-only rules) |
| | Skills (55) | 33 PILOT, 22 LIVE |
| | Specialist agents (8) | not tracked |
| | Memory, with a handoff between sessions | not tracked |
| 3. Guardrails | Hooks (17), each registered and run on an empty input | 2 PILOT, 15 LIVE |
| | Human gate: sends, deletions and public pushes wait for me | LIVE |
| | Untrusted input: mail and web text is treated as data, never as instructions | not tracked |
| 4. Tools | Connectors (MCP servers, 36) | 4 MIXED, 32 LIVE |
| 5. Outputs | Email drafts, staged and never sent | LIVE |
| | Briefings: morning, end of day, weekly | LIVE |
| | Published pages | LIVE |

**Underneath:** deterministic scripts, each with a test, run by a full suite in the background; SQLite stores (35 tables in the main one) for jobs, people, tasks and the improvement backlog; nightly backups (LIVE).

---

## What Running It Like a Program Means Here

1. **One authority per question.** A register says which file decides which question, so the most recently read file is never treated as current fact.
2. **Guardrails in code, not in prose.** A rule broken twice gets a mechanism. The table above shows which rules still have none.
3. **The human decides.** The agent advises and drafts; sends, deletions and public pushes are mine.
4. **Retrieved text is data.** An instruction found inside an email or a web page is a finding to report, never a step to take.

---

*Derived 2026-11-26 from the system's own status sweep. Examples are from my own setup; nothing here describes an employer's systems.*
