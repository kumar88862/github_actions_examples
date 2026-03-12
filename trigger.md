## What is a Trigger in GitHub Actions?
A trigger tells when a workflow should start.
```
on: push
```
This means Run the workflow when code is pushed to the repository.

Common triggers:
- push
- pull_request
- workflow_dispatch
- schedule
- release
- workflow_call

---
1. push
This trigger runs the workflow whenever code is pushed to a repository.

Example-1

```
on: push
```
workflow get trigger when the code is pushed to repository irrespective of branch.

Example-2
```
on:
  push:
    branches:
      - main
```
workflow start when the code is pushed to main branch. 


2. pull_request
This trigger runs when a Pull Request is created or updated.
```
on:
  pull_request:
  
```
Events that trigger it
- PR created
- PR updated
- PR reopened


3. workflow_dispatch
This allows manual pipeline execution from GitHub UI.

```
on:
  workflow_dispatch:
```
Go to:
```
Repository → Actions → Workflow → Run Workflow
```

4. schedule
This trigger runs workflows at a scheduled time using cron syntax.

```
on:
  schedule:
    - cron: "0 2 * * *"

```

What it means

Run workflow every day at 2 AM UTC.

Cron format

```
minute hour day month day_of_week
Cron	        Meaning
0 2 * * *	    Daily 2AM
0 * * * *	    Every hour
0 0 * * 0	    Every Sunday
```

5. release
This trigger runs when a GitHub release is created or published.

```
on:
  release:
    types: [published]
```
6. workflow_call
This trigger allows one workflow to call another workflow. This is used for reusable workflows.

```
on:
  workflow_call:

```
Example
```
jobs:
  call-workflow:
    uses: org/repo/.github/workflows/deploy.yml@main
```



## Real CI/CD Example

Most real pipelines look like this:
```
on:
  push:
    branches: [main]

  pull_request:
    branches: [main]

  workflow_dispatch:

  schedule:
    - cron: "0 2 * * *"
```
Meaning:

- Push → CI build
- PR → validation
- Manual → engineer trigger
- Schedule → nightly jobs

---

## Creating a Reusable Workflow
Reusable workflows must still be placed inside:
```
.github/workflows/
```
Create a Reusable Workflow

```
name: Reusable Build

on:
  workflow_call:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Build application
        run: echo "Building project..."
```
Important part:
```
on:
  workflow_call:

```
This means the workflow can only run when another workflow calls it.

## Calling the Reusable Workflow

```
name: CI Pipeline

on:
 workflow_dispatch

jobs:
  call-build:
    uses: ./.github/workflows/reusable-build.yml
```


