# Caveat on deployment environments

NB deployment environments are only available for public repos OR if you are a paid customer.

Thus, the worked example for this section is found in another repo: [which is public](https://github.com/nabil-hassan/github-actions-sandbox-public)

# Purposes of deployment environments

The main purposes of deployment environments are:

- To define different variable and secret values for different environments.
- To specify required approvers to gate deployments to higher environments.
- To restrict which branches can be deployed to which environments.

# Setting up an environment

- Use the repository settings tab and open the `environments` section:

<img src="../img/deployment-environments-new.png" width="700">

- The dialog that appears is used to configure reviewers, branches, variables and secrets

<img src="../img/environment-config.png" width="700">

- If you add review requirements then any job which has its `environment` set to this environment will require approval before it can run, as per the example below.

```yaml
jobs:
  deploy-production:
    needs: deploy-lower-environment
    runs-on: ubuntu-latest
    environment: production
    steps:
        - name: deploy-prod
          run: echo "Deploying to production"
```

<img src="../img/environment-protection.png" width="700">

## Deployment environment variables and secrets

Repository variables can also be broken into deployment environment variables and secrets.

For instance, we may have different AWS credentials for our development, staging and production environments.

Using GitHub's support for different deployment environments the value of a variable will change depending on which environment it is running in.

Here are the steps required to implement:

- In the GitHub UI create three environments: PRODUCTION, STAGING, TEST:

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