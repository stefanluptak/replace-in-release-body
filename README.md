# Replace pattern in Release body with a text

## Motivation

I needed to replace Jira issues numbers `[XYZ-1234]` in our Release body with actual links to them.

## Usage

```yaml
name: Release notes jira links

on:
  pull_request:
    types:
      - opened

jobs:
  fill-pr-body:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - uses: stefanluptak/replace-in-release-body@v1
        with:
          pattern: "\[(WTF-[0-9]+)\]"
          replacement: "\[\1\]\(https:\/\/your.atlassian.net\/browse\/\1\)"
```

## Notes

`actions/checkout@v2` step before this action is needed, otherwise the `hub` command inside the action won't know on what git repository to operate.