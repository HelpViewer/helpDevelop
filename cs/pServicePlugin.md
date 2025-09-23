# 🔌 pServicePlugin

## Účel pluginu

Tento plugin je určen k definici rozhraní pro rozšiřující služby.

Základem jsou obsluhy napojené na události pluginu 🔌 [pPluginManagement][pPluginManagement].

## Implementace

1. Nový plugin vždy bude mít [pServicePlugin][pServicePlugin] jako svou bázovou třídu.

```javascript
class pNewServicePlugin extends pServicePlugin {
  init() {
    super.init();
  }

  _pluginActivated(pluginName, instanceName, instance, storageName) {
    if (instance) {
      // pokud instance splňuje nějakou podmínku, provést zavedení do seznamu pluginů a další akce
      this.addPlugin(pluginName, instanceName);
    }
  }

  _pluginDeactivated(pluginName, instanceName, instance, storageName) {
  }

  onET...(evt) {
    this._doForAllInstances(this._pluginActivated.bind(this));
  }
}

Plugins.catalogize(pNewServicePlugin);
```

2. Základní plugin musí definovat vhodné události (včetně jejich obsahu), aby se na jeho procesy bylo možné efektivně napojit.

- _pluginActivated - zajišťuje zpracování pro aktivaci nové instance pluginu
- addPlugin - přidání pluginu a jeho instance do seznamu pluginů, které služba bude spravovat. Musí se volat ručně.
- _pluginDeactivated - zajišťuje zpracování pro odebrání instance pluginu, automaticky provede odebrání instance pluginu ze seznamu pluginů ve službě
- onET...(evt) - služba možná bude potřebovat obsluhu nějaké události, kterou zajišťuje zbytek systému nebo jiný plugin, pro který bude tato služba rozšířením. 
- **evt** - bude představovat konkrétní objekt události v závislosti na procesu, který budete vyvíjet
- this._doForAllInstances(this._pluginActivated.bind(this)); - volá metodu _pluginActivated pro všechny evidované instance pluginu. Použití **bind(this)** je nutné, aby se při předání metody **zachoval kontext this**.

## Popis funkčnosti

- Plugin naslouchá událostem ⚡ [PluginActivated][PluginActivated] (volá funkci **\_pluginActivated**) a ⚡ [PluginDeactivated][PluginDeactivated] (volá funkci **\_pluginDeactivated**)
- Plugin naslouchá dalším událostem podle deklarovaných obsluh
- V případě ověření, že instance pluginu splňuje požadavky služby ji zaveďte do seznamu voláním funkce **addPlugin**. 
- Odebrání instance se provede automaticky s přijetím ⚡ [PluginDeactivated][PluginDeactivated]

## Příklady implementací

- ⚙️ [pServiceLocalization][pServiceLocalization] a další potomci třídy 🔌 [pServicePlugin][pServicePlugin]

[pPluginManagement]: :_inst:pPluginManagement:.md "pPluginManagement"
[pServiceLocalization]: :_plg:pServiceLocalization.md "pServiceLocalization"
[PluginActivated]: :_evt:PluginActivated.md "PluginActivated"
[PluginDeactivated]: :_evt:PluginDeactivated.md "PluginDeactivated"
[pServicePlugin]: :_plg:pServicePlugin.md "pServicePlugin"
