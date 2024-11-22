# Overview

Event filters and activity types are used in conjunction with `trigger types` to control when a workflow is triggered.

For instance below our trigger type is `pull_request`, we add an event filter based on the `branch` and an activity type of `opened`.

This effectively ttranslates to: "run when a pull request is opened with a target of main.

```yaml
name: Pull Requests
on: 
  pull_request:
    branches:
      - main
    types: [opened]
```

# Event Filters 

Event filters are used to specify the conditions under which a workflow is triggered.

The following are the core event filters:

- `branches` - specifies the branches the workflow should run against.
- `tags` - specifies the tags the workflow should run against.
- `paths` - specifies the paths the workflow should run against.

Each of these has a variant which can be used to exclude certain conditions:

- `paths-ignore` - specifies the paths the workflow should not run against.
- `branches-ignore` - specifies the branches the workflow should not run against.
- `tags-ignore` - specifies the tags the workflow should not run against.

Here is an example where we run on push to main and release branches but not on the `docs` folder:

```yaml
name: Push to main and release branches
on:
  push:
    branches:
      - main
      - release/*
    paths-ignore:
      - 'docs/**'
```

# Activity Types

Activity types define certain events that occur within the trigger type.

For instance, within a `pull_request` trigger type, the activity types are `opened`, `closed`, `labeled`, `unlabelled`, `reopened`, and `synchronize`.

NB synchronise means when a new commit is pushed to the branch of the pull request.

A full list of event triggers and activity types can be found [in this documentation](https://docs.github.com/en/actions/reference/events-that-trigger-workflows).
