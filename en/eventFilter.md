# 🔺 Filtering events in plugins

Each plugin can receive events from the system. Plugins have a switch to (de)activate the filter for receiving events according to the **aliasName (id)** of the plugin instance:

```javascript
this.eventIdStrict = true;
```

Make the call in the constructor or at the beginning of the init() function, or at the latest before calling base.init().

Event filtering is two-stage - according to eventIdStrict and the name of the handler function. This is described in more detail in the following subchapters.

## Summary

- The **onET_(event name)** function accepts all events with eventName = (event name)
- The **onET(event name)** function accepts all events with eventName = (event name) and id = plugin.aliasName
- **A plugin with plugin.aliasName = ''** accepts all events into the **onET(event name)** or **onET_(event name)** function

> [!WARNING] It is recommended to have only one of the following handlers in the plugin:  
 
- onET(event name)
- onET_(event name)

## How to decide on the settings?

The plugin should not listen to all events, but only some will be sent directly to it, so it will receive a specific id and eventIdStrict = true.

Set EventIdStrict to **true** at least in these cases:

- The plugin will (or may) run in more than one instance (for example, 📇 keyword dictionary and 🔎 full-text search)
- The plugin will be part of a process (🖼️ [pTRPhasePlugin][pTRPhasePlugin] - listing the contents of a chapter)
- The plugin will be part of a larger functional unit (🔹 [pIndexFile:fulltextList][pIndexFile] - dynamic creating a full-text index of help)

📘 A [detailed appendix][appendix] is available for this chapter.

[pTRPhasePlugin]: pTRPhasePlugin.md "pTRPhasePlugin"
[pIndexFile]: :inst:pIndexFile:fulltextList.md "pIndexFile:fulltextList"
[appendix]: eventFilterD.md "Rozbor filtrování událostí v pluginech"