---
name: grill-me
description: Relentlessly interviews you one question at a time to extract what's in your head into a durable, searchable capture file. Activates on "grill me", "grill me about <X>", "stress-test this plan", "pressure-test my thinking on <X>", "interview me about <X>", "drill me on <X>", "get this out of my head", "discovery session on <X>", "I need to think through <X> properly", or any request to externalize a process, plan, decision, or mental model. Walks each branch of the decision tree, gives a recommended answer with every question, and CHECKPOINTS every answer to a markdown file on disk so nothing is lost as the context window fills. NOT a content generator — it extracts, it doesn't write deliverables.
argument-hint: "[topic, plan, or decision to be grilled on]"
---

# Grill Me

You want something out of your head and into a durable system. Interview the user relentlessly about every branch of the topic until you reach genuine shared understanding. The real job is **extraction** — turning what only lives in someone's head into durable, reusable, retrievable context. A five-minute brain-dump is never enough; the questions are how you get the rest.

## The capture file is the whole point

A long interview fills the context window. If answers live only in your head, you will eventually misremember, conflate, or drop one. So you **checkpoint to disk after every single answer**. The file on disk — not your conversation memory — is the source of truth. Never make the user ask you to save progress; it's automatic and constant.

There are TWO distinct "checkpoints" in this skill. Do not conflate them:

1. **Capture-file write** — appending each answer to the markdown file. A cheap local write. Happens after **EVERY single answer**, always. This is the anti-context-loss guarantee.
2. **Ingest / indexing** — making the file searchable in whatever retrieval layer you use (a vector DB, a notes index, etc.). Heavier. Happens **once at session close**, or when the user explicitly says "ingest what we have." Never on a timer, never on a self-counted cadence (you are unreliable at both). The on-disk file is the safety net the whole time; searchability just lands at the end.

## When this runs

The user says one of: "grill me", "grill me about <X>", "stress-test this plan", "pressure-test my thinking on <X>", "interview me about <X>", "drill me on <X>", "get this out of my head", "discovery session on <X>", "I need to think through <X> properly". Or any moment they clearly want to externalize a process / plan / decision / mental model rather than have you produce a deliverable.

## When NOT to run this skill

- **A single thing to save right now.** If the user just wants to persist one paste or insight, that's a quick capture, not a whole interview.
- **They want a deliverable written** (copy, a doc, a post). This skill extracts thinking; it does not produce finished artifacts. Hand off to whatever writing workflow you use.

grill-me is for when there's a body of knowledge in someone's head and the way to get it out is sustained, structured questioning.

## Setup — do this BEFORE the first question

### 1. Resolve the capture path

Pick a sensible location and filename for the notes file, e.g. `notes/YYYY-MM-DD-<topic>-grill.md`. Get today's date with `date +%F`.

### 2. Create the file immediately

Write the header before asking anything (see structure below): title, date, the one-line goal of the session, and empty "Summary" + "Open flags" sections. Tell the user the path in ONE line ("Capturing to `<path>` as we go."). Then ask Q1.

## The checkpoint rule (non-negotiable)

After EVERY answer, BEFORE you ask the next question:

- Append a structured entry to the capture file: the question topic, the key facts and decisions from their answer (**in their own words where the wording matters** — don't paraphrase their exact phrasing into something cleaner), and any flags (things they couldn't answer + who owns them).
- Update or correct earlier entries if a later answer changes them. Keep the running "Summary / key decisions" synthesis current.
- ONLY then ask the next question.

Never batch multiple answers into one write. One answer, one write. The point is that if context is lost at any moment, the file already holds everything said so far.

## Interview method

- Ask **one question at a time.** For each, provide your **recommended answer** — your best inference from context — so the user can simply confirm, correct, or redirect. (This is faster for them and surfaces where your model is wrong.)
- Resolve dependencies in order: settle the upstream decision before the ones that depend on it. Walk each branch of the tree to its end before moving to the next.
- If a question can be answered by **reading the codebase, your notes, or a doc the user hands you** — do that instead of asking. Only surface what's net-new. Don't make the user tell you something the system already knows.
- When the user **can't answer** something, capture it as a flag with the right owner (a teammate, a system to check, a doc to pull) and move on. Don't stall on a gap.
- Keep going until the user says you're done, or you've covered every branch. Near the end, offer a completeness backstop: "Anything we haven't touched that should be in here?"

## Capture file structure

```markdown
# {Topic}: Grill / Discovery Notes
Date: {YYYY-MM-DD} · Goal: {one line}

## Summary / key decisions
(running synthesis, updated as you go — the TL;DR of everything settled so far)

## Q&A log

### Q1 — {topic}
- Asked: {the question}
- Captured: {facts, decisions, the user's words verbatim where it matters}
- Flags: {open item -> owner}

### Q2 — {topic}
...

## Open flags (pending input)
- {item} -> {who/what can answer}
```

## At the end — reconcile, then graduate

1. **Reconcile.** Do a final read of the capture file for contradictions or gaps and fix them inline. Make the "Summary / key decisions" section a clean standalone TL;DR.

2. **Make it searchable.** Ingest or index the file into whatever retrieval layer you use, so it's findable later. If that step fails, say so — don't pretend it worked.

3. **Propose graduating the insights.** The capture file is raw extraction. Now offer to graduate what's reusable into curated layers — but PROPOSE, don't auto-edit:
   - **A curated knowledge page** — a concept, decision, or analysis doc that distills what was extracted.
   - **A persistent context/instructions file** — if the grill changed the standing picture of a project.
   - **An existing skill or tool** — if the grill surfaced nuance a skill is missing. Propose the edit; don't silently rewrite a skill from here.
   - **A preference/rule** the user stated → a durable memory of that rule.

4. **Recap** in a few lines: what's captured (+ path), what's still flagged, and the single suggested next step.

## Why this skill exists

The hardest part of building a good operating system is extraction — getting what's in your head into the system as reusable context, so every downstream answer is sharper. Spending the time up front to grill thoroughly is the axe-sharpening: it gets a skill, a plan, or a strategy to 90% on the first pass instead of crawling there over ten iterations. The capture file makes that extraction durable; the indexing makes it retrievable; the graduation step makes it compound.
