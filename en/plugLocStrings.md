# 🌐 Plugin localization

## Using the localization string

Anywhere in the plugin code, this call:

```javascript
_T('LocalizationKey');
_T('LocalizationKey', { dynamicValue: 'test'});
```

**\_T** will print the value of the localization key **LocalizationKey**. If the value is missing, the key name will be printed with underscores \_LocalizationKey\_ (in markdown output, it will be displayed in italics without underscores - _LocalizationKey_).

The second parameter (object) is used to pass dynamic values that can be inserted into the string.

The chapter 🌐 [New language for Viewer][ViewerNewLang] further describes:

- the structure and meaning of the main localization files,
- their location,
- the format of localization keys, which is automatically mapped to HTML objects according to the match between the id and property name and the key name.

## Separate localization dictionary for the plugin

Using the 🔌 [pServiceLocalization][pServiceLocalization] plugin (part of the basic package), you can add your own localizations for each plugin. Just create the appropriate files in the right place.

Required files:

- **lstr.txt** – fixed texts
- **lstr.js** – dynamic strings (contain variables, compose texts on the fly)

Structure

- Files are stored according to language codes (cs, en, ...).
- The directory tree for each language is shown in the following chapters.
- 🛈 The browser data and help data directory trees differ because they are based on different internal loading processes.

Further information

- A detailed description of the structure and format of localization files can be found in the chapter 🌐 [New language for Viewer][ViewerNewLang].

Description of activity

- When a plugin instance is loaded, its localization dictionary is loaded from the relevant files and added to the already loaded localization.
- When changing the language, the main localization dictionary is loaded first, followed by the dictionaries according to the [loading order][OELoadOrder] of the individual plugin instances.
- In case of key name collisions, the last loaded value takes precedence, as it overwrites all previous ones.

### In browser data

```treeview
HelpViewer/
    zip/
        plugin-class-name/
            cs/
                lstr.js
                lstr.txt
            en/
                lstr.js
                lstr.txt
```

### In help data

```treeview
helpProject/
    cs/
        plugin-class-name/
            lstr.js
            lstr.txt
    en/
        plugin-class-name/
            lstr.js
            lstr.txt
```

[ViewerNewLang]: newLangViewer.md#h-3-1 "New language for Viewer"
[pServiceLocalization]: :_plg:pServiceLocalization.md "pServiceLocalization"
[OELoadOrder]: :_/LORDER.md "Loading order"
