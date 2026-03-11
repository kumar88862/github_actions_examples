## Github actions basics
1. GitHub Actions is a CI/CD automation tool that runs workflows based on repository events.
2. A workflow is an automated process defined in YAML that runs one or more jobs.
3. A job is a group of steps.
4. Workflows run on machines called runners
5. GitHub automatically detects workflows from this folder.
```
.github/
   workflows/
       ci.yml
```
6. Each job runs in a separate environment
7. Jobs can run parallel
8. Jobs can have dependencies
9. A step is a single task executed in a job and Steps execute sequentially.
10. An Action is a reusable unit of code.
11. Minimal Working Workflow
```
name: Hello Pipeline

on: push

jobs:
  hello:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Hello World"
```