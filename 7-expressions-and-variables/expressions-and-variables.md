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