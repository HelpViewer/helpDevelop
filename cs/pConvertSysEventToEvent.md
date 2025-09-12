# 🔌 pConvertSysEventToEvent

## Účel pluginu

Plugin převádí definovanou javascript událost na událost aplikace, která může být zachycena jiným pluginem.

## Implementace

### 1) Konfiguračně s automatickým odesláním ConvertedSystemEvent

1. V souboru **plugins.lst** zaveďte řádek:  
   pConvertSysEventToEvent:[instanceid]
2. V souboru **plugins-config/pConvertSysEventToEvent_[instanceid].cfg** definujte například:

```text
SYSEVENTNAME|click
SYSOBJECT|body
EVENTBUSEVENT|ClickedEvent
EVENTBUSEVENTID|
```

| Název | Popis |
|---|---|
| SYSEVENTNAME | Jméno javascript systémové událostí (addEventListener). |
| SYSOBJECT | Systémový objekt na který se má plugin navázat. Hodnoty: window, document, body, #xxx = HTML prvek s konkrétním id |
| EVENTBUSEVENT | Jméno události na straně aplikace. |
| EVENTBUSEVENTID | Vlastnost id odesílané zkonvertované události. Podle této vlastnosti se uvnitř systému může filtrovat doručení do všech (🟢) nebo do konkrétních pluginů, které mají id shodné jako zpráva (🔺). |

Javascript událost bude automaticky přeložena do události ⚡ [ConvertedSystemEvent][ConvertedSystemEvent] a ta bude zaslána s **id** odpovídajícím **EVENTBUSEVENTID** a **eventName** bude shodné s hodnotou **EVENTBUSEVENT**.

### 2) Programové řešení s vlastní konverzí do jiného objektu události

1. Proveďte kroky v kapitole 1.
2. Připravte v souboru **plugins/[název pluginu].js** například následující kód:

```javascript
class ClickedEvent extends IEvent {
  constructor() {
    super();
    this.elementId = '';
    this.elementIdRoot = '';
    this.elementIdVal = '';
    this.target = null;
    this.event = null;
    this.forwarded = false;
  }
}

ClickedEvent.register();

class pClickConverter extends pConvertSysEventToEvent {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_SYSEVENTNAME = 'click';
    this.DEFAULT_KEY_CFG_SYSOBJECT = 'body';
    this.DEFAULT_KEY_CFG_EVENTBUSEVENT = 'ClickedEvent';
  }

  _fillEventObject(d, evt) {
    d.event = evt;
    d.target = d.event?.target;
    d.elementId = d.target?.id
    const splits = d.elementId?.replace('-', '|').split('|').filter(Boolean) ?? [];
    d.elementIdRoot = splits[0];
    d.elementIdVal = splits[1];
  }
}

Plugins.catalogize(pClickConverter);
```

- ClickedEvent je objekt cílové události na straně aplikace.
- **ClickedEvent.register()** provede registraci objektu události do katalogu (informaci o tomto zápisu najdete v **puiButtonObjectExplorer** v **Strom dědičnosti**, kapitola **Odkaz**). Toto je nutné z důvodu nemožnosti javascriptu provádět rozšířenou detekci objektů podle jmen. Toto jméno musíte mít také uvedeno v konfiguraci v **EVENTBUSEVENT**.
- Řádky **this.DEFAULT_KEY_CFG_** buďto v kódu ponechte nebo je můžete zcela odebrat. Konfigurace z bodu 1 je přepisuje.
- Funkce _fillEventObject(d, evt) provádí samotnou konverzi evt (javascript systémové události) na d (cílová událost na straně aplikace).
- Volání **Plugins.catalogize(pMinPlugin);** je povinné. Provede zavedení pluginu do katalogu načtených pluginů.

Výsledkem jednoho zpracování bude událost ⚡ ClickedEvent s obsahem typu třídy ClickedEvent z ukázky.

### ClickedEvent.register()

Funkce IEvent.register() zajišťuje zavedení třídy události do katalogu, aby mohla být později propojena se jménem v konfiguraci.

| Parametr | Povinnost | Popis |
|---|---|---|
| evtName | Ne | Jméno události, pokud chcete konkrétní třídu svázat s jiným jménem události. Zadání (jiného) jména je určitou náhradou dědičnosti tříd. V případě potřeby můžete vícekrát logicky propojit jednu třídu s více jmény událostí. |
| convertMethod | Ne | Funkce v předpisu (x, e), kde x znamená cílová instance události aplikace, e znamená javascript systémovou událost. |

## Příklady implementací

- 🔌 [pClickConverter][pClickConverter]

[pClickConverter]: :inst:pClickConverter:.md "pClickConverter"
[ConvertedSystemEvent]: :_evt:ConvertedSystemEvent.md "ConvertedSystemEvent"
