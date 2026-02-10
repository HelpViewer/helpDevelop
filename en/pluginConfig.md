# ⚙️ Plugin configuration

The application automatically ensures that the configuration is copied to individual plugin instances when they are loaded.

The location is searched for in the same data file from which the plugin is loaded (application or help file):  

- **zip/plugins-config/[class name]_[instance name].cfg** (in the application data)
- **plugins-config/[class name]_[instance name].cfg** (in the basic help data **Help-.zip** or **root directory without language**)

If it exists, it is loaded and passed to the plugin instance. If it does not exist, the values are pre-filled with the logic and values of the **DEFAULT_KEY_CFG_** constants.

## Format rules

- > [!WARNING] This format is very strict, please follow the rules exactly.
- One line = one item
- Line breaks in the middle of a definition are not allowed, even for values
- In case of duplicate key names, the last defined value is always copied
- In the case of multi-value enumerations, the enumeration of values is listed on a single line and the separator is usually **;**. Each plugin handles the processing and division of values itself (it can therefore have its own separator, but it is recommended to avoid the **|** separator)

## File structure

```text
[1]| [2]
```

## Position description

| Position | Description |
|---|---|
| `[1]` | Configuration key name |
| `[2]` | Configuration key value |
