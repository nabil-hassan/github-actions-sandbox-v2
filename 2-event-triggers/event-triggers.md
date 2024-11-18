# Event Triggers

As we saw in the previous section, the `on` keyword is used to specify the conditions under which a workflow is started.

Below, the event `trigger type` is pull_request and the `activity types` are opened, synchronize, reopened, and closed.

NB synchronized means when a commit is pushed to the branch of the pull request.

```yaml
name: Pull Requests
on: 
  pull_request:
    types: [opened, synchronize, reopened, closed]
```

# Event trigger types

A comprehensive list of event triggers and activity types can be found [here](https://docs.github.com/en/actions/reference/events-that-trigger-workflows).

The key types are:

- push 
- pull_request
- pull_request_review
- workflow_dispatch
- issues

Workflows can also be run __on a schedule__ or manually via workflow dispatch using the `schedule` trigger type.

NB the most frequent you can run is every 15 minutes - using a more frequent expression means the workflow will not run.

```yaml
# Run every 15 minutes
on:
  schedule:
    - cron: "*/15 * * * *"
```