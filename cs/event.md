# ⚡ Událost

Událost definuje událost/zprávu aplikace.  
Událost je možné definovat s obsluhou nebo pouze definovat (bez obsluhy).

## Definice

1. Definujte objekt dat události nebo určete, který z již definovaných potomků ⚡ [IEvent][IEvent] se vám pro událost hodí:

```javascript
class ClickHandlerRegister extends IEvent {
  constructor() {
    super();
    this.handlerId = undefined;
    this.handler = undefined;
  }
}
```

2. Definujte třídu pluginu pro událost:

```javascript
class pEventPlugin extends IPlugin {
  static EVT_CLICK_HANDLER_REGISTER = 'ClickHandlerRegister';

  init() {
    const T = this.constructor;
    const TI = this;

    // (B)

    super.init();
  }
}
Plugins.catalogize(pEventPlugin);
```

3. Rozhodněte, zda můžete mít obsluhu přímo v pluginu nebo ji potřebujete mít právě mimo plugin. Podle svého případu si vyberte potřebný postup podle dalších kapitol.

4. Zdroj kódu kapitoly pak vždy vložte do místa komentáře **(B)**.

### ⚡ Událost s obsluhou

```javascript
    const h_EVT_CLICK_HANDLER_REGISTER = (reply) => {
      // ...
      reply.result = 'replyValue';
    }
    TI.eventDefinitions.push([T.EVT_CLICK_HANDLER_REGISTER, ClickHandlerRegister, h_EVT_CLICK_HANDLER_REGISTER]);
```

### 📄⚡ Událost pouze definovaná

```javascript
    TI.eventDefinitions.push([T.EVT_CLICK_HANDLER_REGISTER, ClickHandlerRegister, null]); // outside event handlers
```

### Význam prvků

- class ClickHandlerRegister - datový objekt události (je možné použít stejnou třídu u více událostí nebo dědit z kteréhokoli potomka IEvent)
- ClickHandlerRegister.constructor - obsahuje výchozí hodnoty objektu zprávy. Je žádoucí, aby se hodnoty, pokud je to možné předvyplnily ideálně výchozí hodnotou podle plánovaného typu. Tato data jsou používána v [prohlížeči objektů][oexplorer] jako součást automatické dokumentace systému.
- const h_EVT_CLICK_HANDLER_REGISTER - obsluha události
- reply.result - standardní vlastnost události (⚡ [IEvent][IEvent]), která je automaticky aplikační logikou přebírána jako odpověď obsluhy na událost. Může to být jakýkoli objekt.
- TI.eventDefinitions.push([T.EVT_CLICK_HANDLER_REGISTER, ClickHandlerRegister, null]) - vytvoří předpis definice události (jméno události, objekt dat události a obslužná metoda nebo null pokud má být událost pouze definována). O zpracování definic se stará předek 🔌 [IPlugin][IPlugin].
- super.init(); - provádí standardní inicializace vazeb. Musí být posledním příkazem, aby se řádně inicializovalo vše definované.

## Zasílání události

V obslužném kódu pak můžete události vyvolávat takto:

```javascript
      const eventName = EventNames.MyNewEvent; //nebo: 'MyNewEvent'

      sendEvent(eventName, (r) => {
        r.id = aliasName;
        r.result = loadedCount;
        //vyplnění dalších potřebných dat
      });
```

V souboru **appmainBaseLogic.js** naleznete příklady funkcí, které podobná volání zapouzdřují.  
> [!WARNING] 
> Je doporučeno si pro svůj plugin založit podobnou sadu funkcí v odděleném souboru (který vložíte do [seznamu skriptů](js.lst.md "Seznam skriptů")). Volání metody **sendEvent** se neindexuje pro [prohlížeč objektů](oexplorer.md "Prohlížeč objektů"), ale tyto funkce budou indexovány.

## Záznamy 🛰️

Záznam v 🛰️ [prohlížeči objektů][oexplorer] znamená, že: 

- v přehledu instance pluginu : plugin odesílá událost ...
- u seznamu komunikačních cest události : událost je odesílána z ...

[IEvent]: :_evt:IEvent.md "IEvent"
[oexplorer]: oexplorer.md "Prohlížeč objektů"
[IPlugin]: :_plg:IPlugin.md "IPlugin"
