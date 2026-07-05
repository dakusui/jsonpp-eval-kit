# Fresh Eyes — Task Brief

Thank you for helping evaluate **JSON++ / jq++**, a lightweight way to reduce
duplication in JSON/YAML configuration. Your experience will inform an IEEE
Software article, and you will be acknowledged in it (see consent at the end of
the questionnaire).

**Time:** about 60–90 minutes.
**You do not need prior JSON++ knowledge** — that is the point. We want to see
what a first-time user experiences.

---

## What you'll need

1. Install jq++ and skim the getting-started guide: see
   [`getting-started.md`](./getting-started.md).
2. The starter corpus: a small set of GitHub Actions workflow files, provided in
   [`corpus/`](./corpus/).

The provided corpus is the main task — please do that one. **Optionally**, if you
also have a configuration of your own that you are *allowed to share* (a personal
or open-source project, or something you can safely mask), trying jq++ on it too is
a welcome bonus — just tell us in the questionnaire. If you have nothing you can
share, don't worry: the provided corpus is all we need.

---

## The task

**Refactor the workflows to reduce duplication**, using JSON++[^constructs] so that
shared structure is expressed once and each file keeps only what makes it different.

Then **verify output equivalence**: confirm the generated output matches the
originals — the getting-started guide shows the exact command. A refactoring that
changes the output is not what we want.

That's it — refactor for reuse, and keep the output equivalent.

Work the way you normally would. **You may use AI assistance** (Claude, Copilot,
etc.) if that's how you usually work — just tell us whether and how in the
questionnaire.

There is no "right answer" and nothing is being graded. We are interested in what
felt natural, what was confusing, and where you got stuck.

---

## What to hand back

1. **Your whole working set** — the original files, your refactored JSON++ sources
   and shared bases, and the generated output (so we can confirm the output stayed
   equivalent and see the structure you created). The easiest way is to zip your
   working directory, or share a link to a repository/branch.
2. The completed **[questionnaire](./questionnaire.md)**.

Please fill in the questionnaire **right after** you finish, while it's fresh.

If you also tried **your own** configuration, only share it if you're permitted to,
and mask any secrets or proprietary values first — placeholders are completely
fine. If you can't share it, that's fine — the provided corpus is all we need.

Thank you — this genuinely helps.

[^constructs]: JSON++ adds a few reserved keys — mainly `$extends` for inheritance
    and evaluable expressions for computed values. The getting-started guide explains
    them; you don't need them memorised to start.
