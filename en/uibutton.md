# 🔘 Button

It is recommended to use the plugin directly: 🖥️ [puiButton][puiButton], which provides functionality including configuration.

The component defines a standard HTML button that is modified by the CSS class **.pnl-btn** in all locations. If you need the button to look different on each panel, style the descendant class selector (**.topPanel .pnl-btn**).

## Definition

1. In the plugin, define the button object and its handler in init (listing shortened to the init function):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    this.cfgId = 'NewBtnId';
    this.cfgCaption = '🔘';
    this.cfgTarget = UI_PLUGIN_SIDEBAR;
    this.button = uiAddButton(this.cfgId, this.cfgCaption, this.cfgTarget, this._buttonAction);

    super.init();
  }

  _buttonAction(evt) {
    alert('Ahoy.');
  }
```

## Meaning of elements

- this.button - contains a reference to the HTML button element
- this.cfgId - ID of the new button
- this.cfgCaption - text of the new button (or icon)
- this.cfgTarget - target panel for the button
- _buttonAction - button click handler
- evt - event ⚡ [ClickedEvent][ClickedEvent]

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[puiButton]: puiButton.md "puiButton"
