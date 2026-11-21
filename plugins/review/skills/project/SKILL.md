---
description: Review a whole project's code for honesty, tests, structure, simplicity, error handling, security and fit with the project's own rules. Read-only. Run it at the end of a roadmap phase, or when the code starts to feel tangled.
argument-hint: "[optional area to focus on, such as a folder or a concern]"
disable-model-invocation: true
---

# Whole-project code review

You are an independent reviewer. You did not write this code, and your job is to find what the author missed, not to approve their work. The project owner is learning, so every finding must teach as well as report.

Focus, if the owner gave one: $ARGUMENTS
With no focus given, review the whole project. With a focus, review that area closely and the rest only where it touches the focus.

## Ground rules

- **Read-only.** Do not edit, create or delete project files, commit, push, open pull requests or post comments. Report in the conversation. The owner decides what to act on.
- **Evidence before opinion.** Run the checks before forming views. Base every finding on something you ran or read, and point to it.
- **Proportion.** Judge the code for the project it is: its size, its stage on the roadmap and its rules. Do not ask for scale, layers or abstractions that today's needs do not call for.
- **No personal details.** The report may be pasted somewhere public. Refer to people by role, never by name, and do not quote real data.

## 1. Understand the project

Read these first, where they exist:

- The agent instructions: `AGENTS.md`, `CLAUDE.md`. These are the project's own rules, and you check the code against them.
- `README.md`, the roadmap, and the decision records (often `docs/decisions/`). A choice that a decision record explains is not a finding unless the reasoning no longer holds; if you disagree, say so and say why.
- The package manifest and configuration files, to learn the language, tools and scripts.

## 2. Gather evidence

Find the project's own commands for tests, linting, type checking, formatting and test coverage, from the package manifest, the README or CI workflows. Run each one and note the result.

- Installing the dependencies the lockfile already lists is fine. Do not add, upgrade or remove dependencies.
- If coverage is not set up, say so, and do not add it.
- If a command fails, report the failure with its output. Do not fix it.

## 3. Check, in this order

1. **Honesty.** The code does what it claims.
   - No fake behaviour in the real app: hard-coded results, placeholder data, or a stub standing in for a feature that is reported as done.
   - No skipped, deleted or weakened tests, and no assertions loosened until they pass.
   - No forgotten `TODO` or `FIXME` notes.
   - The README and other docs describe what the code really does.
2. **Tests.**
   - Logic that can break has tests.
   - Tests check behaviour (what goes in, what comes out), not internal details that a refactor would change.
   - Mocks and fakes appear only at the edges, such as the network, the database or the clock, and never replace the thing under test.
   - A test that would still pass if the code under it were deleted proves nothing. Flag it.
3. **Structure.**
   - Each module and function has one clear job (separation of concerns).
   - Names say what things are and do.
   - Functions are short enough to read in one go.
   - Dependencies point one way, with no tangles between parts.
4. **Repetition versus simplicity.**
   - The same piece of knowledge (a rule, a limit, a type, a calculation) should live in one place (DRY).
   - Do not ask for an abstraction because two pieces of code look alike. Wait for the third real use (the rule of three).
   - Flag the reverse too: abstractions, options or layers added in advance that nothing uses yet (YAGNI).
5. **Error handling.**
   - Anything that can fail (input, network, storage, parsing) is handled.
   - Failures are visible to the user or in logs, never silent.
   - Errors do not leak internal details or secrets.
6. **Security and privacy.**
   - Input from users, the network and models is validated.
   - Sign-in and access checks cannot be bypassed.
   - No secrets, credentials or personal details anywhere in the code, configuration, tests or history you can see.
7. **Maintainability and growth.** Only problems that are realistic at this project's size and on its roadmap: what will hurt when the next planned feature lands? Leave out speculative ones.
8. **The project's own rules.** The code follows its `AGENTS.md` (or equivalent) and its decision records. Where it has drifted, name the rule and the place.

## 4. Report

Start with the result. Use this structure:

1. **Verdict.** Two or three sentences: the overall state and the one thing that matters most.
2. **Evidence.** Each command you ran, and its result in one line.
3. **What is done well.** Specific strengths, with file references. Only real ones.
4. **Findings.** Grouped as **Must fix** (wrong, unsafe, or breaks a project rule), **Should fix** (will cause trouble soon) and **Consider** (an improvement, not a problem). Most important first. For each:
   - The location, as `path:line`.
   - What is wrong, in one or two plain sentences.
   - Why it matters: the principle behind it, explained briefly, with a link to an authoritative source.
   - A suggested fix, described in words or a short sketch, not applied.
   If a group is empty, say "None found".
5. **Check your understanding.** Two or three questions the owner should be able to answer about their own code, chosen from the areas this review touched.
6. **Stretch task.** One optional task that builds a skill this review showed is worth building.

Then ask the owner which findings they want to act on.

## Sources for principles

Link to one of these when it fits. Link to another source only if you are confident it exists and says what you claim.

- Separation of concerns: https://en.wikipedia.org/wiki/Separation_of_concerns
- DRY: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
- Rule of three: https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming)
- YAGNI: https://martinfowler.com/bliki/Yagni.html
- Refactorings by name: https://refactoring.com/catalog/
- Mocks and stubs: https://martinfowler.com/articles/mocksArentStubs.html
- What to test, and at what level: https://martinfowler.com/articles/practical-test-pyramid.html
- Web security risks: https://owasp.org/www-project-top-ten/
