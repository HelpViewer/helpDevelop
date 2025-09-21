# ⚙️ Configuration option

The configuration option represents ⚙️ [plugin configuration][cfgPlug] on the plugin code side.

## Definition

```javascript
class pConfigValuePlugin extends IPlugin {
  init() {
    const T = this.constructor;
    const TI = this;
    TI.DEFAULT_KEY_CFG_FILENAME = 'marked.min.js;LICENSE-marked.md';
    // TI.cfgFILENAME
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

If the **FILENAME** key is not found in the configuration file, the value **DEFAULT_KEY_CFG_FILENAME** will be used.

### Meaning of variables

- DEFAULT_KEY_CFG_**FILENAME** - default value for the configuration key (defines the configuration key, the value can be undefined)
- **FILENAME** - name of the configuration option
- In the plugin, you can access the configuration value via this.cfg**FILENAME** or this.config['FILENAME']

## Records 📄⚙️

If records with the 📄⚙️ icon appear in the [object explorer][oexplorer], it means that the specific keys contained in the configuration are not listed in the plugin as described here in the [definition](#h-2-0).

The reasons for this may include:

- An approach inspired by the [object explorer][oexplorer], where the goal is to have an open set of configuration keys. The list of groups can be arbitrarily long, and its items refer to other keys. These keys are not known in advance because the configuration can be changed dynamically, but the plugin can read them correctly thanks to its internal logic.
- A typo in the key on the configuration file side leads to the creation of another visible item, while the default value is used for the key with the correct name because nothing is read.

[cfgPlug]: pluginConfig.md "Plugin configuration"
[pTRParseMd]: :_inst:pTRParseMd:-md.md#h-2-1 "pTRParseMd:-md"
[oexplorer]: oexplorer.md "Object explorer"
