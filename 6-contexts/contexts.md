# Contexts

Contexts allow you to access information during a workflow and can be broken down into the following types:

- `github` - provides information about the event that triggered the workflow eg the workflow trigger type, branch name etc.
- `env` - environment variables that have been defined in a workflow, job, or step 
- `inputs` - passed to a reuasable workflow or third party action using the `with` statement
- `vars` - variables that have been defined in the repository, organisation etc
- `secrets` - as above but specifically for secrets
- `matrix` - used for build matrixes
- `needs` - used for requirements

A full listing of contexts can be found [here](https://docs.github.com/en/enterprise-cloud@latest/actions/writing-workflows/choosing-what-your-workflow-does/accessing-contextual-information-about-workflow-runs).

See the worked example: [over here](../.github/workflows/06-contexts.yaml)

NB not all contexts are available at every stage of a workflow - see the documents above for details on exactly where and when you can access them.

# Workflow inputs

A workflow that is a reusable workflow or can be called via workflow dispatch can accept inputs.

Here is an example of accepting a simple boolean input and using it within the run name:

```yaml
name: Contexts
run-name: 06 - Contexts | DEBUG - ${{ inputs.debug }}
on:
  workflow_dispatch:
    inputs:
      debug:
        description: 'Run in debug mode'
        type: boolean
        default: false
```

# Environment variables

Environment variables can be defined at the __workflow, job or step level__ using the `env` directive:

You can override existing variables - the order of precedence is: step > job > workflow.

```yaml
name: Contexts
run-name: 06 - Contexts | DEBUG - ${{ inputs.debug }}
on:
  workflow_dispatch:
env:
  MY_WORKFLOW_VAR: "workflow"
  MY_OVERWRITTEN_VAR: "workflow"
jobs:
  environment-context:
    runs-on: ubuntu-latest
    env:
      MY_JOB_VAR: "job"
      MY_OVERWRITTEN_VAR: "overwrite"    # OVERRIDE AT JOB LEVEL
    steps:
      - name: Display environment context information
        run: |
          echo "Workflow environment variable: ${{ env.MY_WORKFLOW_VAR }}"
          echo "Job environment variable: ${{ env.MY_JOB_VAR }}"
          echo "Overwritten environment variable: ${{ env.MY_OVERWRITTEN_VAR }}"
      - name: Override variable at step level
        env:
          MY_OVERWRITTEN_VAR: "step"      # OVERRIDE AT STEP LEVEL
        run: |
          echo "Overwritten environment variable: ${{ env.MY_OVERWRITTEN_VAR }}"
```

