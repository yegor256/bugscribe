---
name: submit-an-issue
description: |
  Use this skill to file a single, already-identified bug
  as a new GitHub issue against a specific repository —
  a defect, a missing feature, or any other finding the
  user or an earlier step has already named. Confirm the
  bug is not a duplicate, write a concise report that
  names the symptom, points to the code, and suggests a
  fix, and post one short follow-up comment pinging the
  repository owner — unless that owner is the same
  GitHub account running the skill, in which case skip
  the ping. One bug per run, one issue per run, at most
  one ping per run — then stop.
---

Operate on the GitHub repository named in the user's
  prompt as the target; refuse to run when no target is
  named.

Refuse to run when no concrete bug has been identified
  yet: this skill reports a finding handed in by the user
  or a previous step, and never searches the source tree
  for new defects on its own.

Clone or pull the repository's default branch into a
  local working directory before writing the report, so
  the file paths and line numbers in the issue match the
  latest committed state and not a stale snapshot.

Confirm the named defect against the source code: open
  the files the user named, read the surrounding context,
  and verify the symptom before writing the issue,
  because a report based on a misreading wastes the
  maintainer's time.

Do not run the build, do not execute the test suite, do
  not start any linter, and do not invoke any static
  analysis tool — this skill is a read-only inspection of
  the source code for verification purposes only.

Do not modify a single file in the repository, do not
  create branches, and do not open pull requests; the
  only writes this skill performs are the new issue and
  its follow-up comment on GitHub.

List every open issue in the repository (for example
  with
  `gh issue list --repo <owner>/<repo> --state open --limit 200 --json number,title,body,labels`)
  and skim each title and body so the handed-in defect
  can be checked against the existing backlog.

Discard the report entirely when it matches an
  already-open issue by topic, file, symptom, or proposed
  fix — a duplicate report wastes the maintainer's time
  and signals careless triage.

Search the closed issues too for the same symptom (for
  example with
  `gh issue list --repo <owner>/<repo> --state closed --search <keywords>`),
  because a defect already debated and rejected,
  wontfixed, or marked as working-as-intended is not
  worth re-filing.

Open the new issue with
  `gh issue create --repo <owner>/<repo> --title ... --body ...`
  using a short, declarative title that names the symptom
  and the location — for example
  `Parser drops trailing newline in foo.go` — and not a
  vague phrase like `Bug in parser`.

Write the body as a few short paragraphs of plain prose:
  one paragraph naming the bug and the file/line, one
  paragraph explaining why it is wrong, and one paragraph
  proposing a concrete fix.

Keep the body compact — a handful of sentences, not a
  wall of text — because maintainers read short bug
  reports and skim long ones.

Never use Markdown headings in the issue body or the
  follow-up comment — no `#`, `##`, `###`, or any other
  heading level — because the report is short prose, not
  a structured document with sections.

Talk like a human in the issue body and the follow-up
  comment: use your own words, write in plain
  conversational phrasing, and drop the stock AI cadence,
  boilerplate openings, and buzzword strings.

Do not add AI markers to the issue or the comment: no
  mention of Claude, ChatGPT, an LLM, or any model name;
  no `Generated with ...` footer, no `Co-Authored-By` AI
  trailer, no robot emoji, no disclosure that the text
  was written by an assistant.

Include a file path and an approximate line number for
  the offending code (for example
  `src/parser/lexer.go:142`) so the maintainer can jump
  straight to it without searching.

Suggest a fix in one or two sentences that names the
  change in concrete terms — which condition to flip,
  which branch to remove, which guard to add, which name
  to align — and stop there.

Do not propose a refactor, a rewrite, or a sweeping
  redesign as the fix; the suggestion must be the
  smallest change that resolves the reported defect.

Do not attach a patch, a diff, or a pull request to the
  issue itself, because the contract of this skill ends
  at the bug report and its follow-up comment.

Do not invent reproduction steps the source code does
  not support, do not fabricate stack traces, and do not
  claim to have run the program — this is a
  static-reading bug report and must read like one.

Identify the repository owner as the `owner` of the slug
  when it is a user account, or as the most active recent
  committer to the default branch when the owner is an
  organization (for example via
  `gh api repos/<owner>/<repo>/contributors` combined
  with `gh api repos/<owner>/<repo>/commits?since=...`).

After the issue is created, capture the new issue number
  from the `gh issue create` output and use it for the
  follow-up comment in the next step.

Skip the follow-up comment entirely when the identified
  recipient is the same GitHub account running the skill
  — compare the recipient's login against
  `gh api user --jq .login` and post nothing when the
  two match, because pinging yourself adds noise without
  reaching another maintainer.

Post one follow-up comment on the new issue (for example
  with
  `gh issue comment <number> --repo <owner>/<repo> --body ...`)
  that `@`-mentions the owner, asks them to take a look
  when they have a moment, and offers to clarify if
  anything in the report is unclear.

Keep the follow-up comment to one or two sentences of
  plain prose — no headings, no bullet lists, no emojis,
  no AI-disclosure boilerplate — because a ping is a
  ping, not a second report.

Do not ping more than one account in the follow-up
  comment, do not @-mention the whole organization, and
  do not request a deadline or a priority label.

Stop after the follow-up comment is posted: do not file
  a second issue, do not open a pull request, and do not
  start a fix — re-run this skill from the top for the
  next bug.
