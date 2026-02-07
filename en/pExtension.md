# 🧩 pExtension

Plugins with the prefix **pExtension**\* extend the existing functionality of the system or external libraries.

## Naming convention

For example:
🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions]

| Part | Meaning | Example |
| --- | --- | --- |
| **pExtension** | extension | **pExtension** |
| **Marked** | what for? | **marked.js** - external library rendering markdown |
|  **Admonitions**| what does it provide? | **highlighted blocks** |

(same library = one common prefix and part of common logic in ancestor **pExtensionMarked**)

## Implementation

1. A new plugin will always have 🧩 [pExtension ("something")][pExtension] as its base classn not **pExtension** directly.
2. The implementation varies greatly depending on the element it will extend. Follow the steps in the chapter 🧩 [first plugin][firstPlugin]
3. The new plugin must be added to 📄 [plugin list][pluginslst] as follows:

```
pExtensionMarked
pExtensionMarkedAdmonitions:
```

in an order that is lower than **pExtension** in the list.

## Possible responsibilities

These plugins may have responsibilities that are discussed in the following subchapters.

### Pre-export conversion

In the case of some plugins, it can be assumed that they perform a transformation into HTML code that general **HTMLTo**\* (**HTMLToMD**, **HTMLToTeX**) converters do not recognize.

Therefore, the plugin side must define the handling of the **onET_PreExportCorrection** event ⚡ [PreExportCorrection][PreExportCorrection], with its **x.temporaryObjects** linked to **corrections** at the point of the export request. **This plugin is responsible for the export output method.** It receives the export type from the call data. It should also provide a backup handler for new or unknown formats (**\***).

Handler example:

```javascript
  onET_PreExportCorrection(e) {
    if (!e || !e.parent) return;

    const cssClass = this.cfgROOTCSSCLASS;
    const willBeUpdated = [...$A(`.${cssClass}`, e.parent)];
    const exportFormatting = new Map([
      ['MD', (id) => `> [!${id}]`],
      ['TEX', (id) => `<strong>[!${id}]</strong> `],
      ['*', (id) => ''],
    ]);
    
    willBeUpdated.forEach(x => {
      const typeClass = x.className.split(' ').filter(Boolean).find(c => c.startsWith(cssClass) && c !== cssClass) || '';
      if (typeClass) {
        const correctionText = (exportFormatting.get(e.exportType) || exportFormatting.get('*'))?.(typeClass.toUpperCase().substring(cssClass.length + 1));
        if (correctionText) {
          const correction = document.createElement('span');
          correction.className = e.CSSClassName;
          correction.innerHTML = correctionText;

          x.prepend(correction);
          e.temporaryObjects.push(correction);
          e.manipulatedObjects.push(x);  
        }
      }
    });
  }
```

(🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions])

## Příklady implementací

- 🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions], 🧩 [pExtensionMarked][pExtensionMarked], and other descendants of the class 🧩 [pExtension][pExtension] whose names begin with **pExtension**.

[pExtension]: :_plg:pExtension.md "pExtension"
[pExtensionMarkedAdmonitions]: :_plg:pExtensionMarkedAdmonitions.md "pExtensionMarkedAdmonitions"
[pExtensionMarked]: :_plg:pExtensionMarked.md "pExtensionMarked"
[firstPlugin]: firstPlugin.md "První plugin"
[pluginslst]: plugins.lst.md "Seznam pluginů (plugins.lst)"
[PreExportCorrection]: :_evt:PreExportCorrection.md "PreExportCorrection"
