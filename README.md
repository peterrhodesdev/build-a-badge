# Build-A-Badge

Creates dynamic and customizable README badges using [shields.io/endpoint](https://shields.io/endpoint) without any extra steps or configuration required.

- [Usage](#usage)
- [Input Parameters](#input-parameters)

## Usage

Add a step to your workflow:

```yml
- name: Build-A-Badge
  uses: peterrhodesdev/build-a-badge@v1.1.0
  with:
    filename: my-badge
    label: "my"
    message: "badge"
```

Display the badge in your README:

```markdown
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/<owner>/<repo>/<filename>.md)
```

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
| logoSvg | no | | An SVG string containing a custom logo. |
| style | no | flat | The default template to use. |
