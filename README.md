<p align="center">
  <a href="https://github.com/marocchino/tool-versions-action"><img alt="GitHub Actions status" src="https://github.com/marocchino/tool-versions-action/workflows/test-local/badge.svg"></a>
</p>

## Usage

### Pre-requisites

Create a workflow `.yml` file in your repositories `.github/workflows` directory. An [example workflow](#example-workflow) is available below. For more information, reference the GitHub Help Documentation for [Creating a workflow file](https://help.github.com/en/articles/configuring-a-workflow#creating-a-workflow-file).

### Inputs

- `path` - path of .tool-versions file, `.tool-versions` by default

### Outputs

Basically, It could be any values depending on your `.tool-versions`.
You can find full asdf plugins list on [here](https://github.com/asdf-vm/asdf-plugins).

### Example workflow

```yaml
name: Get version info from tool-versions

on: push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - name: Read .tool-versions
        uses: marocchino/tool-versions-action@v1
        id: versions
      - name: Use Node.js ${{ steps.versions.outputs.nodejs }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ steps.versions.outputs.nodejs }}
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: ${{ fromJSON(steps.versions.outputs.hugo).version }}
          extended: ${{ fromJSON(steps.versions.outputs.hugo).is_extended }}
```

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
