# 🧩 First plugin

## Plugin creation process

To develop a new plugin, you need to do the following:

1. Define exactly what the plugin should do. Choose a parent for the plugin (**extends**) that is suitable for the given purpose. The content of the plugin will at least correspond to the minimum plugin - **IPlugin**.

### Help package

If you want to add the plugin to the help, then:

2. Create the following files in the help repository in the **_base** directory:
   - **plugins.lst** (list of plugins),
   - **plugins** and **plugins-config** directories

and then proceed according to the **Program package** chapter.

### Program package

If you want to add the plugin to the HelpViewer build:

3. Add the plugin to the [plugins list] with a definition line: 
   - **[class name]** if the plugin is only to be loaded (it is a parent for other plugins, but is not intended to work independently)
   - **[class name]:[instance name]** if the plugin is to be loaded and is intended to provide functionality
4. Place the configuration definitions for the new instance in **zip/plugins-config/[class name]_[instance name].cfg**.
5. Place the plugin source code in the location **zip/plugins/[class name].js**.

For help, use the location without **zip/**.

## Minimum plugin

```javascript
class pMinPlugin extends IPlugin {
  constructor(aliasName, data) {
    super(aliasName, data);
  }

  init() {
    //const T = this.constructor;
    //const TI = this;
    
    super.init();
  }

  deInit() {
    super.deInit();
  }
}

Plugins.catalogize(pMinPlugin);

```

- Calling **Plugins.catalogize(pMinPlugin);** is mandatory because it adds the plugin to the catalog of loaded plugins. Subsequently, based on the plugin name, it is possible to request its instance. Based on the data in **[plugins][plugins].lst**, the application does this itself.
- Calling **super.** should be the first in the constructor and the last in init and deinit. They ensure the application of general common logic.
- const T and TI are abbreviations for accessing this and the class. This is a recommended writing concept across the system.
- If you only have a super. call in a function, you can remove the function entirely. Here in the example, everything is listed for a quick general overview.

## Basic plugins

| Name | Description |
|---|---|
| 🔌 [IPlugin][IPlugin] | Basic plugin for all plugins in the system. Provides basic functions for a general plugin. It is intended for service plugins or event listeners that do not provide any user interface elements themselves. |
| 🔌 [pConvertSysEventToEvent][pConvertSysEventToEvent] | The plugin converts a defined JavaScript event into an application event that can be captured by another plugin. |
| 🔌 [pServicePlugin][pServicePlugin] | Plugin for extended services. It is based on handlers connected to plugin events 🔌 [pPluginManagement][pPluginManagement]. |
| 🧩 [pExtension][pExtension] | Plugins with the prefix **pExtension**\* extend the existing functionality of the system or external libraries. They do not have a fixed structure. |

### User interface

| Name | Description |
|---|---|
| 🖥️ [puiButton][puiButton] | 🔘 Button for the user interface. The action handler must be part of the plugin source. |
| 🖥️ [puiButtonTab][puiButtonTab] | 🔘🎛️ Sidebar button and tab. |
| 🖥️ [puiButtonTabTree][puiButtonTabTree] | 🔘🎛️📂 Sidebar button and tab with tree component. |
| 🖥️ [puiButtonSelect][puiButtonSelect] | 🔘▼ Button with a drop-down list. |

### Chapter text rendering

| Name | Description |
|---|---|
| 🖼️ [pTRPhasePlugin][pTRPhasePlugin] | The plugin receives the ⚡ [ShowChapterResolutions][ShowChapterResolutions] event from the 🖼️ [pTopicRenderer][pTopicRenderer] plugin and performs a single step of process handling. One of its applications is, for example, parsing an md file for listing into chapter text. |
| 🖼️ [pExport][pExport] | The plugin receives the event ⚡ [PrepareExport][PrepareExport] from the plugin 🖥️ [puiButtonExport][puiButtonExport] and exports the chapter text to the format according to the implementation of the plugin - descendant. It also defines the event ⚡ [PreExportCorrection][PreExportCorrection], which is mainly used by descendants 🧩 [pExtension][pExtension] when converting their outputs before export. |

## Implementation examples

- 🖼️ [pTREmptyPlugin][pTREmptyPlugin]

[pTREmptyPlugin]: :_cpp:pTREmptyPlugin.md "Empty plugin"
[IPlugin]: :_plg:IPlugin.md "IPlugin"
[pConvertSysEventToEvent]: pConvertSysEventToEvent.md "pConvertSysEventToEvent"
[pTRPhasePlugin]: pTRPhasePlugin.md "pTRPhasePlugin"
[pExport]: pExport.md "pExport"
[ShowChapterResolutions]: :_evt:ShowChapterResolutions.md "ShowChapterResolutions"
[PrepareExport]: :_evt:PrepareExport.md "PrepareExport"
[pTopicRenderer]: pTopicRenderer.md "pTopicRenderer"
[puiButton]: puiButton.md "puiButton"
[puiButtonTab]:puiButtonTab.md "puiButtonTab"
[puiButtonTabTree]: puiButtonTabTree.md "puiButtonTabTree"
[puiButtonSelect]: puiButtonSelect.md "puiButtonSelect"
[plugins]: plugins.lst.md "List of plugins"
[pServicePlugin]: pServicePlugin.md "pServicePlugin"
[pPluginManagement]: :_plg:pPluginManagement.md "pPluginManagement"
[puiButtonExport]: :_plg:puiButtonExport.md "puiButtonExport"
[pExtension]: pExtension.md "pExtension"
[PreExportCorrection]: :_evt:PreExportCorrection.md "PreExportCorrection"
