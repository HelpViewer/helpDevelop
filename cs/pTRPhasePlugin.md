# 🖼️ pTRPhasePlugin

## Účel pluginu

Plugin přijímá událost ⚡ [ShowChapterResolutions][ShowChapterResolutions] od pluginu 🖼️ [pTopicRenderer][pTopicRenderer] a provede jednotlivý krok procesního zpracování. Plugin pTopicRenderer má ve své konfiguraci definovaný seznam procesních fází a zajišťuje postup jednotlivých zpráv celým procesem.

## Implementace

1. V souboru **plugins.lst** zaveďte řádek:  
   pConvertSysEventToEvent:[instanceid]
2. Připravte v souboru **plugins/[název pluginu].js** například následující kód:

```javascript
class pTRNewPlugin extends pTRPhasePlugin {
  onETShowChapterResolutions(r) {
  }
}

Plugins.catalogize(pTRNewPlugin);
```

onETShowChapterResolutions je odpovědná za prováděný procesní krok. Parametr r je událost ⚡ ShowChapterResolutions. Událost sama obsahuje veškeré podpůrné objekty a metody pro načtení, přípravu či provedení výpisu textu do výstupního HTML prvku pro kapitolu. 

### onETShowChapterResolutions - vybrané vlastnosti

| Vlastnost | Popis |
|---|---|
| doc | Odkaz na konkrétní HTML prvek, který přijme výstup výpisu |
| getStorageData | Odkaz na funkci pro čtení zdroje, který určil plugin 🖼️ [pTRTriage][pTRTriage] na základě vzorů URI adres kapitol a dalších dat. |
| tokens | Shromážděné tokeny (řetězce) během předchozích kroků zpracování. Je možné v některém kroku založit token a v jiném kroku jej zpracovat a provést doplňkovou logiku. |
| onTokenDo | Otestuje, zda zadaný token existuje. Pokud ano, tak jej odebere a provede vloženou funkci. |
| preventDefault | Umožňuje provolat preventDefault na javascript systémové události. Volání je podle standardu nevratné. |
| stopAllPhases | Nastavením na **true** přerušíte další zpracování procesu. Kombinujte se **stop = true**. |

⚠️ V rámci procesu se užívá asynchronicita. Její provolání provádějte vždy takto:  
r.result = r.result.then(() => ...);  
aby jednotlivé kroky na sebe navazovaly.  
Můžete také připojit více událostí ke stejnému result objektu, ale je doporučeno řazení kroků jeden za druhým.

## Příklady implementací

- 🖼️ [pTREmptyPlugin][pTREmptyPlugin]
- 🖼️ [pTRParseMd][pTRParseMd]
- 🖼️ [pTRLoadData][pTRLoadData]

## Další pluginy

- 🖼️ [pTopicRenderer][pTopicRenderer]

[pTRTriage]: :inst:pTRTriage:-triage.md "pTRTriage"
[pTREmptyPlugin]: :inst:pTREmptyPlugin:-htm.md "pTREmptyPlugin"
[ShowChapterResolutions]: :_evt:ShowChapterResolutions.md "ShowChapterResolutions"
[pTopicRenderer]: :_plg:pTopicRenderer.md "pTopicRenderer"
[pTRParseMd]: :_plg:pTRParseMd.md "pTRParseMd"
[pTRLoadData]: :_plg:pTRLoadData.md "pTRLoadData"
