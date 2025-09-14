# ⭐ Zpracování javascript události

Zpracování javascript události slouží k napojení pluginu na systémovou javascript událost.

## Definice

### pConvertSysEventToEvent a konfigurace

Pokud je to možné, upřednostněte instanci pluginu 🔌 [pConvertSysEventToEvent][pConvertSysEventToEvent], kterou upravíte konfigurací. Výsledkem tohoto postupu je přeložená událost systému, kterou si může zachytit kterýkoli plugin prostřednictvím 👂 [obsluhy události][handler].

### Definice uvnitř vlastního pluginu

```javascript
class pSysEventHandling extends IPlugin {
  constructor(aliasName, data) {
    super(aliasName, data);
  }

  init() {
    const T = this.constructor;
    const TI = this;

    TI.SEVT_POPSTATE = new SystemEventHandler('', undefined, window, 'popstate', this._handlePopstate);
    TI.SEVT_POPSTATE.init();

    super.init();
  }

  _handlePopstate(e) {
  }
}
Plugins.catalogize(pSysEventHandling);
```

### Význam prvků

- TI.SEVT_POPSTATE - obsahuje instanci 🔌 [SystemEventHandler][SystemEventHandler], pluginu, který zajišťuje párování na javascript systémovou událost. Zde je ukázka párování na objekt **window**, událost **popstate**. 
- _handlePopstate - obsluha při zachycení události **popstate**
- e - objekt javascript systémové události

#### Parametry konstruktoru SystemEventHandler

| Parametr | Popis |
|---|---|
| aliasName | id pluginu (může zůstat '') |
| data | objekt s konfiguračními daty (může zůstat undefined) |
| target | cílový systémový objekt na který se má plugin napojit |
| eventName | jméno javascript systémové události |
| handler | handler pro událost na straně aplikace |

Dokumentace konfigurace pluginu 🔌 [pConvertSysEventToEvent][pConvertSysEventToEvent] je platná i zde.

### Další informace

Pro více informací k javascript systémovým událostem si projděte dokumentaci javascript standardu **ES2021** (**ECMA script**).  
Úvod na [geeksforgeeks][geeksforgeeks1] Vám může pomoci získat základní přehled.

[pConvertSysEventToEvent]: pConvertSysEventToEvent.md "pConvertSysEventToEvent"
[handler]: handler.md "Obsluha události"
[SystemEventHandler]: :_plg:SystemEventHandler.md "SystemEventHandler"
[geeksforgeeks1]: https://www.geeksforgeeks.org/javascript/javascript-events/ "JavaScript Events"
