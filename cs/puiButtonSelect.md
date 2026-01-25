# 🖥️ puiButtonSelect

## Účel pluginu

Tento plugin je vhodný pro zajištění jednoduchého 🔘▼ tlačítka s výběrovým seznamem.

## Konfigurace

1. Připravte konfiguraci s hodnotami podle [puiButton][puiButton].

## Implementace

2. Nový plugin vždy bude mít [puiButtonSelect][puiButtonSelect] jako svou bázovou třídu.

```javascript
class puiButtonSelectNew extends puiButtonSelect {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_ID = 'downP-selNew';
    this.DEFAULT_KEY_CFG_CAPTION = '🖼️';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
  }

  async init() {
    // ... inicializace událostí aplikace vložte zde ...

    super.init();

    // ... inicializace dat komponenty vložte zde ...

    const items = ['A', 'B', 'C']; // položky
    const selVal = 'B'; // výchozí vybraná hodnota

    appendComboBoxItems(this.select, items, selVal);
  }

  deInit() {
    super.deInit();
  }

  _handle(e) {
    const newVal = e.target.options[e.target.selectedIndex].text;
    // ...
  }

  _handleFocus(e) {
    // ...
  }

  // ...
}

Plugins.catalogize(puiButtonSelectNew);

```

- Řádky **this.DEFAULT_KEY_CFG_** mohou být odebrány, pokud chcete spoléhat pouze na konfiguraci ze souboru. S ohledem na automatickou dokumentaci objektů v pluginu však doporučuji je ponechat.

## Popis funkčnosti

- **this.select** obsahuje odkaz na vytvořený výběrový seznam
- **e** představuje javascript systémové události
- **appendComboBoxItems** připojí množinu položek do výběrového pole. Indexy jsou přiřazeny od 0
- **e.target.selectedIndex** index vybrané položky
- **e.target.options\[e.target.selectedIndex\].text** text vybrané položky
- **this.select.options.length = 0** smaže položky výběrového pole
- **_handleFocus** akce před otevřením seznamu možných voleb
- **sendEvent('ButtonSelectIconSet', (x) => {x.payload = '🖥️'; id = '';});** změní ikonu tlačítka na 🖥️

## Jazykové řetězce

V **zip/lang/(jazyk)/lstr.txt**, například pro pole **downP-selNew** doplňte klíče:

| Klíč | Hodnota | Význam |
| --- | --- | --- |
| downP-selNew | zadejte | Popisek bublinové nápovědy |
| downP-selNew-lab__innerText | zadejte | Popisek titulku pro přístupnost |
| downP-selNew__aria-label | prázdné | aria-label atribut na div prvku, který zapouzdřuje výběrové pole (důvodem je možná duplicita při čtení asistivní čtečkou) | 

## Příklady implementací

- 🖥️ [puiButtonSelectSkin][puiButtonSelectSkin] a další potomci třídy 🖥️ [puiButtonSelect][puiButtonSelect]

[puiButton]: puiButton.md#h-2-1 "puiButton"
[puiButtonSelect]: :_plg:puiButtonSelect.md "puiButtonSelect"
[puiButtonSelectSkin]: :_plg:puiButtonSelectSkin.md "puiButtonSelectSkin"
