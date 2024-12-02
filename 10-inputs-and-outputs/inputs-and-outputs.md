# Inputs and outputs

GitHub actions can take inputs and produce outputs. 

These are useful for passing data between jobs and steps and building reusable workflows using `custom actions` and `reusable workflows`.

They are made available via the `inputs` and `outputs` [contexts](../6-contexts/contexts.md).

Here is an example of passing inputs to a custom action via the `with` keyword.

```yaml
jobs:
  job1:
    steps:
      - name: Ping URL
        uses: nabil-hassan/ping-url-action@v1
        with:
        url: 'https://www.example.com'
        timeout: 1000
```

# Inputs

They can have the following properties:

- `required`: a boolean value that specifies whether the input is required. If set to `true` and the input is not provided, the workflow will fail.
- `default`: a default value for the input if not provided.
- `description`: a description of the input.
- `env`: a boolean value that specifies whether the input is set as an environment variable (by default .
- `type`: the type of the input. Can be `string`, `boolean`, `number`, `choice`, `environment` for workflow dispatch and `string`, `boolean`, `number` for workflow call.

NB workflow calls can also have secrets as inputs using `on.workflow_call.secrets`, we will cover that more in the dedicated section.