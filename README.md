# Bugscribe

[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/yegor256/bugscribe/blob/master/LICENSES/MIT.txt)

A single Claude Code skill that reports an already-identified bug
  as a new GitHub issue — it does not search the source code for
  defects; it files the one handed in by the user or an earlier
  step.

The bundle ships exactly one skill:

* [`submit-an-issue`](skills/submit-an-issue/SKILL.md)
  — verify a handed-in defect against the source code, check the
    backlog for duplicates, post a short report pointing to a file
    and line, and ping the repository owner exactly once.

Suppose you work with [Claude Code].
You do not need to clone this repository — install the bundle as a
  plugin straight from GitHub.
Inside a Claude Code session, run:

```text
/plugin marketplace add yegor256/plugins
/plugin install bugscribe@yegor256
```

The first command registers the [yegor256/plugins] marketplace,
  which lists every plugin maintained under the `yegor256` account;
  the second installs the `bugscribe` plugin from it,
  which exposes the `submit-an-issue` skill to your sessions
  automatically.

To update later, run `/plugin marketplace update yegor256`;
  to remove, run `/plugin uninstall bugscribe@yegor256`.

[yegor256/plugins]: https://github.com/yegor256/plugins

[Claude Code]: https://code.claude.com/docs/en/skills
