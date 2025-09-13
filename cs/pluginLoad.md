# 📑 Zavádění pluginů

Zavést instanci pluginu je v aplikaci možné dvěma způsoby:

1. Definicí v [seznamu pluginů][plugins]. Při spouštění aplikace nebo načítání nápovědy zavedení provede aplikace sama.
2. Voláním funkce kdekoli v kódu aplikace

## Dynamické zavedení pluginu

```javascript
const pluginName = 'puiButtonObjectExplorer';
const pluginId = '-load';
await loadPlugin(pluginName, loadPluginListBasePath(pluginName));
await activatePlugin(pluginName, pluginId);
```

| Definice | Popis |
|---|---|
| pluginName | Jméno třídy pluginu |
| loadPlugin | Zajistí načtení třídy pluginu, pokud zatím načtena nebyla. |
| loadPluginListBasePath(pluginName) | Funkce, která zajistí sestavení správné cesty k souboru pluginu uvnitř balíku dat. Předpokládá, že se soubor pluginu bude nacházet v **plugins/(pluginName).js** |
| activatePlugin | Zajistí vytvoření nové instance pluginu **pluginName** s id **pluginId** |

## Odebrání pluginu za běhu

Plugin odeberete následujícím způsobem:

```javascript
const pluginName = 'puiButtonObjectExplorer';
const pluginId = '-load';
await deactivatePlugin(pluginName, pluginId);
```

⚠️ Tato operace dovolí ze systému odebrat jakýkoli plugin.  
Pokud odeberete klíčový plugin systému, je možné, že aplikace v rámci dané relace:

- přestane částečně či zcela fungovat (nebude reagovat na důležitou událost ze systému nebo javascriptu)
- se bude častěji restartovat
- bude nadměrně překreslovat celé své uživatelské rozhraní

## Akce správy pluginů

Tyto akce správy pluginů provádí buďto základní funkce aplikace nebo plugin 🔌 [pPluginManagement][pPluginManagement], pokud je zaveden (je v základní systémové konfiguraci ve standardním distribučním balíčku). Plugin pPluginManagement poskytuje zapouzdření základních funkcí pro práci s pluginy a zasílání událostí dovnitř systému, pokud dojde ke změně v aktivních pluginech (načtení, inicializace, odebrání, chyba operace načtení/inicializace/odebrání).

[plugins]: plugins.lst.md "Seznam pluginů"
[pPluginManagement]: :_inst:pPluginManagement:.md "pPluginManagement"
