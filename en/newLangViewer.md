# 🌐 New language for Viewer

- For a new Viewer language, you need to create a new directory with the language abbreviation in [localization repository][Localiz] at the main level.
- Select the abbreviation according to the **ISO 639-1** standard.
- Your language translation for **HelpViewer** will be automatically distributed with the next release after PR approval.

## The meaning of files in localization

- Create all files in the **UTF-8 no BOM (65001)** character set.

| File | Meaning |
|---|---|
| lname.txt | The name of the language in the language. E.g. Español in Spanish |
| lstr.js | Keys containing dynamic information. |
| lstr.txt | Keys with static texts. |

## File structure

### lstr.js

```javascript
var _lstr = {
  'key' : () => `value ${global-variable}`,
}; 
```

### lstr.txt

```
key(html element id)|value
key(html element id)__placeholder|input field title before entering it by cursor
key(html element id)__aria-label|accessibility text
key(html element id)__*|value HTML element attribute named *
```

[Localiz]: https://github.com/HelpViewer/Translations "HelpViewer localization"
