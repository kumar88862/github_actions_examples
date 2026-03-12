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


