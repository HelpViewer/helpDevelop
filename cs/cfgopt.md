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

## Záznamy 📄⚙️

Pokud se v [prohlížeči objektů][oexplorer] objeví záznamy s ikonkou 📄⚙️, znamená to, že konkrétní klíče, které konfigurace obsahuje nejsou v pluginu vyjmenovány způsobem, jak je popsáno zde v [definici](#h-2-0).

Důvodem mohou být například:

- přístup inspirovaný [prohlížečem objektů][oexplorer], kde je cílem mít otevřenou množinu konfiguračních klíčů. Seznam skupin může být libovolně dlouhý a jeho položky odkazují na další klíče. Tyto klíče nejsou předem známé, protože konfigurace může být dynamicky měněna, ale plugin je díky své interní logice dokáže správně načíst.
- překlep v klíči na straně konfiguračního souboru vede ke vzniku další viditelné položky, přičemž u klíče správného jména se použije default hodnota protože nic není načteno

[cfgPlug]: pluginConfig.md "Konfigurace pluginů"
[pTRParseMd]: :_inst:pTRParseMd:-md.md#h-2-1 "pTRParseMd:-md"
[oexplorer]: oexplorer.md "Prohlížeč objektů"
