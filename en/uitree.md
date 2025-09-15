# 📂 Tree

It is recommended to use the plugin directly: 🖥️ [puiButtonTabTree][puiButtonTabTree], which provides functionality including configuration, tabs, activation buttons, and other supporting actions.

The component defines a standard HTML ul element, which is modified by the CSS class **.tree**.

## Definition

1. In the plugin, define the tree object in init to handle its items (list shortened to the init function):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    const id = 'tabId';
    const role = '';
    TI.tab = uiAddSidebarPage(id, role);

    TI.cfgTreeId = 'NewTreeId';
    TI.tree = uiAddTreeView(TI.cfgTreeId, TI.tab);

    registerOnClick(TI.cfgTreeId, (e) => {
      const result = TI._treeClick(e);
      _notifyClickedEvent(e, result, TI.cfgTreeId);
    });

    super.init();
  }

  _treeClick(e) {
  }
```

## Meaning of elements

- TI.tab - reference to the HTML element of the parent tree card
- const id - parent card id
- TI.cfgTreeId - id of the new tree
- uiAddTreeView - creates a new tree component
- registerOnClick - adds the basic prefix of all items in the new tree to the mouse click handler list. It is recommended that the tree id be unique across the system so that plugin handlers do not overwrite each other
- _notifyClickedEvent - sends the event ⚡ [ClickedEventTree][ClickedEventTree], which is further processed by the plugin 🖥️ [pui][pui] by logging it or sending the event ⚡ [ClickedEventNotForwarded][ClickedEventNotForwarded] if no event is found for the base prefix of the items

[ClickedEventTree]: :_evt:ClickedEventTree.md "ClickedEventTree"
[ClickedEventNotForwarded]: :_evt:ClickedEventNotForwarded.md "ClickedEventNotForwarded"
[puiButtonTabTree]: puiButtonTabTree.md "puiButtonTabTree"
[pui]: :_plg:pui.md "pui"
