# 🖥️ puiButtonTabTree

## Purpose of the plugin

This plugin is suitable for securing 🔘🎛️📂 buttons and sidebar tabs with a tree component.

## Configuration

1. Prepare the configuration with the same values as for the 🖥️ [puiButton][puiButtonC] component.
2. Add the **TREEID** key, which will contain the name of the new tree.

## Implementation

3. The new plugin will always have [puiButtonTabTree][puiButtonTabTree] as its base class.

```javascript
class puiNewButtonWithTree extends puiButtonTabTree {
  constructor(aliasName, data) {
    super(aliasName, data);
    
    this.DEFAULT_KEY_CFG_ID = 'downP-NewTree';
    this.DEFAULT_KEY_CFG_CAPTION = '📂';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
    
    this.DEFAULT_KEY_CFG_TREEID = newtree';
    //setTreeData(data, this.aliasName, append);
  }
  
  //_buttonAction(evt) {
  //}

  _preShowAction(evt) {
  }

  _preStandardInit() {
  }

  _treeClick(e) {
  }
}

Plugins.catalogize(puiNewButtonWithTree);
```

- The lines **this.DEFAULT_KEY_CFG_** can be removed if you want to rely solely on the configuration from the file. However, considering the automatic documentation of objects in the plugin, I recommend leaving them.

| Object | Description |
|---|---|
| this.tab | Reference to the HTML tab element. Additional objects can be attached to it. |
| this.button | Reference to the HTML button element. |
| this.tree | Reference to the HTML tree element (**ul** element). |
| evt parameter | Application event, ⚡ [ClickedEvent][ClickedEvent] |
| _preStandardInit | Triggered before the tree component is created on the tab. It is intended for creating additional components if necessary. |
| _preShowAction(evt) | Triggered before the card is displayed to the user. Ideal for delayed loading of plugin data displayed to the user on the card, or for preparing a configuration form for further action. It should be overridden with an empty function in the descendant. If the function returns **false**, the card will not be displayed to the user. |
| _buttonAction(evt) | Button action. Usually, it is not necessary to override it if simply displaying the card to the user is sufficient. |
| _treeClick(e) | Action when clicking on a tree item, ⚡ [ClickedEventTree][ClickedEventTree]. If not overwritten, it will take over the shared handler **processAClick** from **appmainBaseLogic.js** (this handler is already on the border between a general solution and a specific implementation). |
| setTreeData(data, this.aliasName, append); | Sets the [tree data][treedata] from the data string. The plugin's aliasName is used for identification. Append can be omitted or set to **true** if you want to append some data to the end of the tree. |

If you are not satisfied with the **setTreeData** function, you can use the lower-level function that this function encapsulates - **linesToHtmlTree**(data, alias) - data is again a string [treedata] and alias is the value of the **TREEID** configuration.

## Functionality description

- The **_preStandardInit**() function is automatically executed when the plugin instance is created.
- The **_buttonAction**(evt) function is a handler for button clicks. The default handling is provided by the parent. Overwriting is not expected, but it is possible.
- In its default behavior, the function calls **_preShowAction**(evt) and  
displays the component card on the panel.
- **_preShowAction**(evt) can return false to block the card from being displayed to the user. If it returns undefined (default behavior) or true, the plugin will display the card normally.

## Implementation examples

- 🖥️ [puiButtonObjectExplorer][puiButtonObjectExplorer] and other descendants 🖥️ [puiButtonTabTree][puiButtonTabTree]

### Scenario: Button with open/close all action

If you define the _buttonAction function in this way:

```javascript
  _buttonAction(evt) {
    this._buttonActionClickOpenCloseAll(evt?.event?.isTrusted);
  }
```

You will get a switch that performs three actions when clicked:

- The tab is not visible -> displays the tab with the tree.
- The tab is visible, there is at least one unopened item -> all items in the tree are opened.
- Card is visible, all items are open -> all tree items are closed.

Example: 🖥️ [puiButtonTOC][cpuiButtonTOC]

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[ClickedEventTree]: :_evt:ClickedEventTree.md "ClickedEventTree"
[puiButtonTabTree]: :_plg:puiButtonTabTree.md "puiButtonTabTree"
[puiButtonC]: puiButton.md#h-2-1 "puiButton"
[cpuiButtonTOC]: :_cpp:puiButtonTOC.md "puiButtonTOC"
[puiButtonObjectExplorer]: :_plg:puiButtonObjectExplorer.md "puiButtonObjectExplorer"
[treedata]: ?d=hlp-aguide/Help-__.zip&p=mdata%2Ftree.lst.md "tree input data format"
