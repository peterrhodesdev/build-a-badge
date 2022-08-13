# Build-A-Badge

[![latest-release](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-latest-release-badge.md&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIiBmaWxsPSIjRkZGIj48IS0tISBGb250IEF3ZXNvbWUgUHJvIDYuMS4yIGJ5IEBmb250YXdlc29tZSAtIGh0dHBzOi8vZm9udGF3ZXNvbWUuY29tIExpY2Vuc2UgLSBodHRwczovL2ZvbnRhd2Vzb21lLmNvbS9saWNlbnNlIChDb21tZXJjaWFsIExpY2Vuc2UpIENvcHlyaWdodCAyMDIyIEZvbnRpY29ucywgSW5jLi0tPjxwYXRoIGQ9Ik00OCAzMmgxNDkuNWMxNyAwIDMzLjIgNi43IDQ1LjIgMTguOGwxNzYgMTc1LjljMjUgMjUgMjUgNjUuNiAwIDkwLjZMMjg1LjMgNDUwLjdjLTI1IDI1LTY1LjYgMjUtOTAuNiAwbC0xNzYtMTc2QTYzLjggNjMuOCAwIDAgMSAwIDIyOS41VjgwYTQ4IDQ4IDAgMCAxIDQ4LTQ4em02NCAxNDRhMzIgMzIgMCAxIDAgMC02NCAzMiAzMiAwIDAgMCAwIDY0eiIvPjwvc3ZnPg==)](https://github.com/peterrhodesdev/build-a-badge/actions?query=workflow%3Abuild-a-badge-badges) [![license](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-license-badge.md)](https://github.com/peterrhodesdev/build-a-badge/blob/main/LICENSE) [![marketplace](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/build-a-badge-marketplace-badge.md)](https://github.com/marketplace/actions/build-a-badge)

GitHub Action to create dynamic and customizable README badges using [shields.io/endpoint](https://shields.io/endpoint).

This is achieved by storing the required JSON data of the badge in the repository's Wiki. Nothing is committed or pushed to the main repository, and there are no external dependencies that require configuring.

The only requirement is to have at least one page in the Wiki so that it can be cloned. See [here](https://docs.github.com/en/communities/documenting-your-project-with-wikis/adding-or-editing-wiki-pages) for instructions on how to add wiki pages.

- [Usage](#usage)
- [Input Parameters](#input-parameters)
- [Examples](#examples)

## Usage

Add a step to your workflow:

```yml
- name: Build-A-Badge
  uses: peterrhodesdev/build-a-badge@v1.1.1
  with:
    filename: my-badge
    label: "my"
    message: "badge"
```

Display the badge in your README:

```markdown
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/<owner>/<repo>/<filename>.md)
```

[![my-badge](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/my-badge.md)](https://github.com/peterrhodesdev/build-a-badge/actions?query=workflow%3Amy-badge)

> The JSON badge data is stored in the wiki section of the repo in a file called `<filename>.md`. By default the name of the workflow will be used as the `filename` parameter. The username and email of the user who performed the last commit will be used as the details for the commit to the wiki.

## Input Parameters

See [shields.io/endpoint](https://shields.io/endpoint) for a list of supported values for the parameters.

| Name | Is required? | Default value | Description |
| --- | --- | --- | --- |
| filename | no | ${{ github.workflow }} | The filename to use in the wiki for storing the JSON badge data. The default value is the name of the workflow that runs the action. Because of this, the file name will need to be specified when creating multiple badges per workflow. |
| label | yes | | The left text. |
| message | yes | | The right text. |
| color | no | lightgrey | The right color. |
| labelColor | no | grey | The left color. |
| namedLogo | no | | Logo supported by Shields. |
| style | no | flat | The default template to use. |

## Examples

### Custom logo

[![last-commit-badge](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/peterrhodesdev/build-a-badge/last-commit-badge.md&logo=data:image/svg%2bxml;base64,PHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeD0iMCIgeT0iMCIgdmlld0JveD0iMCAwIDEyMi45IDEyMCIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgZW5hYmxlLWJhY2tncm91bmQ9Im5ldyAwIDAgMTIyLjg4IDExOS45NyIgZmlsbD0iI0ZGRkZGRiI+PHBhdGggZD0iTTY5LjggNGMwLTIuMiAyLjItNCA1LTRzNC45IDEuOCA0LjkgNHYxNy44YzAgMi4yLTIuMiA0LTUgNHMtNS0xLjgtNS00VjQuMXpNMTQuNCA3OGgxMS4zYy43IDAgMS4zLjYgMS4zIDEuNHY4LjNjMCAuOC0uNiAxLjMtMS4zIDEuM0gxNC40Yy0uOCAwLTEuMy0uNS0xLjMtMS4zdi04LjNjMC0uOC42LTEuNCAxLjMtMS40em00My40LTIzLjhINjljLjQgMCAuNy4xIDEgLjNhNDAuNCA0MC40IDAgMCAwLTExLjQgMTAuN2gtMWMtLjYgMC0xLjItLjYtMS4yLTEuM3YtOC40YzAtLjcuNi0xLjMgMS4zLTEuM3ptLTIxLjcgMGgxMS4zYy43IDAgMS4zLjYgMS4zIDEuM3Y4LjRjMCAuNy0uNiAxLjMtMS4zIDEuM0gzNi4xYy0uNyAwLTEuMy0uNi0xLjMtMS4zdi04LjRjMC0uNy42LTEuMyAxLjMtMS4zem0tMjEuNyAwaDExLjNjLjcgMCAxLjMuNiAxLjMgMS4zdjguNGMwIC43LS42IDEuMy0xLjMgMS4zSDE0LjRjLS44IDAtMS4zLS42LTEuMy0xLjN2LTguNGMwLS43LjYtMS4zIDEuMy0xLjN6TTM2IDc4aDExLjNjLjcgMCAxLjMuNiAxLjMgMS40djguM2MwIC44LS42IDEuMy0xLjMgMS4zSDM2LjFjLS43IDAtMS4zLS41LTEuMy0xLjN2LTguM2MwLS44LjYtMS40IDEuMy0xLjR6bTY3LjQtMTguNWEzMS40IDMxLjQgMCAxIDEtMjQgNTggMzEuNCAzMS40IDAgMCAxIDI0LTU4ek04Ni42IDg3LjdsMS40LTFWNzNhMi41IDIuNSAwIDAgMSA1IDB2MTMuNmMxIC41IDEuOCAxLjMgMi4yIDIuMmg5LjhhMi41IDIuNSAwIDEgMSAwIDVoLTkuN2E1LjMgNS4zIDAgMSAxLTguNy02em0yMy41LTE3LjNjLTEzLTEzLTM1LTkuMy00Mi41IDdhMjYuMyAyNi4zIDAgMSAwIDQ3LjYtLjRjLTEuMy0yLjYtMy00LjUtNS02LjZ6TTI1LjMgNC4xYzAtMi4zIDIuMi00LjEgNS00LjEgMi43IDAgNSAxLjggNSA0djE3LjhjMCAyLjItMi4zIDQtNSA0LTIuOCAwLTUtMS44LTUtNFY0LjF6TTUuNCAzOC44aDk0LjNWMTguNGMwLS43LS4zLTEuMy0uOC0xLjgtLjQtLjQtMS0uNy0xLjctLjdoLTlhMi43IDIuNyAwIDAgMSAwLTUuNWg5YTggOCAwIDAgMSA4IDh2MzIuNGE0MSA0MSAwIDAgMC01LjYtMS41di01SDUuNnY1Mi45YzAgLjcuMiAxLjMuNyAxLjcuNC41IDEgLjggMS43LjhoNDQuOGMuNSAxLjkgMS4yIDMuNyAyIDUuNUg4YTggOCAwIDAgMS04LThWMTguNGE4IDggMCAwIDEgOC04aDkuNmEyLjcgMi43IDAgMCAxIDAgNS41SDhjLS43IDAtMS4zLjMtMS44LjctLjQuNS0uNyAxLjEtLjcgMS44djIwLjR6bTM3LjctMjNhMi43IDIuNyAwIDAgMSAwLTUuNGgxOC40YTIuNyAyLjcgMCAwIDEgMCA1LjVINDMuMXoiLz48L3N2Zz4=)](https://github.com/peterrhodesdev/build-a-badge/actions?query=workflow%3Alast-commit-badge)

Display the last commit date for the repository using a custom logo.

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
        uses: peterrhodesdev/build-a-badge@v1.1.1
        with:
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
