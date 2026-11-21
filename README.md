# claude-plugins

Claude Code plugins for Invisible Cadence projects: shared commands that check code quality, documentation quality and project rules in any repository.

Invisible Cadence is a personal project about using AI and automation to take some of the load out of everyday life. Its projects are built with AI coding agents and reviewed by one person who is learning the stack. This repository holds the tools that help with that review, so every project uses the same standards.

## What is here

One plugin so far.

### `review`

Two read-only reviews, each run in a fresh session so the reviewer is not the same session that wrote the code.

| Command | What it reviews | When to run it |
| --- | --- | --- |
| `/review:project` | The whole codebase: honesty (no fake code or weakened tests), tests, structure, repetition versus simplicity, error handling, security, maintainability, and the project's own rules | At the end of each roadmap phase, or when the code starts to feel tangled |
| `/review:docs` | The documentation: accuracy, one home for each fact, stale content, bloat, findability, the project's own rules, links | Now and then, such as every other phase, or when the docs start to feel heavy |

Both accept an optional focus, for example `/review:project worker` or `/review:docs README.md`.

Each review:

- runs the project's own checks before forming views
- checks the code or docs against that project's `AGENTS.md` (or `CLAUDE.md`), so the rules are not repeated here
- ranks findings as must fix, should fix or consider, each with a location, the principle behind it, a link to a source and a suggested fix
- changes nothing, and ends by asking which findings to act on

Reviews of a single pull request are not covered here, because Claude Code's built-in `/code-review`, `/simplify` and `/security-review` already do that well.

## Install

The marketplace is this repository, `invisible-cadence/claude-plugins`, and the plugin is `review`.

**On your claude.ai account (for cloud sessions and Claude Code Projects):** go to **Customize > Plugins** (https://claude.ai/customize/plugins), choose **Add > Add marketplace**, enter `invisible-cadence/claude-plugins`, then turn on `review`. See [Plugins](https://claude.com/docs/plugins/overview). Threads in a Project then have the commands.

**In Claude Code on your own computer:**

```
/plugin marketplace add invisible-cadence/claude-plugins
/plugin install review@invisible-cadence
```

See [Discover and install plugins](https://code.claude.com/docs/en/discover-plugins).

Declaring the plugin in a project's committed `.claude/settings.json` does not work for cloud sessions: they do not load plugins from repository settings ([Cloud environments: what carries over](https://code.claude.com/docs/en/cloud-environments)). That is why the account route is the one to use in the cloud.

## How it is built

A plugin marketplace is a git repository with a catalogue at `.claude-plugin/marketplace.json`. Each plugin has a manifest at `.claude-plugin/plugin.json`, and each folder under its `skills/` becomes a command named `/<plugin>:<folder>`. See [Plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces) and the [plugins reference](https://code.claude.com/docs/en/plugins-reference).

```
.claude-plugin/marketplace.json        the catalogue
plugins/review/.claude-plugin/plugin.json
plugins/review/skills/project/SKILL.md  /review:project
plugins/review/skills/docs/SKILL.md     /review:docs
```

A full review takes a while and uses a fair share of a plan's allowance, so it should run only when someone asks for one. Each command's description tells Claude to start it only when the project owner explicitly asks.

The commands do not set `disable-model-invocation: true`, although that would be the stricter guard. In a Claude Code Project, your message goes to a coordinator that starts the review in a new thread on your behalf. That setting counts the coordinator as Claude rather than a person, so it blocks the review and the thread asks you to type the command again.

To check the files after a change:

```
claude plugin validate .
claude plugin validate ./plugins/review
```

## Costs

None of its own. A review runs in a Claude Code session and counts against that plan's usage like any other session. Whole-project reviews are among the heavier tasks, which is one reason to run them at checkpoints rather than on every change.

## Limitations

- An AI review is a second opinion, not a safeguard. It can miss things and can be confidently wrong, so read each finding critically. Automatic checks (tests, linting, push protection) stay the real gates.
- The reviews depend on what each project's `AGENTS.md` says. A project with thin rules gets a more generic review.
- The two commands share their report format by copying it, not by referring to one file. Two copies are easier to read than an extra layer of indirection; if a third review is added, the format should move to one shared place.

## Licence

[MIT](LICENSE)
