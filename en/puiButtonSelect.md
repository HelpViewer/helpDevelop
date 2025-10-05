# 🖥️ puiButtonSelect

## Purpose of the plugin

This plugin is suitable for providing a simple 🔘▼ button with a selection list.

## Configuration

1. Prepare the configuration with values according to [puiButton][puiButton].

## Implementation

2. The new plugin will always have [puiButtonSelect][puiButtonSelect] as its base class.

```javascript
class puiButtonSelectNew extends puiButtonSelect {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_ID = 'downP-selNew';
    this.DEFAULT_KEY_CFG_CAPTION = '🖼️';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
  }

  async init() {
    // ... insert application event initialization here ...

    super.init();

    // ... insert component data initialization here ...

    const items = ['A', 'B', 'C']; // items
    const selVal = 'B'; // default selected value

    appendComboBoxItems(this.select, items, selVal);
  }

  deInit() {
    super.deInit();
  }

  _handle(e) {
    const newVal = e.target.options[e.target.selectedIndex].text;
    // ...
  }

  _handleFocus(e) {
    // ...
  }

  // ...
}

Plugins.catalogize(puiButtonSelectNew);

```

- The **this.DEFAULT_KEY_CFG_** lines can be removed if you want to rely solely on the configuration from the file. However, considering the automatic documentation of objects in the plugin, I recommend leaving them.

## Functionality description

- **this.select** contains a link to the created selection list
- **e** represents JavaScript system events
- **appendComboBoxItems** adds a set of items to the selection box. Indexes are assigned from 0
- **e.target.selectedIndex** index of the selected item
- **e.target.options\[e.target.selectedIndex\].text** text of the selected item
- **this.select.options.length = 0** deletes the items in the selection box
- **_handleFocus** action before opening the list of possible options
- **sendEvent('ButtonSelectIconSet', (x) => {x.payload = '🖥️'; id = '';});** changes the button icon to 🖥️

## Implementation examples

- 🖥️ [puiButtonSelectSkin][puiButtonSelectSkin] and other descendants of the class 🖥️ [puiButtonSelect][puiButtonSelect]

[puiButton]: puiButton.md#h-2-1 "puiButton"
[puiButtonSelect]: :_plg:puiButtonSelect.md "puiButtonSelect"
[puiButtonSelectSkin]: :_plg:puiButtonSelectSkin.md "puiButtonSelectSkin"
