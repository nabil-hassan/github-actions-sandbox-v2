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

- Repository variables
- Organisation variables
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

NB environments are only available for public repos OR if you are a paid customer.

Repository variables can also be broken into deployment environment variables and secrets. 

For instance, we may have different AWS credentials for our development, staging and production environments.

Using GitHub's support for different deployment environments the value of a variable will change depending on which environment it is running in.

Refer to the [example workflow](../.github/workflows/08-variables-deployment-environments.yaml) for an example.

Here are the steps required to implement:

- In the GitHub UI create three environments: PRODUCTION, STAGING, DEVELOPMENT:

- Add a variable to each environment with the same name but different values:

- Define the environment for each job and echo the variable:


```yaml
jobs:
  do-prod:
    runs-on: ubuntu-latest
    environment: PRODUCTION
    steps:
      - name: Deploy to production
        run: echo "Deploying with var = ${repo_var}"
        
  do-test:
    runs-on: ubuntu-latest
    environment: TEST
    steps:
    - name: Deploy to production
      run: echo "Deploying with var = ${repo_var}"
```