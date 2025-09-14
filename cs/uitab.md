# 🎛️ Karta

Je doporučeno použít přímo plugin: 🖥️ [puiButtonTab][puiButtonTab], který funkcionalitu zajišťuje včetně konfigurace a tlačítka, které slouží k zobrazení této karty. Tlačítko v tomto pluginu může být nezávisle na kartě umístěno na kterýkoli dostupný panel.

Komponenta nadefinuje standardní HTML div, který vloží do bočního panelu jako skrytý.

## Definice

1. V pluginu v init definujte objekt karty (výpis zkrácen na init funkci):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    const id = 'NewTabId';
    const role = '';
    this.tab = uiAddSidebarPage(id, role);

    super.init();
  }
```

## Význam prvků

- id - id nové záložky
- role - ARIA role, obvykle nechte prázdné

[puiButtonTab]:puiButtonTab.md "puiButtonTab"
