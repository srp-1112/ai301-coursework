# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| allow_ai | The `CONTRIBUTING.md` file text. | The file does not explicitly ban the use of AI-generated code or LLM tools. | Required |
| issue_unassigned | The issue `assignee` field and the comment thread text. | The issue `assignee` field is null/empty AND no comments contain text variants of "I'm working on this" or "can I take this". No linked PRs. | Required |
| maintained_active | The last default-branch commit dates and the repository's archived status flag. | The most recent default-branch commit is within the last 60 days AND the repository archived status is false. Human authored PRs have been merged in last 60 days. | Required |
| clear_scope | The issue description body text and the comments. | The issue description contains a "Steps to Reproduce" OR "Expected Behavior" OR has clear outcome. Estimated lines of code change is less than 10. | Preferred |
| good_first_issue_label | The issue `labels` list. | The labels list contains at least one of the following: "good first issue", "good-first-issue", "first-issue", or "help wanted". | Preferred |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->


- Evaluate checks in order. 
- Reject the issue immediately if any single `Required` check fails or evaluates to `unclear`; there is no need to evaluate remaining checks after a failure.
- Accept the issue only if all `Required` checks pass successfully.
- `Preferred` checks do not alter the binary accept/reject verdict; they are used solely to rank accepted issues after they pass.
