# Matrixes

Matrixes allow us to run several variations of the same job.

The matrix defines a number of key value pairs - each allowing us to modify the actual specific matrix segment.

These form a cartesian product of the key value pairs e.g. below: we will generate 6 permutations:

- 3 permutations for windows os using node version 18, 19 and 20
- 3 permutations for ubuntu os using node version 18, 19 and 20

NB a useful example of the utility is testing a NPM package on multiple versions of Node.js and OS.

```yaml
jobs:
  some-job:
  name: $[{ matrix.os }} - ${{ matrix.version }}
  runs-on: ${{ matrix.os }}
  strategy:
    matrix:
    os: [ubuntu-latest, windows-latest]
    version: [18, 19, 20]
  steps:
    - uses: actions/setup-node@v4
      with:
        node-version: ${{ matrix.version }}
```