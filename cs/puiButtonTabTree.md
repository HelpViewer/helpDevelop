# 🖥️ puiButtonTabTree

## Účel pluginu

Tento plugin je vhodný pro zajištění 🔘🎛️📂 tlačítka a karty bočního panelu s komponentou strom.

## Konfigurace

1. Připravte konfiguraci s hodnotami stejně jako pro komponentu 🖥️ [puiButton][puiButtonC].
2. Přidejte klíč **TREEID**, ve kterém bude jméno nového stromu

## Implementace

3. Nový plugin vždy bude mít [puiButtonTabTree][puiButtonTabTree] jako svou bázovou třídu.

```javascript
class puiNewButtonWithTree extends puiButtonTabTree {
  constructor(aliasName, data) {
    super(aliasName, data);
    
    this.DEFAULT_KEY_CFG_ID = 'downP-NewTree';
    this.DEFAULT_KEY_CFG_CAPTION = '📂';
    this.DEFAULT_KEY_CFG_TARGET = UI_PLUGIN_SIDEBAR;
    
    this.DEFAULT_KEY_CFG_TREEID = newtree';
    //setTreeData(data, this.aliasName, append);
  }
  
  //_buttonAction(evt) {
  //}

  _preShowAction(evt) {
  }

  _preStandardInit() {
  }

  _treeClick(e) {
  }
}

Plugins.catalogize(puiNewButtonWithTree);
```

- Řádky **this.DEFAULT_KEY_CFG_** mohou být odebrány, pokud chcete spoléhat pouze na konfiguraci ze souboru. S ohledem na automatickou dokumentaci objektů v pluginu však doporučuji je ponechat.

| Objekt | Popis |
|---|---|
| this.tab | Odkaz na HTML element karty. Je možno do ní připojit další objekty |
| this.button | Odkaz na HTML element tlačítka |
| this.tree | Odkaz na HTML element stromu (**ul** element) |
| parametr evt | Událost aplikace, ⚡ [ClickedEvent][ClickedEvent] |
| _preStandardInit | Je spouštěna před vytvořením komponenty strom na kartě. Je určena pro založení dalších komponent v případě potřeby. |
| _preShowAction(evt) | Je spouštěna před zobrazením karty uživateli. Je ideální k odloženému načtení dat pluginu, která jsou zobrazována uživateli na dané kartě, případně k přípravě konfiguračního formuláře pro další akci. V potomkovi by měla být přepsána i prázdnou funkcí. Pokud funkce vrátí **false**, tak se karta uživateli nezobrazí. |
| _buttonAction(evt) | Akce tlačítka. Obvykle není třeba ji přepisovat, pokud postačuje pouhé zobrazení karty uživateli |
| _treeClick(e) | Akce kliknutí na položku stromu, ⚡ [ClickedEventTree][ClickedEventTree]. Pokud není přepsána, převezme sdílenou obsluhu **processAClick** z **appmainBaseLogic.js** (tato obsluha je již na hranici obecného řešení a konkrétní implementace). |
| setTreeData(data, this.aliasName, append); | Provede nastavení [dat stromu][treedata] z řetězce data. Pro identifikaci se použije aliasName pluginu. Append může být neuveden a nebo **true**, pokud chcete připojit nějaká data na konec stromu. |

Pokud Vám nevyhovuje funkce **setTreeData**, můžete použít funkci nižší úrovně, kterou tato funkce zapouzdřuje - **linesToHtmlTree**(data, alias) - data je opět řetězec [dat stromu][treedata] a alias zde je hodnota konfigurace **TREEID**.

## Popis funkčnosti

- Funkce **_preStandardInit**() je spuštěna automaticky při vytvoření instance pluginu.
- Funkce **_buttonAction**(evt) představuje handler pro obsluhu kliknutí na tlačítko. Výchozí obsluha je zajištěna z předka. Přepsání se nepředpokládá, ale je možné.
- Ve výchozím chování funkce provolá **_preShowAction**(evt) a  
zobrazí kartu komponenty na panelu.
- **_preShowAction**(evt) může vrátit false, aby zablokovala zobrazení karty uživateli. Pokud vrátí undefined (výchozí chování) nebo true, kartu plugin v pořádku zobrazí.

## Příklady implementací

- 🖥️ [puiButtonObjectExplorer][puiButtonObjectExplorer] a další potomci 🖥️ [puiButtonTabTree][puiButtonTabTree]

### Scénář: Tlačítko s akcí otevři/zavři vše

Pokud funkci _buttonAction nadefinujete tímto způsobem:

```javascript
  _buttonAction(evt) {
    this._buttonActionClickOpenCloseAll(evt?.event?.isTrusted);
  }
```

získáte přepínač, který v případě kliknutí na tlačítko provede 3 stavy:

- Karta není viditelná -> zobrazí kartu se stromem.
- Karta je viditelná, existuje alespoň jedna neotevřená položka -> všechny položky stromu se otevřou.
- Karta je viditelná, všechny položky jsou otevřené -> všechny položky stromu se zavřou.

Ukázka: 🖥️ [puiButtonTOC][cpuiButtonTOC]

[ClickedEvent]: :_evt:ClickedEvent.md "ClickedEvent"
[ClickedEventTree]: :_evt:ClickedEventTree.md "ClickedEventTree"
[puiButtonTabTree]: :_plg:puiButtonTabTree.md "puiButtonTabTree"
[puiButtonC]: puiButton.md#h-2-1 "puiButton"
[cpuiButtonTOC]: :_cpp:puiButtonTOC.md "puiButtonTOC"
[puiButtonObjectExplorer]: :_plg:puiButtonObjectExplorer.md "puiButtonObjectExplorer"
[treedata]: ?d=hlp-aguide/Help-__.zip&p=mdata%2Ftree.lst.md "tree input data format"
