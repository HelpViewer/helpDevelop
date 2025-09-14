# ⚙️ Konfigurační volba

Konfigurační volba zastupuje ⚙️ [konfiguraci pluginů][cfgPlug] na straně kódu pluginu.

## Definice

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

### Ukázka konfiguračního souboru

Tato definice se napáruje na tuto definici v konfiguračním souboru:

```text
FILENAME|README.md
```

[Ukázka na straně prohlížeče objektů][pTRParseMd]

Pokud se v konfiguračním souboru nenajde klíč z konstanty **KEY_CFG_FILENAME**, použije se hodnota **DEFAULT_KEY_CFG_FILENAME**.

### Význam proměnných

- KEY_CFG_FILENAME - jméno konfiguračního klíče na straně konfigurace
- DEFAULT_KEY_CFG_FILENAME - defaultní hodnota pro konfigurační klíč
- ⚠️ DEFAULT_**KEY_CFG_FILENAME** a **KEY_CFG_FILENAME** se musí svým názvem objektu shodovat, aby prohlížeč objektů konfigurační volbu správně vyhodnotil a propojil název i výchozí (záložní) hodnotu.


[cfgPlug]: pluginConfig.md "Konfigurace pluginů"
[pTRParseMd]: :_inst:pTRParseMd:-md.md#h-2-1 "pTRParseMd:-md"
