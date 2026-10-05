# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. In live mode, read `scope.md` first. If the issue is outside the
   scoped repo, or the Repo line is still a placeholder, stop without
   grading. In eval mode, skip this step.
2. Read `rubric.md` and `references/evidence-guide.md`. List every
   check name and the verdict rule, so you know what evidence to look
   for while reading, and use the guide's map to find it.
3. Read the issue context (and, in eval mode, the repo-facts block).
   Write down, in one line each: what the issue reports, any maintainer
   asks in the thread, and any repo rules (templates, contribution
   policy, AI-use disclosure).
4. Read the repro evidence before the plan. Write down: the steps, the
   step where the behavior goes wrong, the observed result, and the
   expected result. The plan is judged against this, so read it first
   so it cannot colour your reading of the plan.
5. Read the candidate plan. Write down: its stated cause, its change,
   its in-scope and not-in-scope lines, the files or areas it names,
   its test plan, and any risks or unknowns it states.
6. Read the candidate plan comment last. Write down what cause, change
   and test it claims, and what it says to the thread.
7. Do not grade anything until all of steps 1-6 are done.

## Evidence gathering

1. Diagnosis grounded: take the plan's stated cause (step 5) and the
   repro evidence's failing step and observed result (step 4). Record
   both as quotes. If the plan states no cause, record "no cause stated".
2. Cause, not symptom: take the plan's change and its stated cause.
   Record where the change acts (file, function, or behavior) and
   whether that is where the cause lives or only where the symptom shows.
3. One bounded change: record the plan's in-scope and not-in-scope
   lines verbatim, and list every distinct change the plan proposes.
   If there is no not-in-scope line, record "no limit stated".
4. Stranger could start: record the first file or area the plan names
   and the approach it gives. Ask whether you could open that place and
   begin without asking the author; record the quote that decides it.
5. Test proves the fix: record the plan's test plan verbatim, and the
   repro steps it should map to. Record the observable result it names
   (or "none named") and whether that result would differ before and
   after the fix.
6. Unknowns stated honestly: record every risk or unknown the plan or
   comment states, and every claim of certainty ("confirmed", "root
   cause", "will fix"). For each certainty claim, record the repro
   fact that supports it, or "unsupported".
7. Comment fits the thread and repo: record each thread ask and repo
   rule from Read order step 3 that applies to a plan comment, and
   whether the comment honors it (quote the line, or "not addressed").
   Record whether the comment names this issue's own specifics.
8. Comment matches plan: record the cause, change and test in the
   comment next to those in the plan, and note any difference.
9. In live mode only, gather issue-side facts with `gh` or the web
   (the thread, the repo's contributing docs). In eval mode, use only
   the bundle text and fetch nothing.

## Check execution

1. Execute the checks in the order the rubric lists them. Grade each
   one from the evidence recorded for it in Evidence gathering; do not
   re-read the whole package unless a recorded fact is missing.
2. Apply the rubric's pass condition exactly as written. Do not add
   your own standards, and do not judge length, headings or polish.
3. Grade `pass` when the evidence meets the pass condition and `fail`
   when it meets the fail condition.
4. Grade `unclear` only when the evidence the check needs is genuinely
   absent from the package after you looked (for example, the repro
   evidence is too thin to tell whether the cause fits). A missing item
   the check requires, such as no stated cause, no test plan, or no
   not-in-scope line, is a `fail`, not `unclear`.
5. For every grade, write one line naming the fact or quote that
   decided it. A grade with no evidence line is not finished.
6. If a step in this procedure is silent on something you had to
   decide, say so in the summary rather than inventing a rule.
7. In live mode, after the checks, hold the plan comment against
   `voice-guide.md` and note any broken rule in the summary. This
   never changes a grade or the verdict.

## Verdict assembly

1. List the grade of each required check, then each preferred check.
2. Apply the rubric's verdict rule: `accept` only if every required
   check is `pass`. Any required `fail` gives `reject`. Any required
   `unclear` also gives `reject`, because the rule counts `unclear` as
   `fail`. Preferred checks never change the verdict.
3. If the verdict is `reject`, name the first required check (in table
   order) that did not pass and quote its deciding evidence in the
   summary. If the verdict is `accept`, quote the evidence line of the
   check that came closest to failing.
4. Emit the summary, then the fenced JSON block from SKILL.md with one
   entry per check and the verdict as its last field. The JSON block
   must be last in the output.
