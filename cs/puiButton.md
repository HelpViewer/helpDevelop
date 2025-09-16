# 🖥️ puiButton

## Účel pluginu

Tento plugin je vhodný pro zajištění jednoduchého 🔘 tlačítka s akcí pro uživatelské rozhraní.

## Konfigurace

1. Připravte konfiguraci s hodnotami:

| Název | Popis |
|---|---|
| ID | Id nového tlačítka. Musí být jedinečné napříč systémem, aby tlačítko nebylo propojeno s jinou akcí a nebo plugin jinou akci nepřepsal. |
| CAPTION | Titulek nebo ikonka pro tlačítko. Pokud **ID** tlačítka je definované jako klíč v lokalizaci, data se přepíší hodnotou překladového klíče. |
| TARGET | Cílový slot pro tlačítko. Obvyklé hodnoty: sidebar (boční panel), header (horní panel nad textem kapitoly). Hodnota může být jakákoli, avšak cílový plugin (páruje se podle ID pluginu) musí být schopen zpracovat událost ⚡ [ButtonSend][ButtonSend] jinak se tlačítko nikde nezobrazí. |

## Implementace

2. Nový plugin vždy bude mít [puiButton][puiButton] jako svou bázovou třídu.

```javascript
class puiButtonFullScreen extends puiButton {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_ID = 'downP-ToggleFS';
    this.DEFAULT_KEY_CFG_CAPTION = '🔲';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
  }
  
  _buttonAction(evt) {
    document.fullscreenElement 
      ? document.exitFullscreen() 
      : document.documentElement.requestFullscreen();
  }
}

Plugins.catalogize(puiButtonFullScreen);
```

- Řádky **this.DEFAULT_KEY_CFG_** mohou být odebrány, pokud chcete spoléhat pouze na konfiguraci ze souboru. S ohledem na automatickou dokumentaci objektů v pluginu však doporučuji je ponechat.
- **this.button** obsahuje odkaz na vytvořené tlačítko.

## Popis funkčnosti

- Funkce **_buttonAction**(evt) představuje handler pro obsluhu kliknutí na tlačítko.
- **evt** představuje ⚡ [ClickedEvent][ClickedEvent]

## Příklady implementací

- Potomci třídy 🖥️ [puiButton][puiButton]

### Scénář: Tlačítko se schováním v 📽 prezentačním režimu

```javascript
this.button.classList.add(C_HIDDENCPRESMODE);
```

[ButtonSend]: :_evt:ButtonSend.md "ButtonSend"
[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[puiButton]: :_plg:puiButton.md "puiButton"
