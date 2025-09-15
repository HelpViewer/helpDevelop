# 🎛️ Tab

It is recommended to use the plugin directly: 🖥️ [puiButtonTab][puiButtonTab], which provides functionality including configuration and a button used to display this tab. The button in this plugin can be placed independently of the tab on any available panel.
The component defines a standard HTML div, which it inserts into the side panel as hidden.

## Definition

1. In the plugin, define the card object in init (listing shortened to the init function):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    const id = 'NewTabId';
    const role = '';
    this.tab = uiAddSidebarPage(id, role);

    super.init();
  }
```

## Meaning of elements

- id - id of the new tab
- role - ARIA role, usually left blank

[puiButtonTab]:puiButtonTab.md "puiButtonTab"
