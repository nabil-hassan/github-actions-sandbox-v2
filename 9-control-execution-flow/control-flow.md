# Control flow

Two important rules related to flow of execution:

1. By default, if a step or job fails, GitHub actions will not run subsequent steps/jobs, unless you: 
 - include an `if` condition on the step in conjunction with a status check function.

```yaml
    steps:
      - name: fail
        run: exit 1

      - name: skipped step
        if: success()
        run: echo "This step will only run if the previous steps succeeded"

      - name: only if failed step
        if: failure()
        run: echo "This step will only run if one of the previous steps failed"
```

- Use `continue-on-error` to run subsequent jobs or steps even if the current one fails.

```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
    - name: step 1
      run: exit 1
    continue-on-error: true
```

2. GitHub will run a workflow's jobs in parallel __unless__ we use the `needs` directive to specify dependencies between jobs.

```yaml
jobs:
job1:
    runs-on: ubuntu-latest
    steps:
    - name: step 1
      run: echo "This is step 1"

job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
    - name: step 2
      run: echo "This is step 2"
```

