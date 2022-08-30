# Build-A-Badge

[![latest-release](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-latest-release-badge.md&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIiBmaWxsPSIjRkZGIj48IS0tISBGb250IEF3ZXNvbWUgUHJvIDYuMS4yIGJ5IEBmb250YXdlc29tZSAtIGh0dHBzOi8vZm9udGF3ZXNvbWUuY29tIExpY2Vuc2UgLSBodHRwczovL2ZvbnRhd2Vzb21lLmNvbS9saWNlbnNlIChDb21tZXJjaWFsIExpY2Vuc2UpIENvcHlyaWdodCAyMDIyIEZvbnRpY29ucywgSW5jLi0tPjxwYXRoIGQ9Ik00OCAzMmgxNDkuNWMxNyAwIDMzLjIgNi43IDQ1LjIgMTguOGwxNzYgMTc1LjljMjUgMjUgMjUgNjUuNiAwIDkwLjZMMjg1LjMgNDUwLjdjLTI1IDI1LTY1LjYgMjUtOTAuNiAwbC0xNzYtMTc2QTYzLjggNjMuOCAwIDAgMSAwIDIyOS41VjgwYTQ4IDQ4IDAgMCAxIDQ4LTQ4em02NCAxNDRhMzIgMzIgMCAxIDAgMC02NCAzMiAzMiAwIDAgMCAwIDY0eiIvPjwvc3ZnPg==)](https://github.com/peterrhodesdev/build-a-badge/actions?query=workflow%3Abuild-a-badge-badges) [![license](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-license-badge.md)](https://github.com/peterrhodesdev/build-a-badge/blob/main/LICENSE) [![marketplace](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-marketplace-badge.md)](https://github.com/marketplace/actions/build-a-badge)

GitHub Action to create dynamic and customizable README badges using the [Shields.io endpoint](https://shields.io/endpoint).

This is achieved by storing the required JSON data of the badge in the repository's Wiki. Nothing is committed or pushed to the main repository, and there are no external dependencies that require configuring.

The only requirement is to have at least one page in your repository's Wiki.

- [Usage](#usage)
- [Input Parameters](#input-parameters)
- [Examples](#examples)

## Usage

Before using the action there must be **at least one page in your repository's Wiki** so that it can be used to store the badge data. See [here](https://docs.github.com/en/communities/documenting-your-project-with-wikis/adding-or-editing-wiki-pages) for instructions on how to add wiki pages.

### Single Badge

![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/my-badge.md)

Add a step to your workflow:

```yml
- name: Build-A-Badge
  uses: peterrhodesdev/build-a-badge@v1.2.3
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    filename: my-badge
    label: my
    message: badge
```

To display the badge in your README point the `url` parameter of the Shields endpoint query string to the raw content of the generated Wiki file:

```markdown
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/<owner>/<repo>/<filename>.md)
```

So, for the badge above it will be:

```markdown
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/my-badge.md)
```

> The JSON badge data is stored in the wiki section of the repo in a file called `<filename>.md`. The username and email of the user who performed the last commit will be used as the details for the commit to the wiki. Alos, the commit message will contain a link to the commit that triggered the badge data update.

### Multiple badges

![multiple-badges-1](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-1.md) ![multiple-badges-2](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-2.md) ![multiple-badges-3](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-3.md) ![multiple-badges-4](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-4.md) ![multiple-badges-5](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-5.md)

The input parameters also support arrays so that multiple badges can be created in a single workflow step.

```yml
name: Create multiple badges
on: [push]
jobs:
  multiple-badges:
    name: Multiple badges
    runs-on: ubuntu-latest
    steps:
      - name: Build-A-Badge
        uses: peterrhodesdev/build-a-badge@v1.2.3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          filename: ("multiple-badges-1" "multiple-badges-2" "multiple-badges-3" "multiple-badges-4" "multiple-badges-5")
          label: ("label 1" "label 2" "label 3" "label 4" "label 5")
          message: ("message 1" "message 2" "message 3" "message 4" "message 5")
          color: ("darkslategrey" "008b8b" 'rgb(128,0,128)' 'hsl(229,100%,50%)' "")
          labelColor: ("critical" "9cf" 'rgba(72,209,204,0.5)' 'hsla(36,80%,40%,0.7)' "")
          namedLogo: ("github" "" "npm" "" "javascript")
          logoSvg: |
            (
              ''
              '<svg id="Layer_1" data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 122.88 122.88"><defs><style>.cls-1{fill:#ffd528;}.cls-1,.cls-2{fill-rule:evenodd;}.cls-2{fill:#141518;}</style></defs><title>smiley</title><path class="cls-1" d="M45.54,2.11A61.42,61.42,0,1,1,2.11,77.34,61.42,61.42,0,0,1,45.54,2.11Z"/><path class="cls-2" d="M45.78,32.27c4.3,0,7.79,5,7.79,11.27s-3.49,11.27-7.79,11.27S38,49.77,38,43.54s3.48-11.27,7.78-11.27Z"/><path class="cls-2" d="M77.1,32.27c4.3,0,7.78,5,7.78,11.27S81.4,54.81,77.1,54.81s-7.79-5-7.79-11.27S72.8,32.27,77.1,32.27Z"/><path d="M28.8,70.82a39.65,39.65,0,0,0,8.83,8.41,42.72,42.72,0,0,0,25,7.53,40.44,40.44,0,0,0,24.12-8.12,35.75,35.75,0,0,0,7.49-7.87.22.22,0,0,1,.31,0L97,73.14a.21.21,0,0,1,0,.29A45.87,45.87,0,0,1,82.89,88.58,37.67,37.67,0,0,1,62.83,95a39,39,0,0,1-20.68-5.55A50.52,50.52,0,0,1,25.9,73.57a.23.23,0,0,1,0-.28l2.52-2.5a.22.22,0,0,1,.32,0l0,0Z"/></svg>'
              ''
              '<?xml version="1.0" encoding="utf-8"?><svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 122.88 106.16" style="enable-background:new 0 0 122.88 106.16" xml:space="preserve"><style type="text/css">.st0{fill-rule:evenodd;clip-rule:evenodd;}</style><g><path fill="#b5eaaa" class="st0" d="M4.02,44.6h27.36c2.21,0,4.02,1.81,4.02,4.03v53.51c0,2.21-1.81,4.03-4.02,4.03H4.02 c-2.21,0-4.02-1.81-4.02-4.03V48.63C0,46.41,1.81,44.6,4.02,44.6L4.02,44.6z M63.06,4.46c2.12-10.75,19.72-0.85,20.88,16.48 c0.35,5.3-0.2,11.47-1.5,18.36l25.15,0c10.46,0.41,19.59,7.9,13.14,20.2c1.47,5.36,1.69,11.65-2.3,14.13 c0.5,8.46-1.84,13.7-6.22,17.84c-0.29,4.23-1.19,7.99-3.23,10.88c-3.38,4.77-6.12,3.63-11.44,3.63H55.07 c-6.73,0-10.4-1.85-14.8-7.37V51.31c12.66-3.42,19.39-20.74,22.79-32.11V4.46L63.06,4.46z"/></g></svg>'
              ''
            )
          style: ("" "plastic" "flat-square" "for-the-badge" "social")
```

- use [bash array](https://www.gnu.org/software/bash/manual/html_node/Arrays.html) syntax
- use single quotes `''` for strings that contain parentheses `()`
- use an empty string `""` to leave a parameter unassigned

> the smiley custom logo is from [Font Awesome](https://fontawesome.com/v5/icons/smile?s=solid) and the thumbs up custom logo is from [UXWing](https://uxwing.com/thumbs-up-black-icon/)

Add the badges to the README according to the `filename` specified for each:

```markdown
![multiple-badges-1](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-1.md)
![multiple-badges-2](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-2.md)
![multiple-badges-3](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-3.md)
![multiple-badges-4](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-4.md)
![multiple-badges-5](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/multiple-badges-5.md)
```

## Input Parameters

See [Shields.io](https://shields.io/) and the [endpoint](https://shields.io/endpoint) for a more detailed description and list of supported values for the parameters.

| Name | Is required? | Default value | Array supported? | Description |
| --- | --- | --- | --- | --- |
| token | yes | | no | GitHub token secret used for authentication. The value [automatically created by GitHub](https://docs.github.com/en/actions/security-guides/automatic-token-authentication) can be used: `${{ secrets.GITHUB_TOKEN }}`. |
| filename | yes | | yes | The filename to use in the wiki for storing the JSON badge data. It cannot contain any whitespace characters. |
| label | yes | | yes | The left text. |
| message | yes | | yes | The right text. |
| color | no | lightgrey | yes | The right color. |
| labelColor | no | grey | yes | The left color. |
| namedLogo | no | | yes | Logo supported by Shields. |
| logoSvg | no | | yes | An SVG string containing a custom logo. |
| style | no | flat | yes | The default template to use. |
| wikiCommitUsername | no | username from the last commit | no | Override for the wiki commit username. |
| wikiCommitEmail | no | email from the last commit | no | Override for the wiki commit email. |
| wikiCommitMessage | no | URL link to the last commit | no | Override for the wiki commit message. |

Parameters marked as *Array supported* can be specified using either a single value or an array. Note that only one or the other is allowed, i.e. either all applicable parameters need to be single values or they all need to be arrays.

If `wikiCommitUsername`, `wikiCommitEmail`, and `wikiCommitMessage` are all overridden, then a checkout step will be skipped in the Build-A-Badge action, which will reduce the amount of time it takes to run.

## Examples

- [GitHub GraphQL API](#github-graphql-api)
- [git](#git)
- [npm package](#npm-package)

### GitHub GraphQL API

![github-graphql-api-open-issues](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-open-issues.md) ![github-graphql-api-open-vulnerabilities](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-open-vulnerabilities.md) ![github-graphql-api-open-pull-requests](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-open-pull-requests.md) ![github-graphql-api-forks](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-forks.md) ![github-graphql-api-stars](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-stars.md)

Badges generated from the results of some requests to the [GitHub GraphQL API](https://docs.github.com/en/graphql): open issues, open vulnerabilities, open pull requests, forks, and stars.

```yml
name: Create GitHub GraphQL API badges
on:
  schedule:
    - cron: "0 0 * * *"
jobs:
  github-graphql-api-badges:
    name: GitHub GraphQL API badges
    runs-on: ubuntu-latest
    steps:
      - name: Output GitHub GraphQL API info
        id: github_info
        run: |
          function github_graphql_request {
            echo $( \
              curl -H 'Content-Type: application/json' \
              -H "Authorization: bearer ${{ secrets.GITHUB_TOKEN }}" \
              -X POST \
              -d '{"query": "query {repository(owner: \"${{ github.repository_owner }}\", name: \"${{ github.event.repository.name }}\") {'$1$2' {totalCount}}}"}' \
              https://api.github.com/graphql \
              | jq ".data.repository."$1".totalCount" \
            );
          }
          echo "::set-output name=open_issues::$(github_graphql_request 'issues' '(states:OPEN)')"
          echo "::set-output name=open_vulnerabilities::$(github_graphql_request 'vulnerabilityAlerts' '(states:OPEN)')"
          echo "::set-output name=open_pull_requests::$(github_graphql_request 'pullRequests' '(states:OPEN)')"
          echo "::set-output name=stars::$(github_graphql_request 'stargazers' '')"
          echo "::set-output name=forks::$(github_graphql_request 'forks' '')"
        shell: bash
      - name: Build-A-Badge
        uses: peterrhodesdev/build-a-badge@v1.2.3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          filename: |
            (
              "github-graphql-api-open-issues"
              "github-graphql-api-open-vulnerabilities"
              "github-graphql-api-open-pull-requests"
              "github-graphql-api-forks"
              "github-graphql-api-stars"
            )
          label: ("open issues" "open vulnerabilities" "open pull requests" "forks" "stars")
          message: |
            (
              "${{ steps.github_info.outputs.open_issues }}"
              "${{ steps.github_info.outputs.open_vulnerabilities }}"
              "${{ steps.github_info.outputs.open_pull_requests }}"
              "${{ steps.github_info.outputs.forks }}"
              "${{ steps.github_info.outputs.stars }}"
            )
          namedLogo: ("github" "github" "github" "github" "github")
          color: ("4078c0" "4078c0" "4078c0" "4078c0" "4078c0")
```

```markdown
![github-graphql-api-open-issues](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-open-issues.md)
![github-graphql-api-open-vulnerabilities](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-open-vulnerabilities.md)
![github-graphql-api-open-pull-requests](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-open-pull-requests.md)
![github-graphql-api-forks](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-forks.md)
![github-graphql-api-stars](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/github-graphql-api-stars.md)
```

### git

![git-size](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-size.md) ![git-file-count](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-file-count.md) ![git-last-commit-date](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-last-commit-date.md) ![git-latest-release](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-latest-release.md) ![git-commits-to-main](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-commits-to-main.md)

Badges generated from the results of some `git` commands: size, file count, last commit date, latest release, and commits to main.

```yml
name: Create git badges
on: [push]
jobs:
  git-badges:
    name: git badges
    runs-on: ubuntu-latest
    steps:
      - name: Check out repo with all history
        uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - name: Output git info
        id: git_info
        run: |
          function format_size { echo $(numfmt --to iec --suffix B $1); }
          function format_number { LC_ALL=en_US.UTF-8 printf "%'d\n" $1; }
          echo "::set-output name=file_count::$(format_number $(git ls-files | wc -l))"
          echo "::set-output name=last_commit_date::$(git log -1 --format=%cd)"
          echo "::set-output name=latest_release::$(git describe --tags --abbrev=0)"
          echo "::set-output name=commits_to_main::$(format_number $(git rev-list --count main))"
          git gc
          echo "::set-output name=size::$(format_size $(($(git count-objects -v | grep 'size-pack: ' | sed 's/size-pack: //g' | tr -d '\n') * 1024)))"
        shell: bash
      - name: Build-A-Badge
        uses: peterrhodesdev/build-a-badge@v1.2.3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          filename: |
            (
              "git-size"
              "git-file-count"
              "git-last-commit-date"
              "git-latest-release"
              "git-commits-to-main"
            )
          label: ("size" "files" "last commit" "latest release" "commits to main")
          message: |
            (
              "${{ steps.git_info.outputs.size }}"
              "${{ steps.git_info.outputs.file_count }}"
              "${{ steps.git_info.outputs.last_commit_date }}"
              "${{ steps.git_info.outputs.latest_release }}"
              "${{ steps.git_info.outputs.commits_to_main }}"
            )
          namedLogo: ("git" "git" "git" "git" "git")
          color: ("f1502f" "f1502f" "f1502f" "f1502f" "f1502f")
```

```markdown
![git-size](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-size.md)
![git-file-count](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-file-count.md)
![git-last-commit-date](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-last-commit-date.md)
![git-latest-release](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-latest-release.md)
![git-commits-to-main](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/git-commits-to-main.md)
```

### npm package

![npm-package-version](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-version.md) ![npm-package-license](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-license.md) ![npm-package-size-unpacked](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-unpacked.md) ![npm-package-size-minified](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-minified.md) ![npm-package-size-minified-gzip](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-minified-gzip.md) ![npm-package-dependency-count](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-dependency-count.md) ![npm-package-downloads](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-downloads.md)

Badges for an npm package ([react](https://www.npmjs.com/package/react) in this example) using the results from:

- `npm view` - version, license, unpacked size
- [Bundlephobia](https://bundlephobia.com/) - minified size, minified + gzipped size, dependencies
- [npm registry](https://github.com/npm/registry/blob/master/docs/download-counts.md) - downloads last week

```yml
name: Create npm package badges
on:
  schedule:
    - cron: "0 0 * * 0"
jobs:
  npm-package-badges:
    name: npm package badges
    runs-on: ubuntu-latest
    env:
      NPM_PACKAGE_NAME: react
    steps:
      - name: Request JSON data from Bundlephobia
        id: bundlephobia
        run: echo "::set-output name=json::$(curl https://bundlephobia.com/api/size?package=$NPM_PACKAGE_NAME)"
        shell: bash
      - name: Output NPM package details
        id: npm_package_details
        run: |
          function format_size { echo $(numfmt --to iec --suffix B $1); }
          function format_number { LC_ALL=en_US.UTF-8 printf "%'d\n" $1; }
          echo "::set-output name=version::$(npm view $NPM_PACKAGE_NAME dist-tags.latest)"
          echo "::set-output name=license::$(npm view $NPM_PACKAGE_NAME license)"
          echo "::set-output name=size_unpacked::$(format_size $(npm view $NPM_PACKAGE_NAME dist.unpackedSize))"
          echo "::set-output name=size_minified::$(format_size $(jq '.size' <<< '${{ steps.bundlephobia.outputs.json }}'))"
          echo "::set-output name=size_minified_gzip::$(format_size $(jq '.gzip' <<< '${{ steps.bundlephobia.outputs.json }}'))"
          echo "::set-output name=dependency_count::$(jq '.dependencyCount' <<< '${{ steps.bundlephobia.outputs.json }}')"
          echo "::set-output name=downloads::$(format_number $(jq '.downloads' <<< $(curl https://api.npmjs.org/downloads/point/last-week/$NPM_PACKAGE_NAME)))"
        shell: bash
      - name: Build-A-Badge
        uses: peterrhodesdev/build-a-badge@v1.2.3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          filename: |
            (
              "npm-package-version"
              "npm-package-license"
              "npm-package-size-unpacked"
              "npm-package-size-minified"
              "npm-package-size-minified-gzip"
              "npm-package-dependency-count"
              "npm-package-downloads"
            )
          label: |
            (
              "version"
              "license"
              "unpacked size"
              "minified size"
              "minified + gzipped size"
              "dependencies"
              "downloads last week"
            )
          message: |
            (
              "${{ steps.npm_package_details.outputs.version }}"
              "${{ steps.npm_package_details.outputs.license }}"
              "${{ steps.npm_package_details.outputs.size_unpacked }}"
              "${{ steps.npm_package_details.outputs.size_minified }}"
              "${{ steps.npm_package_details.outputs.size_minified_gzip }}"
              "${{ steps.npm_package_details.outputs.dependency_count }}"
              "${{ steps.npm_package_details.outputs.downloads }}"
            )
          namedLogo: ("npm" "npm" "npm" "npm" "npm" "npm" "npm")
          color: ("cc3534" "cc3534" "cc3534" "cc3534" "cc3534" "cc3534" "cc3534")
```

```markdown
![npm-package-version](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-version.md)
![npm-package-license](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-license.md)
![npm-package-size-unpacked](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-unpacked.md)
![npm-package-size-minified](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-minified.md)
![npm-package-size-minified-gzip](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-minified-gzip.md)
![npm-package-dependency-count](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-dependency-count.md)
![npm-package-downloads](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-downloads.md)
```
