# Notify Kubewarden Policy Hub

This action can be used to notify Kubewarden's Policy Hub about
a new policy to be listed or of an existing one to be updated.

The action triggers the execution of the `update-policy` workflow on the
`kubewarden/policy-hub` repository with the following input data:

* `repository`: the name of the GitHub repository hosting the policy to be
  added/updated
* `tag`: the name of the latest tag created on the policy repository

## Inputs

* `PAT`: this is the personal access token required to trigger the execution
  of a workflow on the `kubewarden/policy-hub` repository

## Example usage

Add this step to the release pipeline of your policy, the Policy Hub
should be notified 

```
on:
  push:
    tags:
    - 'v*'
jobs:
  release:
    name: Create new release with Wasm artifact
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      # More steps, like building the WebAssembly module and pushing it to
      # an OCI registry

      - name: notify policy-hub
        uses: kubewarden/notify-policy-hub
        with:
          PAT: ${{ secrets.PAT }}
```

