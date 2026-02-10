# 📑 Loading plugins

There are two ways to load a plugin instance in the application:

1. By defining it in the [plugin list][plugins]. The application will load it automatically when it starts or when the help is loaded.
2. By calling the function anywhere in the application code

## Dynamic plugin loading

```javascript
const pluginName = 'puiButtonObjectExplorer';
const pluginId = '-load';
await loadPlugin(pluginName, loadPluginListBasePath(pluginName), STO_DATA);
await activatePlugin(pluginName, pluginId);
```

| Definition | Description |
|---|---|
| pluginName | Name of the plugin class |
| loadPlugin | Ensures that the plugin class is loaded if it has not been loaded yet. |
| loadPluginListBasePath(pluginName) | Function that ensures the correct path to the plugin file within the data package is constructed. Assumes that the plugin file will be located in **plugins/(pluginName).js**. The third parameter specifies which storage to search: STO_DATA is the default, another option is STO_HELP. |
| activatePlugin | Ensures that a new instance of the **pluginName** plugin with id **pluginId** is created |

## Removing a plugin during runtime

You can remove a plugin as follows:

```javascript
const pluginName = 'puiButtonObjectExplorer';
const pluginId = '-load';
await deactivatePlugin(pluginName, pluginId);
```

> [!CAUTION] This operation allows you to remove any plugin from the system.  
If you remove a key system plugin, it is possible that the application within the given session:
- will stop working partially or completely (it will not respond to important events from the system or JavaScript)
- will restart more often
- will excessively redraw its entire user interface

## Plugin management actions

These plugin management actions are performed either by the basic functions of the application or by the 🔌 [pPluginManagement][pPluginManagement] plugin, if it is installed (it is included in the basic system configuration in the standard distribution package). The pPluginManagement plugin provides encapsulation of basic functions for working with plugins and sending events to the system when there is a change in active plugins (loading, initialization, removal, loading/initialization/removal error).

[plugins]: plugins.lst.md "List of plugins"
[pPluginManagement]: :_inst:pPluginManagement:.md "pPluginManagement"
