# 🧩 První plugin

## Postup vytvoření pluginu

Pro vývoj nového pluginu je potřeba provést následující:

1. Definovat co přesně má plugin zajišťovat. Podle vhodnosti k danému účelu zvolte předka pro daný plugin (**extends**). Obsah pluginu bude přinejmenším odpovídat minimálnímu pluginu - **IPlugin**.

### Balík nápovědy

Pokud chcete plugin přidat do nápovědy, pak:

2. Založte v repozitáři nápovědy v adresáři **_base** soubor:
   - **plugins.lst** (seznam pluginů),
   - adresáře **plugins** a **plugins-config**

a dále postupujte podle kapitoly **Balík programu**.

### Balík programu

Pokud plugin chcete přidat do sestavení HelpVieweru:

3. Do [seznamu pluginů][plugins] zaveďte plugin definičním řádkem: 
   - **[jméno třídy]** pokud má být plugin pouze načten (je předkem pro jiné pluginy, ale není určen k samostatné práci)
   - **[jméno třídy]:[jméno instance]** pokud má být plugin načten a je určen k zajištění funkcionality
4. Do umístění **zip/plugins-config/[jméno třídy]_[jméno instance].cfg** vložte konfigurační definice pro novou instanci.
5. Do umístění **zip/plugins/[jméno třídy].js** vložte zdrojový kód pluginu.

V případě nápověd použijte umístění bez **zip/**.

## Minimální plugin

```javascript
class pMinPlugin extends IPlugin {
  constructor(aliasName, data) {
    super(aliasName, data);
  }

  init() {
    //const T = this.constructor;
    //const TI = this;
    
    super.init();
  }

  deInit() {
    super.deInit();
  }
}

Plugins.catalogize(pMinPlugin);

```

- Volání **Plugins.catalogize(pMinPlugin);** je povinné, protože provede zavedení pluginu do katalogu načtených pluginů. Následně na základě znalosti jména pluginu je možné si vyžádat jeho instance. Na základě dat v **[plugins][plugins].lst** toto udělá aplikace sama.
- Volání **super.** by mělo být první u konstruktoru a u init a deinit poslední. Zajišťují aplikaci obecné spoelčné logiky.
- const T a TI jsou zkratky pro přístup k this a ke třídě. Je to napříč systémem doporučená koncepce psaní.
- V případě, že máte ve funkci pouze volání super. , můžete funkci odebrat zcela. Zde v ukázce je vše uvedeno pro rychlý obecný přehled.

## Základní pluginy

| Název | Popis |
|---|---|
| 🔌 [IPlugin][IPlugin] | Základní plugin pro všechny pluginy v systému. Poskytuje základní funkce pro obecný plugin. Je určen pro pluginy služeb nebo posluchačů událostí, které samy nebudou zajišťovat žádný prvek uživatelského rozhraní. |
| 🔌 [pConvertSysEventToEvent][pConvertSysEventToEvent] | Plugin převádí definovanou javascript událost na událost aplikace, která může být zachycena jiným pluginem. |
| 🔌 [pServicePlugin][pServicePlugin] | Plugin pro rozšiřující služby. Základem jsou obsluhy napojené na události pluginu 🔌 [pPluginManagement][pPluginManagement]. |

### Uživatelské rozhraní

| Název | Popis |
|---|---|
| 🖥️ [puiButton][puiButton] | 🔘 Tlačítko pro uživatelské rozhraní. Obsluha akce musí být součástí zdroje pluginu. |
| 🖥️ [puiButtonTab][puiButtonTab] | 🔘🎛️ Tlačítko a karta bočního panelu. |
| 🖥️ [puiButtonTabTree][puiButtonTabTree] | 🔘🎛️📂 Tlačítko a karta bočního panelu s komponentou strom. |
| 🖥️ [puiButtonSelect][puiButtonSelect] | 🔘▼ Tlačítko s výběrovým seznamem. |

### Výpis textu kapitol

| Název | Popis |
|---|---|
| 🖼️ [pTRPhasePlugin][pTRPhasePlugin] | Plugin přijímá událost ⚡ [ShowChapterResolutions][ShowChapterResolutions] od pluginu 🖼️ [pTopicRenderer][pTopicRenderer] a provede jednotlivý krok procesního zpracování. Jednou z jeho aplikací je například parsování md souboru pro výpis do textu kapitoly. |

## Příklady implementací

- 🖼️ [pTREmptyPlugin][pTREmptyPlugin]

[pTREmptyPlugin]: :_cpp:pTREmptyPlugin.md "Prázdný plugin"
[IPlugin]: :_plg:IPlugin.md "IPlugin"
[pConvertSysEventToEvent]: pConvertSysEventToEvent.md "pConvertSysEventToEvent"
[pTRPhasePlugin]: pTRPhasePlugin.md "pTRPhasePlugin"
[ShowChapterResolutions]: :_evt:ShowChapterResolutions.md "ShowChapterResolutions"
[pTopicRenderer]: pTopicRenderer.md "pTopicRenderer"
[puiButton]: puiButton.md "puiButton"
[puiButtonTab]:puiButtonTab.md "puiButtonTab"
[puiButtonTabTree]: puiButtonTabTree.md "puiButtonTabTree"
[puiButtonSelect]: puiButtonSelect.md "puiButtonSelect"
[plugins]: plugins.lst.md "Seznam pluginů"
[pServicePlugin]: pServicePlugin.md "pServicePlugin"
[pPluginManagement]: :_plg:pPluginManagement.md "pPluginManagement"
