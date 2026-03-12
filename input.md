# What are Inputs in GitHub Actions?
Inputs are parameters passed to workflows when they start.

```
Deploy workflow
   ↓
environment = dev
version = v1.2
```
The workflow behaves differently depending on the input.

# Inputs with workflow_dispatch
Inputs are most commonly used with manual workflows.
```
name: Deploy Application

on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Select environment"
        required: true
        type: choice
        options:
          - dev
          - stage
          - prod

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Print environment
        run: echo "Deploying to ${{ inputs.environment }}"
```

How it works

In the Actions tab, when you click Run workflow, GitHub will show a dropdown:
```
environment
  dev
  stage
  prod
```
Then the pipeline prints:
```
Deploying to prod
```
# Accessing Inputs
Inputs are accessed using:
```
${{ inputs.input_name }}
```
Example:
```
run: echo "${{ inputs.environment }}"
```

# Different Input Types
```
Type	    Description
string	    Text input
boolean	    true / false
choice	     Dropdown options
environment	GitHub environment
```

# Example with Multiple Inputs
```
name: Deploy

on:
  workflow_dispatch:
    inputs:
      app_name:
        description: "Application Name"
        required: true
        type: string

      version:
        description: "Version to deploy"
        required: true
        type: string

      environment:
        description: "Environment"
        required: true
        type: choice
        options:
          - dev
          - qa
          - prod
```