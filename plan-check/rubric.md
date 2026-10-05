# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis grounded | The plan's stated cause, read against the repro evidence block's steps and actual-vs-expected result. | Pass if the cause explains the specific behavior the repro evidence shows (the step where it goes wrong and the observed result) and contradicts nothing in it. Fail if the cause ignores, contradicts, or is unrelated to what the repro shows, or if the plan states no cause. Unclear if the cause could be true but the repro evidence is too thin to tell. | required |
| Cause, not symptom | The plan's change read against its stated cause and the repro evidence. | Pass if the change acts where the cause is (so that, once made, the repro's wrong behavior cannot happen), not merely where the symptom shows up. Fail if the change hides, special-cases, or papers over the symptom while the evidence points at a different underlying cause. | required |
| One bounded change | The plan's in-scope and not-in-scope statements, and the files or areas it names, read against the issue's ask. | Pass if the plan is one change that fixes the reported issue and names what it will not touch. Fail if it bundles unrelated fixes, refactors, or renames, or names no limit so the change could grow without end. | required |
| Stranger could start | The plan's named files or areas, approach, and order of work. | Pass if someone who has never seen the issue could open a named file or area and begin the work without asking the author anything. Fail if the location or approach is left vague ("fix the handler", "update the logic") or depends on knowledge only the author has. | required |
| Test proves the fix | The plan's test plan read against the repro evidence's steps and artifacts. | Pass if the test plan reruns the repro's own steps (or an equivalent) and names an observable result that differs before and after the fix. Fail if it only says "verify it works", checks something the bug never touched, or has no observable outcome. | required |
| Unknowns stated honestly | The plan's risks, unknowns and assumptions, read against what the repro evidence and repo-facts block actually establish. | Pass if anything the evidence does not settle (an unconfirmed cause, an untested platform, an untried edge case) is named as unknown or as a risk, and no claim goes beyond the evidence. Fail if the plan or comment asserts certainty the evidence does not support (for example, "root cause confirmed" with no repro step showing it). | required |
| Comment fits the thread and repo | The plan comment read against the thread highlights and the repo-facts block (templates, contributing asks, contribution policy, AI-use disclosure). | Pass if the comment honors every ask in the thread and the repo facts that applies to a plan comment, including any stated AI disclosure or contribution-policy requirement, and says what the plan does in this issue's own terms. Fail if it ignores a maintainer's request, breaks a stated repo rule, or is boilerplate that could be pasted on any issue. | required |
| Comment matches plan | The plan comment read against the candidate plan. | Pass if the comment states the same cause, change and test as the plan, with nothing added or dropped. Fail if the comment promises something the plan does not contain or contradicts it. | preferred |

## Verdict rule

Accept if every `required` check passes; otherwise reject. A `fail` on
any required check rejects. An `unclear` on a required check also
rejects: a plan that cannot be verified from the package is not ready
to build from, so `unclear` counts as `fail`. `preferred` checks are
reported but never change the verdict.
