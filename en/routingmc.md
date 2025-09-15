# 🔀 Mouse click routing

This object is managed by the 🖥️ [pui][pui] plugin. It is a dictionary of prefixes of names or specific names under which service methods are stored. This structure is used technologically by other plugins. It is also possible to define your own service here.

## Definition

1. In the plugin, you define the handler in init as follows (excerpt shortened to the init function):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    TI.cfgTreeId = 'NewTreeId';
    registerOnClick(TI.cfgTreeId, (evt) => {
      TI._treeClick(evt);
    });

    super.init();
  }

  _treeClick(evt) {
  }
```

In the [object explorer][oexplorer], this item can be found under the plugin 🖥️ [pui][puir].

## Meaning of elements

- TI.cfgTreeId - id key for passing the event ⚡ [ClickedEvent][ClickedEvent]. The event will be passed to the connected handler if the key in the routing matches:
  - the entire object id,
  - the first part of the element id (the element id is divided by the characters **|** and **-**. The reason for this is that tree components have a common handler for their items, and this handler is also implemented here)
- registerOnClick(TI.cfgTreeId,  (evt) => { - attaches the function in the second parameter to the ID or base name in TI.cfgTreeId

## Reset handler

If necessary, reset the handler to the same key by assigning an empty method again:

```javascript
    const TI = this;
    TI.cfgTreeId = 'NewTreeId';
    registerOnClick(TI.cfgTreeId, (evt) => {});
```

## Implementation examples

- 🖥️ [pui][puir] - UI interface logic control plugin

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[oexplorer]: oexplorer.md "Object explorer"
[pui]: :_plg:pui.md "pui"
[puir]: :_inst:pui:.md#h-2-1 "pui routing table"
