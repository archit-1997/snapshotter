# snapshotter

A `GitHub` Action which creates a string
using the `commit SHA` and the `current timestamp` which can be used to name a `tag` and then publish it to `GitHub`.

## Usage

```yml
name: snapshot workflow
on:
  push:
    branches:
      - master
jobs:
  Generate Tag:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Create tag with Github SHA and timestamp
      uses: DevourTech/snapshotter@v1.1
      with:
        BASE_VERSION: v0.0.0
```

## Options

### Inputs

- `BASE_VERSION` (Required)

Base semantic version used to create snapshot. <br>
**Eg. v3.4.3**
<br>

###  Outputs
- `SNAPSHOT_VERSION`

Version generated by the action.

**Eg.v3.4.3-20200712152333-a007e621125e**

##Workflow

- Add this action to your repo
- Commit some changes
- push either to **master** or any other branch specified in the workflow
- On **push (or merge)**, the action will:
    - Get the latest commit hash and timestamp
    - Generate a custom string using the above two arguments

### NOTE

This action just generates a custom string which can be used as an output to release a tag with custom name.
If you also want to release this tag to `GitHub`, add this action [GitHub Script](https://github.com/marketplace/actions/github-script)
to your workflow file .