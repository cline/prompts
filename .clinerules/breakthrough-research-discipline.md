# Research experiment discipline (breakthrough loop)

Rules for projects where Cline runs experiment campaigns: keeps the
numbers honest before they become claims. Full methodology:
https://github.com/GuoCheng24/breakthrough-harness

### Scope
These rules govern experiment campaigns and any sentence that reports a
number. Routine code changes, refactors and infrastructure work are exempt.

### Target triage (before any experiment campaign)
Confirm all four, or say which one fails and stop:
1. a cheap scoring function exists (seconds-minutes, unambiguous, machine-run);
2. the groundwork exists (data downloadable, baselines published);
3. a win is externally recognisable (leaderboard, or referee-grade controlled
   comparison);
4. the oracle ceiling and a trivial/random baseline leave a gap worth mining -
   measure both BEFORE round 1, not at round 10.

### Harness before methods
- One evaluation entry point; ground truth stays inside the harness.
  Tier the scoring: Tier 0 sanity in seconds, Tier 1 selection in minutes,
  Tier 2 confirmation at full budget. When Tier 1 is genuinely hours (e.g.
  training runs), use a cheaper proxy only after showing it rank-correlates
  with the full score on one pilot round.
- Score null models first (constant output, untrained model, input copy).
  If a null model ever scores well, the harness is broken: freeze all
  conclusions and repair it before anything else. Keep one positive control -
  a signal the harness must detect; if it stops detecting it, same freeze.
- Pin metric conventions; if the published convention differs from ours,
  report both, labelled.
- Calibration and evaluation data are physically separate, split on the unit
  of independence (patient/speaker/site/time - not just files); tuning of any
  kind touches calibration only.
- Reproduce one published baseline number before trusting our own. If we
  cannot match it, keep reading the recipe (optimizer, loss, metric
  convention, operator) - do not "improve" an unmatched baseline.
- Verify every new guard by breaking what it watches, and confirm it fails
  for the right reason.

### The loop
Generate 10-30 variants per round, each with a one-line reason it might win;
sanity-check one instance before entry; sweep in parallel with executors that
only call the entry point (never write method code inline); select on
calibration; confirm top-k on held-out at full budget. **A gain that does not
reproduce held-out does not exist.** Report confirmations with an error bar
(paired difference vs the incumbent across instances/seeds); a sub-point gain
whose interval crosses zero is a coin flip, not a result. Budget held-out
accesses: log each one, and keep one final untouched set that is scored
exactly once, for the headline claim. Persist numbers to disk and commit
before writing sentences about them; convert each round's failures into new
harness checks.

### Claim polarity
The main sentence of any result must be constructive: "we propose X, it
solves Y, the number is Z." Audits, ablations and negative findings are
supporting material, never the headline. Check: is the main verb
"propose/solve/achieve", or "found that ... fails"? One counterweight:
polarity governs target choice and framing, not honesty - when a held-out-
confirmed null closes a question the field cares about, record the negative
and re-enter target triage; never massage a null into a positive.

### Stop conditions
- Candidates stop carrying new reasons -> the space is mined out: record the
  ceiling number, then escalate to a more ambitious target class instead of
  continuing to sweep the exhausted one.
- Any anti-cheat check fires -> fix the harness before interpreting anything.

### Verify, then go deeper
The 30-second proof of the selection discipline:
`git clone https://github.com/GuoCheng24/breakthrough-harness && cd breakthrough-harness && python examples/toy_loop.py`
Full methodology: harness/CHECKLIST.md, loop/LOOP.md, rules/RULES.md in the
same repository.
