# 🔀 Směrování kliknutí myši

Tento objekt je spravován pluginem 🖥️ [pui][pui]. Je to slovník předpon jmen a nebo konkrétních jmen, pod kterými jsou uloženy obslužné metody. Tuto strukturu technologicky využívají ostatní pluginy. Je zde dovoleno nadefinovat i vlastní obsluhu.

## Definice

1. V pluginu v init definujete objekt zdroje takto (výpis zkrácen na init funkce):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    TI.cfgTreeId = 'NewTreeId';
    registerOnClick(TI.cfgTreeId, (evt) => {
      TI._treeClick(evt);
    });

    super.init();
  }

  _treeClick(evt) {
  }
```

V [prohlížeči objektů][oexplorer] je tato položka k dohledání pod pluginem 🖥️ [pui][puir].

## Význam prvků

- TI.cfgTreeId - id klíč pro předání události ⚡ [ClickedEvent][ClickedEvent]. Událost bude do připojené obsluhy předána pokud klíč ve směrování bude shodný s:
  - id objektu úplně,
  - první částí id prvku (části id prvku se dělí podle znaku **|** a **-**. Důvodem je skutečnost, že stromové komponenty mají společný handler pro své položky, přičemž tento handler je zde také zaveden)

## Příklady implementací

- 🖥️ [pui][puir] - řídící plugin logiky UI rozhraní

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[oexplorer]: oexplorer.md "Prohlížeč objektů"
[pui]: :_plg:pui.md "pui"
[puir]: :_inst:pui:.md#h-2-1 "pui směrovací tabulka"
