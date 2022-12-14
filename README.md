# carthage-update-check-action
[![CI-Master](https://github.com/MeilCli/carthage-update-check-action/actions/workflows/ci-master.yml/badge.svg)](https://github.com/MeilCli/carthage-update-check-action/actions/workflows/ci-master.yml)  
Carthage new package version check action for GitHub Actions.

## Required
This action must execute on macOS.

## Example
Slack notification example, using [8398a7/action-slack](https://github.com/8398a7/action-slack):

```yaml
name: Check Package

on: 
  schedule:
    - cron: '0 8 * * 5' # every friday AM 8:00
jobs:
  carthage:
    runs-on: macOS-latest
    steps:
    - uses: actions/checkout@v1
    - uses: MeilCli/carthage-update-check-action@v3
      id: outdated
    - uses: 8398a7/action-slack@v2
      if: steps.outdated.outputs.has_carthage_update != 'false'
      with:
        status: ${{ job.status }}
        text: ${{ steps.outdated.outputs.carthage_update_text }}
        author_name: GitHub Actions
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
```
You can also pin to a [specific release](https://github.com/MeilCli/carthage-update-check-action/releases) version in the format `@v3.x.x`

## input
- `execute_directories`
  - optional
  - execute directories of npm outdated command
  - if multiple directories, write multiline

## output
- `has_carthage_update`
  - has new package version information
  - value: `true` or `false`
- `carthage_update_text`
  - new package version information text
- `carthage_update_json`
  - new package version information json

## Contributes
[<img src="https://gist.github.com/MeilCli/e93dff5045ec3114e4073597fa844b07/raw/79be247c9959df1d046baec619233911a0ca1b97/metrics_contributors.svg">](https://github.com/MeilCli/carthage-update-check-action/graphs/contributors)

### Could you want to contribute?
see [Contributing.md](./.github/CONTRIBUTING.md)

## License
[<img src="https://gist.github.com/MeilCli/e93dff5045ec3114e4073597fa844b07/raw/79be247c9959df1d046baec619233911a0ca1b97/metrics_licenses.svg">](LICENSE)
