# ⚙️ Configuration option

The configuration option represents ⚙️ [plugin configuration][cfgPlug] on the plugin code side.

## Definition

```javascript
class pConfigValuePlugin extends IPlugin {
  static KEY_CFG_FILENAME = 'FILENAME';

  init() {
    const T = this.constructor;
    const TI = this;
    TI.DEFAULT_KEY_CFG_FILENAME = 'marked.min.js;LICENSE-marked.md';
    TI.cfgFileName = TI.config[T.KEY_CFG_FILENAME] || TI.DEFAULT_KEY_CFG_FILENAME;
    super.init();
  }
}
Plugins.catalogize(pConfigValuePlugin);
```

### Configuration file example

This definition is paired with this definition in the configuration file:

```text
FILENAME|README.md
```

[Example on the object browser page][pTRParseMd]

If the key from the **KEY_CFG_FILENAME** constant is not found in the configuration file, the value **DEFAULT_KEY_CFG_FILENAME** is used.

### Meaning of variables

- KEY_CFG_FILENAME - name of the configuration key on the configuration side
- DEFAULT_KEY_CFG_FILENAME - default value for the configuration key
- ⚠️ DEFAULT_**KEY_CFG_FILENAME** and **KEY_CFG_FILENAME** must match in name so that the object browser can correctly evaluate the configuration option and link the name and default (backup) value.

## Records 📄⚙️

If records with the 📄⚙️ icon appear in the [object explorer][oexplorer], it means that the specific keys contained in the configuration are not listed in the plugin as described here in the [definition](#h-2-0).

The reasons for this may include:

- An approach inspired by the [object explorer][oexplorer], where the goal is to have an open set of configuration keys. The list of groups can be arbitrarily long, and its items refer to other keys. These keys are not known in advance because the configuration can be changed dynamically, but the plugin can read them correctly thanks to its internal logic.
- A typo in the key on the configuration file side leads to the creation of another visible item, while the default value is used for the key with the correct name because nothing is read.

[cfgPlug]: pluginConfig.md "Plugin configuration"
[pTRParseMd]: :_inst:pTRParseMd:-md.md#h-2-1 "pTRParseMd:-md"
[oexplorer]: oexplorer.md "Object explorer"
