# PR workflow

## Motivations

This was motivated by observing that our workflows run whenever a developer pushes a commit TO ANY BRANCH,
irrespective of whether they intend to create a PR against it.

It was also motivated to allow "machine gun commiters" to not rack up costs by constantly running checks.

## Requirements 

- Checks should run only when a commit is pushed for a PR branch - if a branch is not associated with a PR then we shouldn’t run checks against it to avoid incurring cost.

- PRs cannot be merged into main unless they pass a set of checks.

- Developers should be able to temporarily disable checks, but they cannot merge until the checks are re-enabled and all are passing.

## Implementation

- Use the file [pr.yaml](./pr.yaml) to implement the workflow.
- The workflow illustrates the conditons and triggers, but you would need to add sensible steps for linting and testing.

- Enable branch protection rules on your trunk branch, optionally add a merge queue and require status checks to pass before merge.
- Select the workflow as one of the required checks (it must have run at least once)