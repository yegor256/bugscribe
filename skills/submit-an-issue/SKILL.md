---
name: submit-an-issue
description: |
  Use this skill to file one already-identified bug
  as GitHub issue against one specific repository.
---

## Target

Target GitHub repository named by user.
Refuse when no concrete bug has been handed in.

## Research

Clone or pull default branch before writing report.
Verify symptom against source code before writing.

## Boundaries

Do not run build, tests, linters, or static analysis.
Do not modify files, create branches, or open pull requests.

## Duplicates

Check open issues for duplicate before filing.
Discard report when it matches already-open issue.
Check closed issues too for same symptom.

## Title

Use short declarative title naming symptom and location.

## Body

Write body as few short paragraphs.
Cover bug, why it is wrong, and proposed fix.
Read `examples/` directory and mirror its title shape, structure, and tone.
Keep body compact.
Never use Markdown headings in body or comment.

## Voice

Write like human.
Avoid AI cadence, boilerplate openings, and buzzword strings.
Never add `Generated with` footers or `Co-Authored-By` AI trailers.
Never add robot emoji.

## Evidence

Include file path and approximate line number for offending code.
Quote offending code as snippet whenever source is available.
Let snippet show defect, since code beats prose.

## Fix

Suggest concrete fix in one or two sentences.
Do not propose refactors, rewrites, or sweeping redesigns.
Do not attach patches, diffs, or pull requests to issue.
Do not invent reproduction steps or fabricate stack traces.
Do not claim to have run program.

## Label

Attach `bug` label to issue when account can label issues.
Skip label when account lacks that permission.

## Owner

Read `.github/CODEOWNERS` to find repository owner.
Take account from global `*` entry as repository owner.
Fall back to slug owner when `.github/CODEOWNERS` is absent.
For organizations, treat top recent committer as owner.
Identify authenticated account before deciding on follow-up comment.

## Comment

When owner is authenticated account, file issue and stop.
Never post follow-up comment to yourself.
Never `@`-mention authenticated account.
When owner is someone else, `@`-mention owner in one follow-up comment.
Offer to clarify in that comment.
Keep comment to one or two sentences.
Ping one account and never request deadline.
Stop after follow-up comment.
