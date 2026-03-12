# What are Environment Variables?
Environment variables are key-value pairs used inside workflows.
```
env:
  APP_NAME: payment-service
```

Use it later:

```
run: echo $APP_NAME
```
# Environment Variables at Workflow Level
These variables are available for all jobs and steps.
```
name: Env Example

on: push

env:
  APP_NAME: payment-service
  ENVIRONMENT: dev

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Print variables
        run: |
          echo "App is $APP_NAME"
          echo "Environment is $ENVIRONMENT"
```

# Environment Variables at Job Level
Variables defined inside a job are available only for that job.
```
jobs:
  build:
    runs-on: ubuntu-latest

    env:
      BUILD_TYPE: docker

    steps:
      - name: Print variable
        run: echo "Build type is $BUILD_TYPE"
```

# Environment Variables at Step Level
Variables can also be defined only for a specific step.

```
steps:
  - name: Test step variable
    env:
      TEST_ENV: staging
    run: echo "Testing in $TEST_ENV"
```
# Accessing Environment Variables
```
$APP_NAME
```
In GitHub expressions:
```
${{ env.APP_NAME }}
```
# Example with Multiple Variables

```
name: Environment Example

on: workflow_dispatch

env:
  APP_NAME: payment-service
  VERSION: v1.2
  ENVIRONMENT: staging

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Print deployment info
        run: |
          echo "App: $APP_NAME"
          echo "Version: $VERSION"
          echo "Environment: $ENVIRONMENT"
```