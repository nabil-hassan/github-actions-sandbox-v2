# Expressions 

Expressions are comprised of one or more of the following:

- `literals` - fixed values such as strings, numbers, or booleans
- `variables` - references to context information such as `github`, `env`, `inputs`, `secrets`, `matrix`, `needs`
- `operators` - symbols that perform operations on one or more values e.g. &&, ||, !, ==, !=, >, <, >=, <=, etc.
- `functions` - GitHub actions inbuilt functions that can be used to manipulate data or perform operations

Expressions are always enclosed in `${{ }}` and can be used in a variety of places in a workflow file.

## Ternary operators

Ternary operators have two forms:

- `${{expression || default_value}}`
- `${{expression && value_if_true || value_if_false}}`

Here is an example which is based on a boolean workflow input variable.

# Variables

## Default variable values

Default values can be set for variables using the `||` operator.

```yaml

```