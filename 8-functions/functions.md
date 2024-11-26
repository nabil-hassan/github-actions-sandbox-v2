# Functions

GitHub broadly offers two types of functions:

- [General purpose functions](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/evaluate-expressions-in-workflows-and-actions#functions): e.g. contains(), startsWith(), toJson(), fromJson(), etc.
- [Status check functions](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/evaluate-expressions-in-workflows-and-actions#status-check-functions): - allows you to check the status of a job, step or workflow e.g. success(), failure(), always(), cancelled()

## Status check functions

NB the default behaviour of GitHub is to not execute a step if the previous step failed. 

You can override this by placing an `if` condition on your job or step and using one of the following: 

- using the `always()` function - meaning it will run even if the previous step failed or was cancelled.
- using `!cancelled()` - meaning it will run if the previous step was not cancelled.

You can also use the success() and failure() functions within if expressions.

Here is a worked example.

## Hashing

You can use the `hashFiles()` on a filepath or set of file paths to generate a hash of the file contents.

This can be used for purposes of caching or to see if something has changed.

## Type conversions

NB environment variables are stored as Strings, but can be converted to Booleans or Integers using the `fromJson()` function.

```yaml
name: Type conversions
on: workflow_dispatch
env: 
  continue: true
  count: 3
jobs:
  type-conversions:
    runs-on: ubuntu-latest
    steps:
      - name: Convert a string to a boolean
        run: echo "${{ fromJson(env.continue) }}"
      - name: Convert a string to an integer
        run: echo "${{ fromJson(env.true) }}"
```

## Object filters

You can transform arrays of objects using [object filters](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/evaluate-expressions-in-workflows-and-actions#object-filters)..

Given this array of objects, the expression `fruits.*.name` returns : `["apple", "orange", "pear"]`

```json
[
  { "name": "apple", "quantity": 1 },
  { "name": "orange", "quantity": 2 },
  { "name": "pear", "quantity": 1 }
]
```

If you apply a filter on an array-type property, the result will be an array of arrays e.g.

```json
{
  "scallions":
  {
    "colors": ["green", "white", "red"],
    "ediblePortions": ["roots", "stalks"],
  },
  "beets":
  {
    "colors": ["purple", "red", "gold", "white", "pink"],
    "ediblePortions": ["roots", "stems", "leaves"],
  },
}
```

The filter `vegetables.*.ediblePortions` would evaluate to: `[["roots", "stalks"], ["roots", "stems", "leaves"]]` 