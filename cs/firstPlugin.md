# 🧩 První plugin

## Postup vytvoření pluginu

Pro vývoj nového pluginu je potřeba provést následující:

1. Definovat co přesně má plugin zajišťovat. Podle vhodnosti k danému účelu zvolte předka pro daný plugin (**extends**). Obsah pluginu bude přinejmenším odpovídat minimálnímu pluginu - **IPlugin**.
2. Do seznamu [pluginů][plugins] zaveďte plugin definičním řádkem: 
   - **[jméno třídy]** pokud má být plugin pouze načten (je předkem pro jiné pluginy, ale není určen k samostatné práci)
   - **[jméno třídy]:[jméno instance]** pokud má být plugin načten a je určen k zajištění funkcionality
3. Do umístění **zip/plugins-config/[jméno třídy]_[jméno instance].cfg** vložte konfigurační definice pro novou instanci.
4. Do umístění **zip/plugins/[jméno třídy].js** vložte zdrojový kód pluginu.

## Minimální plugin

```javascript
class pMinPlugin extends IPlugin {
  constructor(aliasName, data) {
    super(aliasName, data);
  }

  init() {
    super.init();
  }

  deInit() {
    super.deInit();
  }
}

Plugins.catalogize(pMinPlugin);

```

## Základní pluginy

| Název | Popis |
|---|---|
| 🔌 [IPlugin][IPlugin] | Základní plugin pro všechny pluginy v systému. Poskytuje základní funkce pro obecný plugin. Je určen pro pluginy služeb nebo posluchačů událostí, které samy nebudou zajišťovat žádný prvek uživatelského rozhraní. |
| 🔌 [pConvertSysEventToEvent][pConvertSysEventToEvent] | Plugin převádí definovanou javascript událost na událost aplikace, která může být zachycena jiným pluginem. |
| 🖼️ [pTRPhasePlugin][pTRPhasePlugin] | Plugin přijímá událost ⚡ [ShowChapterResolutions][ShowChapterResolutions] od pluginu [pTopicRenderer][pTopicRenderer] a provede jednotlivý krok procesního zpracování. Jednou z jeho aplikací je například parsování md souboru pro výpis do textu kapitoly. |
| 🖥️ [puiButton][puiButton] | 🔘 Tlačítko pro uživatelské rozhraní. Obsluha akce musí být součástí zdroje pluginu. |
| 🖥️ [puiButtonTab][puiButtonTab] | 🔘🎛️ Tlačítko a karta bočního panelu. |
| 🖥️ [puiButtonTabTree][puiButtonTabTree] | 🔘🎛️📂 Tlačítko a karta bočního panelu s komponentou strom. |

[pTREmptyPlugin]: :_cpp:pTREmptyPlugin.md "Prázdný plugin"
[IPlugin]: :_plg:IPlugin.md "IPlugin"
[pConvertSysEventToEvent]: :_plg:pConvertSysEventToEvent.md "pConvertSysEventToEvent"
[pTRPhasePlugin]: :_plg:pTRPhasePlugin.md "pTRPhasePlugin"
[ShowChapterResolutions]: :_evt:ShowChapterResolutions.md "ShowChapterResolutions"
[pTopicRenderer]: :_plg:pTopicRenderer.md "pTopicRenderer"
[puiButton]: :_plg:puiButton.md "puiButton"
[puiButtonTab]: :_plg:puiButtonTab.md "puiButtonTab"
[puiButtonTabTree]: :_plg:puiButtonTabTree.md "puiButtonTabTree"
[plugins]: plugins.lst.md "Seznam pluginů"
