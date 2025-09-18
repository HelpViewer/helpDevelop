# 🖥️ puiButton

## Purpose of the plugin

This plugin is suitable for providing a simple 🔘 button with an action for the user interface.

## Configuration

1. Prepare the configuration with the following values:

| Name | Description |
|---|---|
| ID | ID of the new button. It must be unique across the system so that the button is not linked to another action and the plugin does not overwrite another action. |
| CAPTION | Caption or icon for the button. If the **ID** of the button is defined as a key in localization, the data will be overwritten with the value of the translation key. |
| TARGET | Target slot for the button. Common values: sidebar (side panel), header (top panel above the chapter text), bottom (bottom panel below the chapter text, empty panel is usually hidden). The value can be anything, but the target plugin (matched by plugin ID) must be able to handle the ⚡ [ButtonSend][ButtonSend] event, otherwise the button will not be displayed anywhere. |

## Implementation

2. A new plugin will always have [puiButton][puiButton] as its base class.

```javascript
class puiButtonFullScreen extends puiButton {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_ID = 'downP-ToggleFS';
    this.DEFAULT_KEY_CFG_CAPTION = '🔲';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
  }
  
  _buttonAction(evt) {
    document.fullscreenElement 
      ? document.exitFullscreen() 
      : document.documentElement.requestFullscreen();
  }
}

Plugins.catalogize(puiButtonFullScreen);
```

- The lines **this.DEFAULT_KEY_CFG_** can be removed if you want to rely solely on the configuration from the file. However, considering the automatic documentation of objects in the plugin, I recommend leaving them.
- **this.button** contains a reference to the created button.

## Functionality description

- The **_buttonAction**(evt) function is a handler for button clicks.
- **evt** represents ⚡ [ClickedEvent][ClickedEvent]

## Implementation examples

- Descendants of the 🖥️ [puiButton][puiButton] class

### Scenario: Button hidden in 📽 presentation mode

```javascript
this.button.classList.add(C_HIDDENCPRESMODE);
```

[ButtonSend]: :_evt:ButtonSend.md "ButtonSend"
[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[puiButton]: :_plg:puiButton.md "puiButton"
