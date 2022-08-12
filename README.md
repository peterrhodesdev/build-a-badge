# Build-A-Badge

Creates dynamic and customizable README badges using [shields.io/endpoint](https://shields.io/endpoint) without any extra steps or configuration required.

- [Usage](#usage)
- [Input Parameters](#input-parameters)

## Usage

Add a step to your workflow:

```yml
- name: Build-A-Badge
  uses: peterrhodesdev/build-a-badge@v1.0.2
  with:
    filename: test-badge
    label: "left text"
    message: "right text"
    color: blue
```

Display the badge in your README:

```markdown
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/<owner>/<repo>/test-badge.md)
```

> The JSON badge data is stored in the wiki section of the repo in a file called `<filename>.md`. The username and email of the user who performed the last commit will be used as the details for the commit to the wiki.

## Input Parameters

| Name | Is required? | Default value | Description |
| --- | --- | --- | --- |
| filename | no | ${{ github.workflow }} | The filename to use in the wiki for storing the JSON badge data. The default value is the name of the workflow that runs the action. Because of this, the file name will need to be specified when creating multiple badges per workflow. |
| label | yes | | The left text of the badge. |
| message | yes | | The right text of the badge. |
| color | no | lightgrey | The right color of the badge. See [shields.io/endpoint](https://shields.io/endpoint) for a list of supported values. |

