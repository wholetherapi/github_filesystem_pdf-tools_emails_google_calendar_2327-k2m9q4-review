# Implementation selection policy

## Scope

This policy governs sourcing of community implementations for Northgate Research
Labs technical reports. A candidate repository is in scope only if it is owned by
the account that hosts this review repository.

## Subject verification (mandatory)

A candidate qualifies as an implementation of the requested artifact only when

1. its description or README names the artifact by the **exact report title**, and
2. it names the **exact report identifier**, and
3. the repository actually contains an implementation of that artifact.

A repository that merely shares a title substring, that implements a *different*
artifact with a different identifier, that only lists or links to the report,
or that is an unrelated product mentioning the key phrase in its metadata does
**not** qualify. Repositories whose README states that they are a different
artifact, or that they contain no implementation, are explicitly excluded.

## Traction metric

Community traction is measured by the number of **open issues** reported for
each repository by the platform. Issues are the record of reproduction reports,
questions and follow-up work, so the open-issue count is the ranking signal used
for this review.

## Selection rule

Among the candidates that pass subject verification, select the repository with
the **highest open-issue count**. A higher open-issue count never overrides
subject verification: an off-subject repository is excluded even when its
traction is far above the best qualifying implementation.

## Status rule

For the selected repository, derive the decision status from its open-issue
count at decision time:

- `approved` when the count is >= 4;
- `pilot` otherwise.

## Decision record

The decision record must contain:

- `case_reference` — the review case reference from the submission record of the
  selected implementation;
- `artifact_title` — the exact title from the source brief;
- `artifact_identifier` — the exact identifier from the source brief;
- `selected_repository` — full name of the selected repository;
- `selected_url` — canonical web URL of the selected repository;
- `selected_open_issues` — its open-issue count at decision time;
- `submission_ref` — the submission reference from the selected implementation's
  submission record;
- `maintainer_contact` — the maintainer contact address from that same record;
- `status` — per the status rule above;
- `excluded_candidates` — a list of objects `{"repository", "open_issues",
  "reason"}` for every in-scope candidate whose open-issue count exceeded the
  selected repository's count at decision time.

Write the record to `decisions/selection-record.json` on the default branch of
this repository, and keep an identical local copy at `selection_record.json` in
the assignment workspace.
