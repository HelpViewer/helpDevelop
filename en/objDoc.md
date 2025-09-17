# 📑 Documenting objects

To maintain the clarity of the application and plugins, it is recommended that new objects always be documented whenever possible.

In HelpViewer, documentation is organized as a tree of objects and automatic lists with the option to click through to a detailed page. Everything is controlled by 🧩 [object browser][oexplorer], which displays content according to the current state of the system. On individual pages, it can then supplement information from manually prepared documentation (if available), thereby expanding automatically generated chapters.

This manual documentation can be expanded in the [helpInternalRef][RhelpInternalRef] repository (zip/i directory in the HelpViewer project). This repository becomes part of the released package and has a structure corresponding to a standard help file. The format and preparation procedure are described in the [author documentation][AuthDoc].

Within this special help, you only add .md files. There is no need to deal with the tree or indexes, as they are dynamically created by the 🧩 [object explorer][oexplorer] according to the state of the system.

## Naming convention for descriptive documents

General location structure:  
**i/(language, ISO 639-1 abbreviation)/(object type abbreviation)_(plugin class name)\_(plugin instance name)\_(object name).md**

If you have problems with text not displaying, you can also obtain the exact expected location from the **browser dev console** messages (Warning level, message starts with: 'ObjectExplorer: requested path:').

In the examples, the **en** subdirectory represents the language.

| Object type | Full path example and description |
|---|---|
| Plugin group | **i/en/grp_UI.md** (UI can be replaced by any other group from the [group list][oexplorerGrp] in the object browser) |
| 🧩 Plugin class | **i/en/plg_pColorTheme.md** (pColorTheme is the name of the plugin class) |
| 🔹 Plugin instance | **i/en/oeod_inst_puiButtonKeywordIndex_keywordList.md** (puiButtonKeywordIndex is the name of the plugin class, keywordList is the name of the instance or is not specified if aliasName (id) is empty) |
| ⚡ Event | **i/en/event_PluginsDump.md** (PluginsDump is the name of the event) |
| ⚡ Event field | **i/en/p_PluginsDump_createdAt.md** (PluginsDump is the name of the event, createdAt is the name of the field)  |
| ⚡ Event field (backup description across documentation) | **i/en/p__createdAt.md** (createdAt is the field name, there are two underscores in the path, leave these) |
| ⚙️ Configuration option | **i/en/cfgopt_puiButtonKeywordIndex_keywordList_CAPTION.md** (puiButtonKeywordIndex is the name of the plugin class, keywordList is the name of the plugin instance, CAPTION is the name of the configuration key on the code side) |
| 🛰️ [Event sending][eventTra] | **i/en/transmitter_puiSidebar_sidebar_ClickHandlerRegister.md** (puiSidebar is the name of the plugin class, sidebar is the name of the plugin instance, ClickHandlerRegister is the name of the transmitted event) |
| 📦 Source/Package | **i/en/res_pTRParseMd_-md_MARKED.md** (pTRParseMd is the name of the plugin class, -md is the name of the instance, MARKED is the name of the source) [Source][resource] may have additional descriptive information. |
| 👂 Event handler | **i/en/hdl_puiButtonKeywordIndex_keywordList_onETIndexFileLoaded.md** (puiButtonKeywordIndex is the name of the plugin class, keywordList is the name of the plugin instance, onETIndexFileLoaded is the full name of the event handler function on the code side) |
| 🔘 UI element | **i/en/uiobject_puiButtonKeywordIndex_keywordList_downP-Glossary.md** (puiButtonKeywordIndex is the name of the plugin class, keywordList is the name of the plugin instance, downP-Glossary is the id of the html element id of the element) |
| ⭐ Javascript event | **i/en/sysevent_pConvertSysEventToEvent_pPrePrintEvent_window.beforeprint.md** (pConvertSysEventToEvent is the name of the plugin class, pPrePrintEvent is the name of the plugin instance, window is the name of the HTML element to which the handler was attached, beforeprint is the name of the Javascript event) |
| ⇄ Integrated process | **i/en/grpproc_fulltextList.md** (toc is the name of the integrated process - the name of the plugin instance) |
| 📄 Source code listing | **i/en/cpp_pIndexFile.md** (pIndexFile is the name of the plugin class) |
| 🏷️ Class function | **i/en/method_pIndexFile_keywordList_init.md** (pIndexFile is the name of the plugin class, keywordList is the name of the plugin instance, init is the name of the function) |

## Convention for linking to documentation from external help

⚠️ For the links to work and the chapter to be displayed, the [object browser][oexplorer] must be open before accessing the data within the session. Indexing always takes place when the tree tab of this plugin is opened.

General link path structure:  
**:(object type):(plugin class name):(plugin instance name):(object name).md**

| Object type | Link path example |
|---|---|
| Plugin group | **:_grp:UI.md** |
| 🧩 Plugin class | **:_plg:pTopicRenderer.md** |
| 🔹 Plugin instance | **:_inst:pIndexFile:fulltextList.md** |
| ⚡ Event including handler | **:_evt:DebugEventEvent.md** |
| 📄⚡ Event without handler | **:_evtD:DebugEventEvent.md** |
| ⚙️ Configuration option | **:_cfg:pIndexFile:keywordList:FILENAMEKW.md** |
| 📄⚙️ Configuration option ([dynamic][cfgDyn]) | **:_cfgE:puiButtonObjectExplorer:-load:RENDER-F.md** |
| 🛰️ [Event sending][eventTra] | **:_tra:puiSidebar:sidebar:ClickHandlerRegister.md** |
| 📦 Source/Package | **:_res:pTRParseMermaid:-connected:MERMAID.md** |
| 👂 Event handler | **:_hdl:puiHeader:header:onETButtonSend.md** |
| 🔘 Button | **:_btn:puiButtonVersionSearch::downP-ChangeVersion.md** |
| 🎛️ Card | **:_page:puiButtonObjectExplorer:-load:oexpP.md** |
| 📂 Tree | **:_tree:puiButtonObjectExplorer:-load:objectList.md** |
| ⭐ Javascript event | **:_evtSys:pConvertSysEventToEvent:pPrePrintEvent:window.beforeprint.md** |
| ⇄ Integrated process | **:_grpproc:fulltextList.md** |
| 📄 Source code listing | **:_cpp:pui.md** |
| 🏷️ Class function | **:_fn:pIndexFile:keywordList:init.md** |

The documentation for authors describes how to [add a link to the chapter text][AuthDocLinks].

### Obtaining the path to an object from the object browser

1. Open 🧩 [object browser][oexplorer].
2. Find the desired object:
   - in the **object tree** 
   - or by entering it in the **search bar** and pressing **Enter**
3. Open the browser's dev tools.
4. Activate **Select element** and click on the corresponding **a** object.
5. In the **data-param** attribute, you will find the full path to the object.

[RhelpInternalRef]: https://github.com/HelpViewer/helpInternalRef "HelpViewer documentation for system objects"
[AuthDoc]: ?d=hlp-aguide/Help-__.zip "Documentation for authors"
[oexplorer]: oexplorer.md "Object browser"
[oexplorerGrp]: :_cfg:puiButtonObjectExplorer:-load:GROUPSLIST.md "List of groups in the object explorer"
[resource]: resource.md#h-2-3 "Resource - further information"
[cfgDyn]: cfgopt.md#h-2-1 "Dynamic configuration keys"
[eventTra]: event.md#h-2-2 "Sending an Event"
[AuthDocLinks]: ?d=hlp-aguide/Help-__.zip&d=hlp-aguide/Help-__.zip&p=links.md#h-3-0 "Links in texts"
