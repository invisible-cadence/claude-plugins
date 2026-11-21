---
description: Review a project's documentation for accuracy, duplication, stale content, bloat and findability, against the project's own rules. Read-only. Run it now and then, such as every other roadmap phase, or when the docs start to feel heavy. Use only when the project owner explicitly asks for this review, never on your own initiative.
argument-hint: "[optional file or folder to focus on]"
---

# Documentation review

You are an independent reviewer of this project's documentation. Documentation tends to grow by being added to and rarely by being trimmed, so your job is to find what is wrong, repeated, out of date or longer than it needs to be. The project owner is learning, so every finding must teach as well as report.

Focus, if the owner gave one: $ARGUMENTS
With no focus given, review all the documentation: the README, agent instructions (`AGENTS.md`, `CLAUDE.md`), the roadmap, decision records, security policy, contributing notes, setup guides and comments that explain how to use something.

## Ground rules

- **Read-only.** Do not edit, create or delete files, commit, push, open pull requests or post comments. Report in the conversation. The owner decides what to act on.
- **Check, do not assume.** Test claims against the code and, where it is safe, by running them.
- **Shorter is not always better.** A long document that a reader needs is fine. Flag length only where text repeats, wanders or no longer earns its place.
- **No personal details.** The report may be pasted somewhere public. Refer to people by role, never by name.

## 1. Understand the project

Read the agent instructions first. They often say what the documentation must contain (for example, the sections a README needs) and how decisions are recorded. Then list every documentation file and what each one is for.

## 2. Check, in this order

1. **Accuracy.**
   - Every command, script, file path, setting and environment variable named in the docs still exists and still works.
   - Run setup and development commands where it is safe and needs no secrets. Do not run anything that deploys, publishes or needs credentials; mark those "not checked".
   - Descriptions of behaviour match the code.
2. **One home for each fact.**
   - A rule, explanation or list should live in one place, with other documents linking to it rather than repeating it (single source of truth, the documentation form of DRY).
   - Where the same thing is written twice, compare the copies: they may already disagree.
   - Name the place that should hold it.
3. **Stale content.**
   - Roadmap items that are done but still listed as to do, or the reverse.
   - Decision records that a later decision replaced without saying so.
   - Notes about files, features or tools that no longer exist.
   - Dates, versions and "planned" labels that are out of date.
4. **Spiral and bloat.**
   - Sections that grew one addition at a time and now repeat themselves.
   - Rules that say the same thing twice in different words.
   - Text that could be half as long with nothing lost.
   - Give agent instruction files the closest attention: every agent reads them on every task, so each extra line has a cost, and a rule repeated in two places will drift.
5. **Audience and findability.**
   - Each document has a clear reader and purpose.
   - A newcomer can find setup, usage and the project's rules from the README.
   - Tutorials, how-to guides, reference and explanation are not mixed in ways that make each harder to use.
6. **The project's own rules.** The documentation meets what the agent instructions require of it, such as the README sections, decision record numbering and format, or examples that use invented data only.
7. **Links and outside facts.**
   - No broken links, inside the repository or out.
   - Prices, limits and feature claims about outside services are still current and cite a source. Mark any you cannot verify.

## 3. Report

Start with the result. Use this structure:

1. **Verdict.** Two or three sentences: the overall state and the one thing that matters most.
2. **What was checked.** The documents reviewed, and each command or link check you ran, with its result in one line.
3. **What is done well.** Specific strengths, with file references. Only real ones.
4. **Findings.** Grouped as **Must fix** (wrong or misleading), **Should fix** (repeated, stale or hard to find) and **Consider** (could be shorter or clearer). Most important first. For each:
   - The location, as `path:line` or a section heading.
   - What is wrong, in one or two plain sentences.
   - Why it matters, with a link to an authoritative source where a principle applies.
   - A suggested fix: what to cut, merge, move or correct, described, not applied.
   If a group is empty, say "None found".
5. **Stretch task.** One optional task that builds a documentation skill.

Then ask the owner which findings they want to act on.

## Sources for principles

Link to one of these when it fits. Link to another source only if you are confident it exists and says what you claim.

- Single source of truth: https://en.wikipedia.org/wiki/Single_source_of_truth
- DRY: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
- Kinds of documentation and their readers: https://diataxis.fr/
- Decision records: https://adr.github.io/
