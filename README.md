# Build-A-Badge

[![latest-release](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-latest-release-badge.md&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIiBmaWxsPSIjRkZGIj48IS0tISBGb250IEF3ZXNvbWUgUHJvIDYuMS4yIGJ5IEBmb250YXdlc29tZSAtIGh0dHBzOi8vZm9udGF3ZXNvbWUuY29tIExpY2Vuc2UgLSBodHRwczovL2ZvbnRhd2Vzb21lLmNvbS9saWNlbnNlIChDb21tZXJjaWFsIExpY2Vuc2UpIENvcHlyaWdodCAyMDIyIEZvbnRpY29ucywgSW5jLi0tPjxwYXRoIGQ9Ik00OCAzMmgxNDkuNWMxNyAwIDMzLjIgNi43IDQ1LjIgMTguOGwxNzYgMTc1LjljMjUgMjUgMjUgNjUuNiAwIDkwLjZMMjg1LjMgNDUwLjdjLTI1IDI1LTY1LjYgMjUtOTAuNiAwbC0xNzYtMTc2QTYzLjggNjMuOCAwIDAgMSAwIDIyOS41VjgwYTQ4IDQ4IDAgMCAxIDQ4LTQ4em02NCAxNDRhMzIgMzIgMCAxIDAgMC02NCAzMiAzMiAwIDAgMCAwIDY0eiIvPjwvc3ZnPg==)](https://github.com/peterrhodesdev/build-a-badge/actions?query=workflow%3Abuild-a-badge-badges) [![license](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-license-badge.md)](https://github.com/peterrhodesdev/build-a-badge/blob/main/LICENSE) [![marketplace](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-marketplace-badge.md)](https://github.com/marketplace/actions/build-a-badge)

GitHub Action to create dynamic and customizable README badges using the [Shields.io endpoint](https://shields.io/endpoint).

This is achieved by storing the required JSON data of the badge in the repository's Wiki. Nothing is committed or pushed to the main repository, and there are no external dependencies that require configuring.

The only requirement is to have at least one page in the Wiki so that it can be cloned. See [here](https://docs.github.com/en/communities/documenting-your-project-with-wikis/adding-or-editing-wiki-pages) for instructions on how to add wiki pages.

- [Usage](#usage)
- [Input Parameters](#input-parameters)
- [Examples](#examples)

## Usage

### Single Badge

![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/my-badge.md)

Add a step to your workflow:

```yml
- name: Build-A-Badge
  uses: peterrhodesdev/build-a-badge@v1.2.1
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
  test-badge:
    name: Multiple badges
    runs-on: ubuntu-latest
    steps:
      - name: Build-A-Badge multiple
        uses: peterrhodesdev/build-a-badge@v1.2.1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          filename: ("multiple-badges-1" "multiple-badges-2" "multiple-badges-3" "multiple-badges-4" "multiple-badges-5")
          label: ("label 1" "label 2" "label 3" "label 4" "label 5")
          message: ("message 1" "message 2" "message 3" "message 4" "message 5")
          color: ("darkslategrey" "008b8b" 'rgb(128,0,128)' 'hsl(229,100%,50%)' "")
          labelColor: ("critical" "9cf" 'rgba(72,209,204,0.5)' 'hsla(36,80%,40%,0.7)' "")
          namedLogo: ("github" "" "npm" "" "javascript")
          style: ("" "plastic" "flat-square" "for-the-badge" "social")
```

- use [bash array](https://www.gnu.org/software/bash/manual/html_node/Arrays.html) syntax
- use single quotes `''` for strings that contain parentheses `()`
- use an empty string `""` to leave a parameter unassigned

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

| Name | Is required? | Default value | Description |
| --- | --- | --- | --- |
| filename | yes | | The filename to use in the wiki for storing the JSON badge data. It cannot contain any whitespace characters. |
| label | yes | | The left text. |
| message | yes | | The right text. |
| color | no | lightgrey | The right color. |
| labelColor | no | grey | The left color. |
| namedLogo | no | | Logo supported by Shields. |
| style | no | flat | The default template to use. |

> Each parameter supports either a single value or an array. Only one or the other is supported, i.e. either all parameters need to be single or all parameters need to be an array.

## Examples

- [Custom logo](#custom-logo)
- [npm package](#npm-package)

### Custom logo

[![last-commit-badge](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/last-commit-badge.md&logo=data:image/svg%2bxml;base64,PHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeD0iMCIgeT0iMCIgdmlld0JveD0iMCAwIDEyMi45IDEyMCIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgZW5hYmxlLWJhY2tncm91bmQ9Im5ldyAwIDAgMTIyLjg4IDExOS45NyIgZmlsbD0iI0ZGRkZGRiI+PHBhdGggZD0iTTY5LjggNGMwLTIuMiAyLjItNCA1LTRzNC45IDEuOCA0LjkgNHYxNy44YzAgMi4yLTIuMiA0LTUgNHMtNS0xLjgtNS00VjQuMXpNMTQuNCA3OGgxMS4zYy43IDAgMS4zLjYgMS4zIDEuNHY4LjNjMCAuOC0uNiAxLjMtMS4zIDEuM0gxNC40Yy0uOCAwLTEuMy0uNS0xLjMtMS4zdi04LjNjMC0uOC42LTEuNCAxLjMtMS40em00My40LTIzLjhINjljLjQgMCAuNy4xIDEgLjNhNDAuNCA0MC40IDAgMCAwLTExLjQgMTAuN2gtMWMtLjYgMC0xLjItLjYtMS4yLTEuM3YtOC40YzAtLjcuNi0xLjMgMS4zLTEuM3ptLTIxLjcgMGgxMS4zYy43IDAgMS4zLjYgMS4zIDEuM3Y4LjRjMCAuNy0uNiAxLjMtMS4zIDEuM0gzNi4xYy0uNyAwLTEuMy0uNi0xLjMtMS4zdi04LjRjMC0uNy42LTEuMyAxLjMtMS4zem0tMjEuNyAwaDExLjNjLjcgMCAxLjMuNiAxLjMgMS4zdjguNGMwIC43LS42IDEuMy0xLjMgMS4zSDE0LjRjLS44IDAtMS4zLS42LTEuMy0xLjN2LTguNGMwLS43LjYtMS4zIDEuMy0xLjN6TTM2IDc4aDExLjNjLjcgMCAxLjMuNiAxLjMgMS40djguM2MwIC44LS42IDEuMy0xLjMgMS4zSDM2LjFjLS43IDAtMS4zLS41LTEuMy0xLjN2LTguM2MwLS44LjYtMS40IDEuMy0xLjR6bTY3LjQtMTguNWEzMS40IDMxLjQgMCAxIDEtMjQgNTggMzEuNCAzMS40IDAgMCAxIDI0LTU4ek04Ni42IDg3LjdsMS40LTFWNzNhMi41IDIuNSAwIDAgMSA1IDB2MTMuNmMxIC41IDEuOCAxLjMgMi4yIDIuMmg5LjhhMi41IDIuNSAwIDEgMSAwIDVoLTkuN2E1LjMgNS4zIDAgMSAxLTguNy02em0yMy41LTE3LjNjLTEzLTEzLTM1LTkuMy00Mi41IDdhMjYuMyAyNi4zIDAgMSAwIDQ3LjYtLjRjLTEuMy0yLjYtMy00LjUtNS02LjZ6TTI1LjMgNC4xYzAtMi4zIDIuMi00LjEgNS00LjEgMi43IDAgNSAxLjggNSA0djE3LjhjMCAyLjItMi4zIDQtNSA0LTIuOCAwLTUtMS44LTUtNFY0LjF6TTUuNCAzOC44aDk0LjNWMTguNGMwLS43LS4zLTEuMy0uOC0xLjgtLjQtLjQtMS0uNy0xLjctLjdoLTlhMi43IDIuNyAwIDAgMSAwLTUuNWg5YTggOCAwIDAgMSA4IDh2MzIuNGE0MSA0MSAwIDAgMC01LjYtMS41di01SDUuNnY1Mi45YzAgLjcuMiAxLjMuNyAxLjcuNC41IDEgLjggMS43LjhoNDQuOGMuNSAxLjkgMS4yIDMuNyAyIDUuNUg4YTggOCAwIDAgMS04LThWMTguNGE4IDggMCAwIDEgOC04aDkuNmEyLjcgMi43IDAgMCAxIDAgNS41SDhjLS43IDAtMS4zLjMtMS44LjctLjQuNS0uNyAxLjEtLjcgMS44djIwLjR6bTM3LjctMjNhMi43IDIuNyAwIDAgMSAwLTUuNGgxOC40YTIuNyAyLjcgMCAwIDEgMCA1LjVINDMuMXoiLz48L3N2Zz4=)](https://github.com/peterrhodesdev/build-a-badge/actions?query=workflow%3Alast-commit-badge)

Display the last commit date for the repository using a custom logo.

The custom logo is defined by the `logo` parameter in the Shields.io endpoint query string. So it will be assigned in the README, not in the workflow.

```yml
name: Create last commit badge
on: [push]
jobs:
  last-commit-badge:
    name: Last commit badge job
    runs-on: ubuntu-latest
    steps:
      - name: Check out repo
        uses: actions/checkout@v3
      - name: Output last commit
        id: last_commit
        run: echo "::set-output name=value::$(git log -1 --format=%cd)"
      - name: Build-A-Badge
        uses: peterrhodesdev/build-a-badge@v1.2.1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          filename: last-commit-badge
          label: "Last commit"
          message: ${{ steps.last_commit.outputs.value }}
          color: blue
```

The steps to include a custom logo in the badge like the one above are are:

1. Download an SVG file (the image used above is from [UXWing](https://uxwing.com/date-and-time-icon/)).
1. Edit the fill color if desired (I used the free SVG editor from [RapidTables](https://www.rapidtables.com/web/tools/svg-viewer-editor.html) to change the fill to white with `fill="#FFFFFF"`).
1. Minify the SVG to reduce the length of the URL that will be produced (I used the SVG minifier tool at [Devina](https://devina.io/svg-minifier)).
1. Convert the SVG to a Base64 data URI (I used [Base64 Guru](https://base64.guru/converter/encode/image/svg)).
1. Encode the data URI by replacing the plus sign (`+`) with `%2b`.
1. Add the encoded data URI to the query string in the README like: `https://img.shields.io/endpoint?url=...&logo=<encoded data URI>`.

```markdown
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/last-commit-badge.md&logo=data:image/svg%2bxml;base64,PHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeD0iMCIgeT0iMCIgdmlld0JveD0iMCAwIDEyMi45IDEyMCIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgZW5hYmxlLWJhY2tncm91bmQ9Im5ldyAwIDAgMTIyLjg4IDExOS45NyIgZmlsbD0iI0ZGRkZGRiI+PHBhdGggZD0iTTY5LjggNGMwLTIuMiAyLjItNCA1LTRzNC45IDEuOCA0LjkgNHYxNy44YzAgMi4yLTIuMiA0LTUgNHMtNS0xLjgtNS00VjQuMXpNMTQuNCA3OGgxMS4zYy43IDAgMS4zLjYgMS4zIDEuNHY4LjNjMCAuOC0uNiAxLjMtMS4zIDEuM0gxNC40Yy0uOCAwLTEuMy0uNS0xLjMtMS4zdi04LjNjMC0uOC42LTEuNCAxLjMtMS40em00My40LTIzLjhINjljLjQgMCAuNy4xIDEgLjNhNDAuNCA0MC40IDAgMCAwLTExLjQgMTAuN2gtMWMtLjYgMC0xLjItLjYtMS4yLTEuM3YtOC40YzAtLjcuNi0xLjMgMS4zLTEuM3ptLTIxLjcgMGgxMS4zYy43IDAgMS4zLjYgMS4zIDEuM3Y4LjRjMCAuNy0uNiAxLjMtMS4zIDEuM0gzNi4xYy0uNyAwLTEuMy0uNi0xLjMtMS4zdi04LjRjMC0uNy42LTEuMyAxLjMtMS4zem0tMjEuNyAwaDExLjNjLjcgMCAxLjMuNiAxLjMgMS4zdjguNGMwIC43LS42IDEuMy0xLjMgMS4zSDE0LjRjLS44IDAtMS4zLS42LTEuMy0xLjN2LTguNGMwLS43LjYtMS4zIDEuMy0xLjN6TTM2IDc4aDExLjNjLjcgMCAxLjMuNiAxLjMgMS40djguM2MwIC44LS42IDEuMy0xLjMgMS4zSDM2LjFjLS43IDAtMS4zLS41LTEuMy0xLjN2LTguM2MwLS44LjYtMS40IDEuMy0xLjR6bTY3LjQtMTguNWEzMS40IDMxLjQgMCAxIDEtMjQgNTggMzEuNCAzMS40IDAgMCAxIDI0LTU4ek04Ni42IDg3LjdsMS40LTFWNzNhMi41IDIuNSAwIDAgMSA1IDB2MTMuNmMxIC41IDEuOCAxLjMgMi4yIDIuMmg5LjhhMi41IDIuNSAwIDEgMSAwIDVoLTkuN2E1LjMgNS4zIDAgMSAxLTguNy02em0yMy41LTE3LjNjLTEzLTEzLTM1LTkuMy00Mi41IDdhMjYuMyAyNi4zIDAgMSAwIDQ3LjYtLjRjLTEuMy0yLjYtMy00LjUtNS02LjZ6TTI1LjMgNC4xYzAtMi4zIDIuMi00LjEgNS00LjEgMi43IDAgNSAxLjggNSA0djE3LjhjMCAyLjItMi4zIDQtNSA0LTIuOCAwLTUtMS44LTUtNFY0LjF6TTUuNCAzOC44aDk0LjNWMTguNGMwLS43LS4zLTEuMy0uOC0xLjgtLjQtLjQtMS0uNy0xLjctLjdoLTlhMi43IDIuNyAwIDAgMSAwLTUuNWg5YTggOCAwIDAgMSA4IDh2MzIuNGE0MSA0MSAwIDAgMC01LjYtMS41di01SDUuNnY1Mi45YzAgLjcuMiAxLjMuNyAxLjcuNC41IDEgLjggMS43LjhoNDQuOGMuNSAxLjkgMS4yIDMuNyAyIDUuNUg4YTggOCAwIDAgMS04LThWMTguNGE4IDggMCAwIDEgOC04aDkuNmEyLjcgMi43IDAgMCAxIDAgNS41SDhjLS43IDAtMS4zLjMtMS44LjctLjQuNS0uNyAxLjEtLjcgMS44djIwLjR6bTM3LjctMjNhMi43IDIuNyAwIDAgMSAwLTUuNGgxOC40YTIuNyAyLjcgMCAwIDEgMCA1LjVINDMuMXoiLz48L3N2Zz4=)
```

### npm package

![npm-package-version](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-version.md) ![npm-package-license](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-license.md) ![npm-package-size-unpacked](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-unpacked.md) ![npm-package-size-minified](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-minified.md) ![npm-package-size-minified-gzip](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-size-minified-gzip.md) ![npm-package-dependency-count](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-dependency-count.md) ![npm-package-downloads](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/npm-package-downloads.md)

Badges for an npm package ([react](https://www.npmjs.com/package/react) in this example) using the results from the `npm view` command as well as the [npm registry](https://github.com/npm/registry/blob/master/docs/download-counts.md) and [Bundlephobia](https://bundlephobia.com/) APIs.

```yml
name: Create npm package badges
on: [push]
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
      - name: Build-A-Badge npm package
        uses: peterrhodesdev/build-a-badge@v1.2.1
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
          color: ("blue" "yellow" "purple" "orange" "green" "red" "")
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
