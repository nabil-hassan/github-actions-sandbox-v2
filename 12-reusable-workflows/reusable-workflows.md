# Reusable workflows

Any workflow can be made reusable by adding the `workflow_call` entry to the `on` directive of a workflow.

It can receive inputs and secrets, as well as produce outputs.

For a refresher on these types of item, see [the inputs/outputs section](../10-inputs-and-outputs)

For the full official documentation, see [over here](https://docs.github.com/en/actions/sharing-automations/reusing-workflows).

```yaml
on:
  workflow_call:
    inputs:
      aws-region:
        type: string
        
    secrets:
      auth-token:
        required: true
        
    outputs:
      server-url:
        value: <value>
```

In the caller workflow (i.e. what the one that makes use of the reusable workflow) you pass inputs, secrets as follows:

NB notice that unlike custom actions, reusable workflows are __only available__ at the `job level` and not the `step level`. 

```yaml
jobs:
  backend-infra:
    uses: resuable-deploy@v1
    secrets:
      auth-token: ${{ secrets.GH_PAT }}
    with:
      aws-region: ${{ vars.AWS_REGION }}
```

The outputs of the reusable job can be accessed using the `outputs` context

# Personal access tokens

In some cases, the resuable workflow may be stored in another repository.

In this case, the best practice is to use a `personal access token` to allow access for the caller.