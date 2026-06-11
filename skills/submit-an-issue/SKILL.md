---
name: submit-an-issue
description: |
  Use this skill to file an already-identified bug
  as a GitHub issue against a specific repository.
---

Target the GitHub repository the user named.
Refuse when no concrete bug has been handed in.
Clone or pull the default branch before writing the report.
Verify the symptom against the source code before writing.
Do not run the build, tests, linters, or static analysis.
Do not modify files, create branches, or open pull requests.
Check the open issues for a duplicate before filing.
Discard the report when it matches an already-open issue.
Check the closed issues too for the same symptom.
Use a short, declarative title naming the symptom and the location.
Write the body as a few short paragraphs.
Cover the bug, why it is wrong, and a proposed fix.
Read the `examples/` directory and mirror its title shape, structure, and tone.
Keep the body compact.
Never use Markdown headings in the body or the comment.
Write like a human.
Avoid AI cadence, boilerplate openings, and buzzword strings.
Never add `Generated with` footers or `Co-Authored-By` AI trailers.
Never add robot emoji.
Include a file path and an approximate line number for the offending code.
Quote the offending code as a snippet whenever the source is available.
Let the snippet show the defect, since code beats prose.
Suggest a concrete fix in one or two sentences.
Do not propose refactors, rewrites, or sweeping redesigns.
Do not attach patches, diffs, or pull requests to the issue.
Do not invent reproduction steps or fabricate stack traces.
Do not claim to have run the program.
Attach the `bug` label to the issue when the account can label issues.
Skip the label when the account lacks that permission.
The owner is the slug owner, or the top recent committer for an organization.
Identify the authenticated account before deciding on a follow-up comment.
When the owner is the authenticated account, file the issue and stop.
Never post a follow-up comment to yourself.
Never `@`-mention the authenticated account.
When the owner is someone else, `@`-mention the owner in one follow-up comment.
Offer to clarify in that comment.
Keep the comment to one or two sentences.
Ping one account and never request a deadline.
Stop after the follow-up comment.
