# 🖥️ puiButtonTab

## Purpose of the plugin

This plugin is suitable for securing 🔘🎛️ buttons and sidebar tabs.

## Configuration

1. Prepare the configuration with the same values as for the 🖥️ [puiButton][puiButtonC] component.

## Implementation

2. The new plugin will always have [puiButtonTab][puiButtonTab] as its base class.

```javascript
class puiNewButtonWithTab extends puiButtonTab {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_ID = 'downP-NewButton';
    this.DEFAULT_KEY_CFG_CAPTION = '🤡';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
  }

  _preShowAction(evt) {
    //this.tab
  }

  //_buttonAction(evt) {
  //}

}

Plugins.catalogize(puiNewButtonWithTab);
```

- The lines **this.DEFAULT_KEY_CFG_** can be removed if you want to rely solely on the configuration from the file. However, considering the automatic documentation of objects in the plugin, I recommend leaving them.

| Object | Description |
|---|---|
| this.tab | Reference to the HTML element of the tab. It is possible to attach additional objects to it |
| this.button | Reference to the HTML element of the button |
| parameter evt | Application event, ⚡ [ClickedEvent][ClickedEvent] |
| _preShowAction(evt) | Triggered before the card is displayed to the user. Ideal for delayed loading of plugin data displayed to the user on the card, or for preparing a configuration form for further action. It should be overwritten with an empty function in the descendant. If the function returns **false**, the card will not be displayed to the user. |
| _buttonAction(evt) | Button action. Usually, it is not necessary to overwrite it if simply displaying the card to the user is sufficient. |

## Functionality description

- The **_buttonAction**(evt) function is a handler for button clicks. The default handling is provided by the parent, but it may be desirable to override it, see the implementation examples below.
- In its default behavior, the function calls **_preShowAction**(evt) and  
displays the component card on the panel.
- **_preShowAction**(evt) can return false to block the card from being displayed to the user. If it returns undefined (default behavior) or true, the plugin will display the card normally.

## Implementation examples

- 🖥️ [puiButtonChangeLanguage][puiButtonChangeLanguage]

### Button with actions based on tab visibility - _buttonAction(evt)

If you define the _buttonAction function this way:

```javascript
  _buttonAction(evt) {
    if (this.tab.classList.contains(C_HIDDENC)) {
      super._buttonAction();
    } else {
      // (B)
    }
  }
```

you get a two-step process:

- first click: displays a hidden tab (usually with a prepared form)
- second click: performs another operation in branch **(B)** with data taken from the form

Example: 🖥️ [puiButtonAsBook][cpuiButtonAsBook]

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[puiButtonTab]: :_plg:puiButtonTab.md "puiButtonTab"
[puiButtonC]: puiButton.md#h-2-1 "puiButton"
[cpuiButtonAsBook]: :_cpp:puiButtonAsBook.md "puiButtonAsBook"
[puiButtonChangeLanguage]: :_plg:puiButtonChangeLanguage.md "puiButtonChangeLanguage"
