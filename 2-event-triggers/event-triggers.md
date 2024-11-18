# Event Triggers

As we saw in the previous section, the `on` keyword is used to specify the conditions under which a workflow is started.

Below, the event trigger type is pull request and the actions are opened, synchronize, reopened, and closed.

NB synchronized means when a commit is pushed to the branch of the pull request.

```yaml
name: Pull Requests
on: 
  pull_request:
    types: [opened, synchronize, reopened, closed]
```

