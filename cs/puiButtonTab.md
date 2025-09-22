# 🖥️ puiButtonTab

## Účel pluginu

Tento plugin je vhodný pro zajištění 🔘🎛️ tlačítka a karty bočního panelu.

## Konfigurace

1. Připravte konfiguraci s hodnotami stejně jako pro komponentu 🖥️ [puiButton][puiButtonC].

## Implementace

2. Nový plugin vždy bude mít [puiButtonTab][puiButtonTab] jako svou bázovou třídu.

```javascript
class puiNewButtonWithTab extends puiButtonTab {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_ID = 'downP-NewButton';
    this.DEFAULT_KEY_CFG_CAPTION = '🤡';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
  }

  _preShowAction(evt) {
    //this.tab
  }

  //_buttonAction(evt) {
  //}

}

Plugins.catalogize(puiNewButtonWithTab);
```

- Řádky **this.DEFAULT_KEY_CFG_** mohou být odebrány, pokud chcete spoléhat pouze na konfiguraci ze souboru. S ohledem na automatickou dokumentaci objektů v pluginu však doporučuji je ponechat.

| Objekt | Popis |
|---|---|
| this.tab | Odkaz na HTML element karty. Je možno do ní připojit další objekty |
| this.button | Odkaz na HTML element tlačítka |
| parametr evt | Událost aplikace, ⚡ [ClickedEvent][ClickedEvent] |
| _preShowAction(evt) | Je spouštěna před zobrazením karty uživateli. Je ideální k odloženému načtení dat pluginu, která jsou zobrazována uživateli na dané kartě, případně k přípravě konfiguračního formuláře pro další akci. V potomkovi by měla být přepsána i prázdnou funkcí. Pokud funkce vrátí **false**, tak se karta uživateli nezobrazí. |
| _buttonAction(evt) | Akce tlačítka. Obvykle není třeba ji přepisovat, pokud postačuje pouhé zobrazení karty uživateli |

## Popis funkčnosti

- Funkce **_buttonAction**(evt) představuje handler pro obsluhu kliknutí na tlačítko. Výchozí obsluha je zajištěna z předka, ale může být žádoucí ji přepsat, viz. Příklady implementací níže.
- Ve výchozím chování funkce provolá **_preShowAction**(evt) a  
zobrazí kartu komponenty na panelu.
- **_preShowAction**(evt) může vrátit false, aby zablokovala zobrazení karty uživateli. Pokud vrátí undefined (výchozí chování) nebo true, kartu plugin v pořádku zobrazí.

## Příklady implementací

- 🖥️ [puiButtonChangeLanguage][puiButtonChangeLanguage]

### Tlačítko s akcemi podle viditelnosti záložky - _buttonAction(evt)

Pokud funkci _buttonAction nadefinujete tímto způsobem:

```javascript
  _buttonAction(evt) {
    if (this.tab.classList.contains(C_HIDDENC)) {
      super._buttonAction();
    } else {
      // (B)
    }
  }
```

získáte dvoukrokové zpracování:

- první kliknutí : zobrazí skrytou záložku (obvykle s připraveným formulářem)
- druhé kliknutí : provede další operaci ve větvi **(B)** s daty, která si převezme z formuláře

Ukázka: 🖥️ [puiButtonAsBook][cpuiButtonAsBook]

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[puiButtonTab]: :_plg:puiButtonTab.md "puiButtonTab"
[puiButtonC]: puiButton.md#h-2-1 "puiButton"
[cpuiButtonAsBook]: :_cpp:puiButtonAsBook.md "puiButtonAsBook"
[puiButtonChangeLanguage]: :_plg:puiButtonChangeLanguage.md "puiButtonChangeLanguage"
