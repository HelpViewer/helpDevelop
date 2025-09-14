# 📂 Strom

Je doporučeno použít přímo plugin: 🖥️ [puiButtonTabTree][puiButtonTabTree], který funkcionalitu zajišťuje včetně konfigurace, karty, aktivačního tlačítka a dalších podpůrných akcí.

Komponenta nadefinuje standardní HTML ul element, které je upravený CSS třídou **.tree**.

## Definice

1. V pluginu v init definujte objekt stromu obsluhu jeho položek (výpis zkrácen na init funkci):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    const id = 'tabId';
    const role = '';
    TI.tab = uiAddSidebarPage(id, role);

    TI.cfgTreeId = 'NewTreeId';
    TI.tree = uiAddTreeView(TI.cfgTreeId, TI.tab);

    registerOnClick(TI.cfgTreeId, (e) => {
      const result = TI._treeClick(e);
      _notifyClickedEvent(e, result, TI.cfgTreeId);
    });

    super.init();
  }

  _treeClick(e) {
  }
```

## Význam prvků

- TI.tab - odkaz na HTML element karty nadřízené stromu
- const id - id nadřízené karty
- TI.cfgTreeId - id nového stromu
- uiAddTreeView - založí novou komponentu stromu
- registerOnClick - přidá do seznamu obsluh kliknutí myši základní předponu všech položek nového stromu. Je vhodné, aby id stromu bylo jedinečné napříč systémem, aby se obsluhy navzájem pluginů nepřepsaly
- _notifyClickedEvent - odešle událost ⚡ [ClickedEventTree][ClickedEventTree], kterou dále zpracuje plugin 🖥️ [pui][pui] a to zalogováním, případně odesláním události ⚡ [ClickedEventNotForwarded][ClickedEventNotForwarded] pokud se nepodaří najít událost pro základní předponu položek

[ClickedEventTree]: :_evt:ClickedEventTree.md "ClickedEventTree"
[ClickedEventNotForwarded]: :_evt:ClickedEventNotForwarded.md "ClickedEventNotForwarded"
[puiButtonTabTree]: puiButtonTabTree.md "puiButtonTabTree"
[pui]: :_plg:pui.md "pui"
