# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

https://github.com/LegalQuants/lq-ai/issues/490

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
{
  "rubric": "/home/sande/.claude/skills/issue-select/skill/rubric.md",
  "model": "sonnet",
  "agreement": [
    1,
    1
  ],
  "results": [
    {
      "id": "issue-14",
      "verdict": "accept",
      "failed_checks": [],
      "checks": [
        {
          "name": "allow_ai",
          "grade": "pass",
          "evidence": "contribution policy (CONTRIBUTING.md): no statement on AI or contribution tooling"
        },
        {
          "name": "issue_unassigned",
          "grade": "pass",
          "evidence": "this issue: assignees: none; linked PRs: none; Comments (0 total)"
        },
        {
          "name": "maintained_active",
          "grade": "pass",
          "evidence": "last push 2026-08-05, archived: no; last 5 default-branch commits (2026-08-01 to 2026-08-05) are human-authored merged PRs"
        },
        {
          "name": "clear_scope",
          "grade": "pass",
          "evidence": "issue lists exact 6 files, exact lines/text to change, and a grep-based verification step; estimated ~8 lines changed total"
        },
        {
          "name": "good_first_issue_label",
          "grade": "pass",
          "evidence": "labels: documentation, good first issue"
        }
      ],
      "error": null
    }
  ]
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

I took another 5 issues to test individually as I iterated over and tuned the rubrics. I also iterated over the 4 calibaration issues. I ran against all issues only once after my final update to rubrics.

All updates were done locally. So there is just one commit.

I realize I could have started with the calibrations ones  and then used the issues as test samples (took some time to figure out how to run calibration issues only).

Pivots:
- clear_scope too strict with AND criterias. Modified to OR. 
- There is barely any information in the issue itself. The expectation might be whoever picks of the story is familiar with the repo and the application. Assuming false positive in gold labels for now.
- checks not considering the complexity of solution. Also realized hard to know what criteria was used to accept or reject. Updated eval.py code to note each rubric check and outcome and the reason.
- Added check to estimate max lines of code for potential solution.

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

```bash
sande@sandeeppc:~/codepath/ai301-unit1-starter$ python3 eval/run_eval.py --rubric /home/sande/.claude/skills/issue-select/skill/rubric.md --only issue-14 --out issue-14-verdict.json
grading 1 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-14: accept

item      gold    verdict  agree  note
issue-14  accept  accept   yes    

allow_ai: pass — contribution policy (CONTRIBUTING.md): no statement on AI or contribution tooling; 
issue_unassigned: pass — this issue: assignees: none; linked PRs: none; Comments (0 total); 
maintained_active: pass — last push 2026-08-05, archived: no; last 5 default-branch commits (2026-08-01 to 2026-08-05) are human-authored merged PRs; 
clear_scope: pass — issue lists exact 6 files, exact lines/text to change, and a grep-based verification step; estimated ~8 lines changed total; good_first_issue_label (preferred): pass — labels: documentation, good first issue

agreement: 1/1 scored items
full results written to issue-14-verdict.json
```


**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| clear_scope | The issue description body text and the comments. | The issue description contains a "Steps to Reproduce" OR "Expected Behavior" OR has clear outcome. Estimated lines of code change is less than 10. | Required |

First good issue should have clarity, ideally documented, but it is also ok if it can be easily inferred. Outcome needs to be clear. Its good if it has steps to reproduce, possible implementtaion etc. Most importantly it should be scoped to a relatively small task. It should not involve multiple files. 

Because of the complexity requirement, only 2 of the 8 accepted issues matched from the gold labels.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

It will miss issues with little description even though it may be clear (esp, if issue assumes someone will look at the repo and what it does before looking at issue, so even little context would be sufficient).
It might also accept issues as first good issues, even if it contains headers terms it is looking for but information is not complete.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
It is a documentation task, so it is doable. I am not sure if it fits what we are trying to do in the classroom.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
   AI not banned, issue not assigned, pr not linked, repo maintained and active were identified correctly. Clarity and scope was non-deterministic and affected the verdict significantly with small changes to the wording. Ex. Or vs And, add or remove key words.
3. The anticipated difficulty in claiming it.
   Documentation itself should be easy to do.

]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`; `history.md` in this directory on how I got to the run in eval-run.txt, 
updated `run_eval.py` to print reasoning behind the verdict.
