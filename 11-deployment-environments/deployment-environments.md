# Caveat on deployment environments

NB deployment environments are only available for public repos OR if you are a paid customer.

Thus, the worked example for this section is found in another repo: [which is public](https://github.com/nabil-hassan/github-actions-sandbox-public)

## Deployment environment variables and secrets

Repository variables can also be broken into deployment environment variables and secrets.

For instance, we may have different AWS credentials for our development, staging and production environments.

Using GitHub's support for different deployment environments the value of a variable will change depending on which environment it is running in.

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