# 🔘 Tlačítko

Je doporučeno použít přímo plugin: 🖥️ [puiButton][puiButton], který funkcionalitu zajišťuje včetně konfigurace.

Komponenta nadefinuje standardní HTML tlačítko, které je upravené CSS třídou **.pnl-btn** a to ve všech umístěních. Pokud je potřeba, aby tlačítko na každém panelu vypadalo jinak, nastylujte selektor potomka tříd (**.topPanel .pnl-btn**).

## Definice

1. V pluginu v init definujte objekt tlačítka a jeho obsluhu (výpis zkrácen na init funkci):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    this.cfgId = 'NewBtnId';
    this.cfgCaption = '🔘';
    this.cfgTarget = UI_PLUGIN_SIDEBAR;
    this.button = uiAddButton(this.cfgId, this.cfgCaption, this.cfgTarget, this._buttonAction);

    super.init();
  }

  _buttonAction(evt) {
    alert('Ahoj.');
  }
```

## Význam prvků

- this.button - obsahuje odkaz na HTML element tlačítka
- this.cfgId - id nového tlačítka
- this.cfgCaption - text nového tlačítka (nebo ikonka)
- this.cfgTarget - cílový panel pro tlačítko
- _buttonAction - obsluha kliknutí na tlačítko
- evt - událost ⚡ [ClickedEvent][ClickedEvent]

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[puiButton]: puiButton.md "puiButton"
