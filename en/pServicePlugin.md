# 🔌 pServicePlugin

## Purpose of the plugin

This plugin is designed to define interfaces for extension services.

It is based on handlers connected to plugin events 🔌 [pPluginManagement][pPluginManagement].

## Implementation

1. A new plugin will always have [pServicePlugin][pServicePlugin] as its base class.

```javascript
class pNewServicePlugin extends pServicePlugin {
  init() {
    super.init();
  }

  _pluginActivated(pluginName, instanceName, instance, storageName) {
    if (instance) {
      // if the instance meets a condition, add it to the plugin list and perform other actions
      this.addPlugin(pluginName, instanceName);
    }
  }

  _pluginDeactivated(pluginName, instanceName, instance, storageName) {
  }

  onET...(evt) {
    this._doForAllInstances(this._pluginActivated.bind(this));
  }
}

Plugins.catalogize(pNewServicePlugin);
```

2. The basic plugin must define appropriate events (including their content) so that its processes can be effectively connected.

- _pluginActivated - ensures processing for activating a new plugin instance
- addPlugin - adds a plugin and its instance to the list of plugins that the service will manage. Must be called manually.
- _pluginDeactivated - ensures processing for removing the plugin instance, automatically removes the plugin instance from the list of plugins in the service
- onET...(evt) - the service may need to handle an event provided by the rest of the system or another plugin for which this service will be an extension.
- **evt** - will represent a specific event object depending on the process you are developing
- this._doForAllInstances(this._pluginActivated.bind(this)); - calls the _pluginActivated method for all registered instances of the plugin. The use of **bind(this)** is necessary to **preserve the context of this** when passing the method.

## Functionality description

- The plugin listens for events ⚡ [PluginActivated][PluginActivated] (calls the **\_pluginActivated** function) and ⚡ [PluginDeactivated][PluginDeactivated] (calls the **\_pluginDeactivated** function)
- The plugin listens for other events according to the declared handlers
- If the plugin instance meets the service requirements, add it to the list by calling the **addPlugin** function.
- The instance is removed automatically upon receiving ⚡ [PluginDeactivated][PluginDeactivated]

## Implementation examples

- ⚙️ [pServiceLocalization][pServiceLocalization] and other descendants of the class 🔌 [pServicePlugin][pServicePlugin]

[pPluginManagement]: :_inst:pPluginManagement:.md "pPluginManagement"
[pServiceLocalization]: :_plg:pServiceLocalization.md "pServiceLocalization"
[PluginActivated]: :_evt:PluginActivated.md "PluginActivated"
[PluginDeactivated]: :_evt:PluginDeactivated.md "PluginDeactivated"
[pServicePlugin]: :_plg:pServicePlugin.md "pServicePlugin"
