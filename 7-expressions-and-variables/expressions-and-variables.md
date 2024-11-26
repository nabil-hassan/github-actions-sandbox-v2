# Expressions 

Expressions are comprised of one or more of the following:

- `literals` - fixed values such as strings, numbers, or booleans
- `variables` - references to context information such as `github`, `env`, `inputs`, `secrets`, `matrix`, `needs`
- `operators` - symbols that perform operations on one or more values e.g. &&, ||, !, ==, !=, >, <, >=, <=, etc.
- `functions` - GitHub actions inbuilt functions that can be used to manipulate data or perform operations

Expressions are always enclosed in `${{ }}` and can be used in a variety of places in a workflow file.

## Ternary operators

Ternary operators have two forms where `expression` is either a boolean-type variable or a condition that evaluates to a boolean:   :

- `${{expression || default_value}}`
- `${{expression && value_if_true || value_if_false}}`

Here is an example which is based on a boolean workflow input variable.

```yaml
name: Expressions
run-name: Using expressions | DEBUG - ${{ inputs.debug && 'ON' || 'OFF' }}
on:
  workflow_dispatch:
    inputs:
      debug:
        description: 'Debug mode'
        required: false
        type: boolean
        default: false
```

# Variables

Variables can be broken into the following kinds:

- Repository variables - either secret or standard
- Organisation variables - either secret or standard
- Environment variables - defined at the workflow, job or step level (they override from least to most precedence)

To see how to define and use environment variables, see the [contexts documentation](../6-contexts/contexts.md#environment-variables).

Repository and organisation variables are defined in the settings tab of the repository or organisation.

You can access them using two forms:

- First is the fully qualified context form:

```yaml
steps:
    - name: Accessing a repository variable
      run: echo ${{ vars.my_repo_variable }}
    - name: Accessing an environment variable
      run: echo ${{ env.MY_ENV_VARIABLE }}
```

- Second is simply by name:

```yaml
steps:
    - name: Accessing a repository variable
      run: echo ${{ my_repo_variable }}
    - name: Accessing an environment variable
      run: echo ${{ MY_ENV_VARIABLE }}
```

## Deployment environment variables and secrets

See also: [the deployment environment section](../11-deployment-environments/deployment-environments.md)

Repository variables can also be broken into deployment environment variables and secrets.

They will be accessed using the `vars` and `secrets` contexts respectively.

However, be aware the actual values are only available once you have specified the environment for a job.

See the comments below:

```yaml
# this is not fine as actions has no context of which environment will be used at this point so will not use the environmnet override
name: Deployment environments workflow
run-name: Deploy to ${{ github.event.inputs.environment }}
env:
  MY_ENV_VAR: ${{ vars.MY_ENV_VAR || 'DEFAULT' }}

jobs:
  # this example is fine as the environment is specified and the override will get picked up
  deploy-production:
    needs: deploy-lower-environment
    runs-on: ubuntu-latest
    environment: production
    steps:
        - name: deploy-prod
          run: echo "Welcome to the deployment environments workflow. The environment variable is:" ${{ vars.MY_ENV_VAR || 'DEFAULT' }}
```