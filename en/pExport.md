# 🖼️ pExport

## Purpose of the plugin

This plugin defines the basic interface for exporting the displayed text of a chapter.

The derived plugin is usually encapsulated logic between:

- **HelpViewer** (🖥️ [puiButtonExport][puiButtonExport]) and
- a converter from **HTML** to the desired format, which is usually handled by an external script. 

If necessary, the plugin 📦 [Resource][resource] will load the converter.

## Implementation

1. A new plugin will always have 🖼️ [pExport][pExport] as its base class.
2. The implementation will look something like this:

```javascript
class pExportNEW extends pExport {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.RES_HTMLTONEW = new Resource('HTMLTONEW', undefined, STO_DATA, 'HTMLToNEW/HTMLToNEW.js;HTMLToNEW/LICENSE;HTMLToNEW/README.md');
  }
  
  async onETPrepareExport(evt) {
    let promise = Promise.resolve(true);

    if (typeof HTMLTONEW !== 'function')
      promise = this.RES_HTMLTONEW?.init(promise);

    promise = promise.then(async() => {
      const ctx = { listStack: [], i_img: 0, i_svg: 0, embeds: evt.embeds };
      const converted = HTMLTONEW(evt.parent, ctx);
      evt.output.file('output.txt', converted);
  
      if (evt.doneHandler)
        evt.doneHandler();

    });
  }
}

Plugins.catalogize(pExportNEW);
```

3. The new plugin must be added to the 📄 [list of plugins][pluginslst]:

```
pExportNEW:NEW
```

in an order that is lower than **pExport** in the list.

The ID after the colon (here NEW) will be offered in the drop-down list of the 📥 Export button.

## Functionality description

- The user clicks on the 📥 Export button
- The button handler creates a ZIP archive and collects images and other nested elements found in the text into it and sends the data as a link to the chapter text or handler **doneHandler**, which ensures that the ZIP file is displayed to the user
- The button handler sends the event ⚡ [PrepareExport][PrepareExport]
- The derived plugin (**pExportNEW**) defines the handler 👂 **onETPrepareExport**, which takes over the prepared intermediate result
- The export handler (which may be asynchronous) works primarily with:
  - **evt.embeds** - embedded elements, images, SVG
  - **evt.parent** - parent HTML object (display area for chapter text)
- The export handler calls the converter function, which passes the necessary context object with empty or default values, a reference to the HTML object containing the complete input, or additional input depending on the implementation
- The export handler takes the conversion result and calls **evt.output.file('name.txt', result);** to write to the ZIP output
- Finally, the export handler calls **evt.doneHandler();**. This releases the ZIP file to the user's browser for standard download

## Pre-export conversion

In the case of some plugins (naming convention in the **pExtension**\* system - for example: 🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions]), it can be assumed that they perform a transformation into HTML code that general **HTMLTo**\* (**HTMLToMD**, **HTMLToTeX**) converters do not recognize.

### Procedure

1. In the derived class **pExport**\* in **onETPrepareExport**, the variable **corrections** (array) will be defined, which will record future changes in the DOM structure of the chapter text.
2. Trigger the event ⚡ [PreExportCorrection][PreExportCorrection] with **x.temporaryObjects** linked to **corrections**
3. Calls to **onET_PreExportCorrection** will be made on plugins and the outputs from **pExtension**\* plugins will be converted according to the type of export format being prepared - the extension plugin will transform its conversion back into a simplified output for the **HTMLTo**\* converter.
4. **corrections** will contain elements created by the conversion
5. The conversion from HTML to the desired format will be called
6. Go through **corrections** in a loop and delete all contained elements - temporary edits will be cleared from the visible input.

### Sample implementation

```javascript
  //...
  async onETPrepareExport(evt) {
    //...
    promise = promise.then(async() => {
      //...
      const corrections = [];
      sendEvent(EventNames.PreExportCorrection, (x) => {
        x.exportType = this.aliasName;
        x.parent = evt.parent;
        x.temporaryObjects = corrections;
      });

      const converted = HTMLTONEW(evt.parent, ctx);
      corrections.forEach(x => x.remove());
      //...
    }
  }
```

The event ⚡ [PreExportCorrection][PreExportCorrection] has a handler on the side of 🧩 [pExtension][pExtension]\*, which ensures point 3 [Procedure][H30].

## Implementation examples

- 🖼️ [pExportHTM][pExportHTM] and other descendants of the class 🖼️ [pExport][pExport] whose names begin with **pExport**.
- Converters: [HTMLToTeX][HTMLToTeX], [HTMLToMD][HTMLToMD]

[puiButtonExport]: :_plg:puiButtonExport.md "puiButtonExport"
[pExportHTM]: :_plg:pExportHTM.md "pExportHTM"
[pExtension]: pExtension.md#h-3-0 "pExtension"
[pExtensionMarkedAdmonitions]: :_plg:pExtensionMarkedAdmonitions.md "pExtensionMarkedAdmonitions"
[PrepareExport]: :_evt:PrepareExport.md "PrepareExport"
[PreExportCorrection]: :_evt:PreExportCorrection.md "PreExportCorrection"
[pExport]: :_plg:pExport.md "pExport"
[resource]: resource.md "Resource"
[pluginslst]: plugins.lst.md "List of plugins (plugins.lst)"
[HTMLToTeX]: https://github.com/HelpViewer/HTMLToTeX "HTML -> TeX"
[HTMLToMD]: https://github.com/HelpViewer/HTMLToMD "HTML -> md"
[H30]: #h-3-0 "Postup"
