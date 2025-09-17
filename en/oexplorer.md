# 🧩 Object explorer

HelpViewer includes the **puiButtonObjectExplorer** plugin. This plugin is used to browse the current state of the system and the catalog of links and defined objects.

## Activation

⚠️ The ObjectExplorer plug-in is only loaded if the application is running with **DEBUG_MODE = true** in **hvdata/appmain.js**. Otherwise, no functionality or output is available, and the application returns a "not found" response for the chapters served by the module.

⚠️ If the plugin has not yet been active during the session, some of the functionality from the list of functions will not yet be available when using links.

If the plugin is active, you will see this button on the sidebar:

<button class="pnl-btn" id="downP-ObjectExplorer" title="Object explorer" aria-label="Object explorer">🧩</button>

## Functions

The plugin displays, for example:

- Overview of [groups and supported objects][OEGroups]
- [Dependency tree][OETree] of plugins and events
- [Order][OELoadOrder] of loading [plugin instances][PlgsList]
- Plugins in categories (controlled by plugin configuration)
- Plugins in groups according to common ID (plugins thus form an integrated whole - dictionary of keywords, chapter text rendering procedure, etc.)
- List of elements and objects provided by a specific plugin instance
- List of plugin instance configuration options
- Element documentation, if available (currently mainly in English)
- Information about defined filters and links in the event transfer chain: sender -> handler.

It also supports:

- Searching for an object by its key name with accuracy down to the subordinate plugin definition
- Searching for an object by its type is possible by copying the type symbol (icon) into the search bar
- Displaying a formatted listing of the plugin source code

## Data sources

- Manual link definitions by developers
- Static analysis (scanning code that is loaded but not running)
- Dynamic analysis (automated scanning of runtime and sent events during operation - ⚡ [DebugEventEvent][DebugEventEvent])

## Limitations

1. The plugin is only available in **DEBUG** mode to protect production environments.
2. ⚠️ For a complete list of objects, the functionality must be executed at least once during the session.
3. Only named functions and objects that the plugin exposes via **this** are indexed.

[PlgsList]: plugins.lst.md "List of plugins"
[OEGroups]: :_/README.md "Object categories list"
[OETree]: :_/tree/TREE.md "Dependency tree"
[OELoadOrder]: :_/LORDER.md "Loading order"
[DebugEventEvent]: :_evt:DebugEventEvent.md "DebugEventEvent"
