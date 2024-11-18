<h1> GitHub Actions V2 </h1>

<img src="./img/maxresdefault.png" width="500"/>

A newer version of GitHub actions sandbox.

This readme acts as a guide to the key areas of the repository.

NB please see the [Forumlas](./0-formulas) sections for examples of how to address common requirements.

<h1>Table of contents</h1>

<!-- TOC -->
* [Cool things](#cool-things)
* [Getting started](#getting-started)
* [Event Triggers](#event-triggers)
* [Workflow Runners](#workflow-runners)
<!-- TOC -->

# Cool things

Reverting PRs in case of failure.

# Getting started

The key parts of getting started are understanding some basic concepts of YAML syntax and the building blocks of GitHub Actions.

We also need to understand how jobs and steps run and how they are or are not dependent on each other.

- [A note on codespaces and ASDF](./1-getting-started/getting-started.md#a-note-on-codespaces-and-asdf)
- [YAML crash course](./1-getting-started/getting-started.md#yaml-crash-starter)
- [Writing multi-line statements](./1-getting-started/getting-started.md#writing-multi-line-statements)
- [Building blocks](./1-getting-started/getting-started.md#building-blocks)
- [Job Parallelism and execution separation](./1-getting-started/getting-started.md#parallelism-and-execution-environment)
- [Example workflow](./.github/workflows/01-building-blocks.yaml)

# Event Triggers

Event triggers specify the conditions under which a workflow is started and optionally which branches it should be run against.

By default event triggers run for any branch which match the trigger conditions.

Workflows can also be started manually using `workflow dispatch` or run on a CRON schedule using `schedule`.

- [The main event trigger types](./2-event-triggers/event-triggers.md#event-trigger-types)
- [Accessing the event trigger details](./2-event-triggers/event-triggers.md#accessing-the-workflow-event-trigger-details)
- [Example workflow](./.github/workflows/02-workflow-events.yaml)

# Workflow Runners

Workflow runners are virtual servers used to execute the jobs that comprise our workflows.

You can use the `runs-on` keyword to specify the runner for a job. 

You either use the default GitHub hosted runners or __self-hosted__ runners.

GitHub provides Windows, Ubuntu and Mac runners.

- [Notes on jobs and runner relationship](./3-workflow-runners/workflow-runners.md#notes-on-jobs-and-runners)
- [Comparison of runner types](./3-workflow-runners/workflow-runners.md#comparison-of-runner-types)
- [A note on security regarding self-hosted runners](./3-workflow-runners/workflow-runners.md#a-note-on-security-regarding-self-hosted-runners)
- [What's available in my runner?](./3-workflow-runners/workflow-runners.md#whats-available-in-my-runner)
- [Example workflow](./.github/workflows/03-workflow-runners.yaml)

# Third Party Actions