# 📦 Resource

The purpose of the 📦 [Resource][Resource] plugin is to provide a basic definition and process for loading external packages. A simple list of files separated by semicolons is sufficient for initialization. The plugin is not capable of completely independent operation, as the loading process is specific to a particular scenario. Although it is possible to create a new class from the plugin, it is recommended to simply use it, with the parent plugin that controls the process step taking care of the loading and checking of the loading status.

## Definition

1. In the plugin, define the resource object in init as follows (listing shortened to the init function):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    const filename = 'marked.min.js;LICENSE-marked.md';
    TI.RES_MARKED = new Resource('MARKED', undefined, STO_DATA, filename);

    super.init();
  }

  onETShowChapterResolutions(r) {
    if (!window.marked)
      r.result = this.RES_MARKED?.init(r.result);

    r.result = (!r.content || r.content.length == 0) ? r.result : r.result.then(() => r.content = marked.parse(r.content));
  }
```

## Meaning of elements

- const filename - a list of package files separated by semicolons. Paths are relative to the base directory of the repository. Can be taken from the plugin configuration.
- this.RES_MARKED?.init initializes the resource (loads **js** and **css** files from the list)

## Creating a plugin instance

new Resource('MARKED', undefined, STO_DATA, filename):

| Parameter | Default | Description |
|---|---|---|
| aliasName | required | Plugin ID. Define an alias that will be used as the name of this resource/package in the [object explorer][oexplorer] |
| data | required | Enter undefined. This is configuration data - key value. The plugin does not expect any configuration |
| source | STO_DATA | Name of the source data file. Values: STO_DATA (application), STO_HELP (help/data file) |
| fileList | '' | List of files separated by semicolons |

The example creates an instance of the plugin 📦 [Resource][Resource] named MARKED, without configuration. It searches for data in the application data (**data.zip**). The package contains files from fileList.

## Resource plugin functions

The Resource plugin encapsulates:

- calculating the total size of the listed files
- loading and removing loaded files
- finding the readme and license files ([object explorer][oexplorer] uses them in the detail page of this type of resource, if they exist in the list)

## Implementation examples

Examples of implementations of this plugin differ in individual implementations, primarily in terms of the moment of introduction and checks to see if the plugin is already introduced.

- 🖼️ [pTRParseMd][pTRParseMd] - Conversion of Markdown files to HTML output
- 🖼️ [pTRParsePrism][pTRParsePrism] - Syntax highlighting in code listings
- 🖼️ [pTRParseMermaid][pTRParseMermaid] - Rendering Mermaid graphs from text definitions

Translated with DeepL.com (free version)

[Resource]: :_plg:Resource.md "Resource"
[oexplorer]: oexplorer.md "Object explorer"
[pTRParseMd]: :_plg:pTRParseMd.md "pTRParseMd"
[pTRParsePrism]: :_plg:pTRParsePrism.md "pTRParsePrism"
[pTRParseMermaid]: :_plg:pTRParseMermaid.md "pTRParseMermaid"
