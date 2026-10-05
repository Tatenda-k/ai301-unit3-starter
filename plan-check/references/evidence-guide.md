# Evidence guide: where evidence lives in a plan package

A package has five parts, in this order: **Repo facts**, **Issue**,
**Thread highlights** (a subsection of Issue), **Repro evidence**, then
the **Candidate plan** and the **Candidate plan comment**. The repro
evidence is the ground truth. It is the one part that records what
actually happened on a machine, so the plan is graded against it, and
not the other way round. Anything the thread or the plan merely
*claims* (a "root cause identified above", "it seems like") is a claim
until the repro evidence supports it.

In live mode the same parts exist in different places: Issue and Thread
are the live GitHub issue and its comments; Repro evidence is the
student's own posted repro comment (or, on the house issue, the house
repro pack as the drafts quote it); Repo facts are the repo's issue
template, CONTRIBUTING.md and any AI policy; the plan and plan comment
are the student's drafts. Only what the drafts contain and quote counts
as the plan.

## Diagnosis and grounding

**Where it lives.**
- The plan's stated cause: the "Cause:" line or "Diagnosis" section of
  the Candidate plan. If the plan has no stated cause (only "poke
  around and find it"), that absence is the finding.
- What that cause must explain: the Repro evidence block's numbered
  steps, its **control** run (the same action with the suspect
  variable removed), and its **Actual** line. Controls and timings are
  the most decisive facts in the block; read them before the plan.
- Where the cause came from: Thread highlights. A cause borrowed from
  a commenter ("as identified in this thread") is a hypothesis, and the
  repro evidence is what confirms or kills it.
- Live: the issue thread, the student's posted repro comment, and
  maintainer comments naming a culprit file or function.

**What good looks like.** The stated cause makes a prediction that the
repro evidence already satisfies: every step, the control, and the
Actual line are consistent with it, and nothing in the evidence rules
it out. A diagnosis fails when a control or measurement in the repro
block contradicts it (for example the plan blames the pager's key
bindings while a repro step with no pager in the loop still shows the
slowdown), or when it targets a symptom the evidence shows is
downstream of the real cause. A diagnosis grounded in a maintainer's
analysis passes if that analysis matches the repro too. A plan that
names no cause and defers it to "figure out where it lives" is
ungrounded, not merely incomplete.

## Scope

**Where it lives.**
- The plan's in/out statement: "In: ... Out: ...", a "Scope" section,
  or a not-in-scope line. Also the plan's list of changes, since the
  real scope is what the steps touch, whatever the scope line says.
- The issue's title and Expected line: the size of the problem as the
  reporter stated it.
- Thread highlights: any maintainer note that a broader fix is hard,
  deferred, or already owned by another PR.
- The plan comment: does it repeat the same bounds, or promise more?

**What good looks like.** One change that fixes the behavior the
Repro evidence shows, with named files or call sites and an explicit
statement of what is left alone. A bounded plan can be small and
still be complete (a two-site clamp, one callback). Scope creep looks
like a fix bundled with a refactor, migration, redesign, new
abstraction, CI changes, or "while I'm in there" cleanups that the
repro evidence does not require. Another failure: a scope line that
says "minimal" while the steps list unrelated work, or a fix that
reaches into the area a maintainer said is hard without saying so.
Narrowing is fine and good when it is honest about what is deferred and
why.

## Executability

**Where it lives.** The Candidate plan's "Change(s)", "Approach", or
equivalent: the files or areas named, the mechanism of the fix, and
the order of work. Cross-check each named file or function against the
Issue and Repro evidence, where the culprit is often already located
(a path in the thread, a line in a log). Live: check that named paths
exist in the repo.

**What good looks like.** A stranger could open the repo and begin
without asking the author anything: at least one concrete location
(file, function, or call site), a concrete mechanism (what gets
added, changed or called), and no step that is really "investigate".
A plan that says it will look for where the code lives and decide the
approach later fails, however enthusiastic it is. Naming a plausible
file isn't enough if the evidence points somewhere else; that is a
grounding problem, graded under Diagnosis.

## Test plan

**Where it lives.** The "Test"/"Test plan" part of the Candidate plan,
read against the Repro evidence's **Steps**, **Control** and
**Expected**/**Actual** lines. Also check whether the plan comment
mentions the test.

**What good looks like.** The test is decisive: it names the
observable outcome that flips from broken to fixed, and it reuses the
repro's own steps or artifacts so a reviewer can see before/after on
the same case (re-run steps 1 to 3, expect the pushed color at step 3;
expect exit 0 on the failing command; three spellings of the path in a
fixture). Extra credit when it also checks the control or a sibling
path that shares the code. It fails when it names no outcome ("undo
works", "should feel fast") or when it is generic and would pass
without the fix ("run the full test suite and make sure nothing
regresses"). That doesn't prove the reported behavior is gone.

## Honesty

**Where it lives.** Wherever the plan or comment states certainty or
uncertainty: risks, "unknown", "to verify", "I assume", "I'd present
this as opt-in" language in the Candidate plan, and the confidence
level in the plan comment ("I traced this to...", "reproduced on...").
Compare claims against the Repro evidence: versions, what was actually
run, what was and wasn't tested. A mid-build deviation belongs in an
updated plan.md (live mode), not just in the diff.

**What good looks like.** Claims are no stronger than their backing.
Unknowns the plan cannot resolve from the package are named as
unknowns with a way to check them, or as decisions left to the
maintainers; they are not dressed as facts. False confidence looks like
"I traced this to X" when the package only shows someone else's claim,
a diagnosis stated as settled that the control run contradicts, or a
comment claiming a test or reproduction the evidence block does not
contain. Hedging everywhere is not honesty either: the plan should be
decisive on what the evidence does establish.

## Comms

**Where it lives.**
- The Candidate plan comment, read against **Thread highlights**
  (maintainer direction, requests for testing, mentions of prior or
  open PRs and who owns the fix) and the **Repo facts** block (issue
  template fields, contribution policy, review-bandwidth notes, and any
  AI-use or AI-comment rule).
- Live: the whole thread, open PRs linking the issue, CONTRIBUTING.md,
  and AI_POLICY.md.

**What good looks like.** The comment shows it was written for this
thread: it responds to the specific maintainer signals present (a
stated direction, a requested test, a warning that the deep fix is
hard, an open competing PR) and honors the repo's stated rules. When
the policy requires disclosure of AI use or human-written comments,
the comment contains that disclosure or is plainly in the author's
own words, as the policy asks. It states what is being proposed and
what version was reproduced, in a few plain sentences. It fails by
ignoring explicit maintainer direction, racing an existing PR without
mentioning it, omitting a required disclosure, or being boilerplate
that could be pasted on any issue ("I'll fix this, wish me luck!").
Tone and polish don't matter; engagement with the thread and
compliance with the repo's stated asks do.
