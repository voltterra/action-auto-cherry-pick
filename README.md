# Automatic cherry-picking

Cherry-picks commits from a merged PR, creating a new PR to a target branch.
Allows setting a name of a submodule and will automatically fast-forward it to
also match the `target-branch`.

Check [action.yml](action.yml) for a description of inputs and outputs.


TODO: Update the sample with added parameters
### Configuration sample

```yaml
name: 'Cherry pick Release/candidate into develop'
on:
  pull_request:
    branches:
      - release/candidate # Branches where the original PRs will be merged
    types:
      - closed

jobs:
  test-cherry-pick:
    runs-on: ubuntu-latest
    name: Test the cherry-pick action
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          submodules: recursive #If you need to operate on submodules

      - name: Cherry pick
        id: cherry-pick
        uses: wireapp/action-auto-cherry-pick@v1.0.2
        with:
          # Branch which will receive the automatic cherry-picks
          target-branch: 'develop'

          # If you want the action to fast-forward the submodules to a specific branch
          submodules-target-branch: 'develop'
          pr-title-suffix: '🍒'

      - name: Get the output
        run:
          echo "The created PR number is ${{
          steps.cherry-pick.outputs.pr-number }}"
```


## Original authors
TODO: Add the link to the original repository
