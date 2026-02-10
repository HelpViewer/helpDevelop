# 📄 List of external dependencies (deps.lst)

- > [!WARNING] This format is very strict, please follow the rules exactly.
- The file defines a list of external files or packages that the CI script will attach to the release package.
- One line = one item
- Line breaks in the middle of a definition are not allowed

## File structure

```text
[1]|[2][|]
```

## Position descriptions

| Position | Description |
|---|---|
| `[1]` | File name on the application package side |
| `[2]` | File name on the external file/package source side |
| `[\|]` | If the line ends with a vertical bar, it is copied to the **hvdata** directory, otherwise the file is placed in **hvdata/data.zip**. |
