# 📄 List of plugins (plugins.lst)

- ⚠️ This format is very strict, please follow the rules exactly.
- The file defines the list and order of JavaScript files with plugin-organized code that the application will load.
- One line = one item
- Line breaks in the middle of a definition are not allowed

## Location

- Application data file: zip/plugins.lst
- Help file: helpProject/_base/plugins.lst

## File structure

```text
[1]
[1]:
[1]:[2]
[1]:[2];[2]
```

## Position descriptions

| Position | Description |
|---|---|
| `[1]` | Relative path to the file without the extension relative to the root of the data storage. |
| `[2]` | Name of the plugin instance (id). |

## Description of definitions

| Definition | Description |
|---|---|
| `[1]` | The plugin is only loaded into memory. Suitable for plugins from which other plugins are derived, but which are not intended to be active in the application themselves. |
| `[1]:` | The plugin is loaded and loaded with id ''. |
| `[1]:[2]` | The plugin is loaded and loaded with id [2]. |
| `[1]:[2];[2]` | The plugin is loaded and loaded in multiple instances. The order of loading and use of id is according to definitions [2]. |

## Additional features

- When loading each instance, the system automatically checks whether there is a separate configuration for the plugin instance. The file name is always: **plugins-config/\[1\]_\[2\].cfg**. If \[2\] is not specified, then the name **plugins-config/\[1\]_.cfg** is used.
