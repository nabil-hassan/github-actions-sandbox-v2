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