# ▼ Filtrování událostí v pluginech

Každý plugin může přijímat události ze systému. V pluginech existuje přepínač na (de)aktivaci filtru na příjem událostí podle **aliasName (id)** instance pluginu:

```javascript
this.eventIdStrict = true;
```

Volání provádějte v konstruktoru nebo na začátku funkce init() nebo nejpozději před voláním base.init().

Filtrování událostí je dvoustupňové - podle eventIdStrict a jména obslužné funkce. V následujících podkapitolách je popsáno podrobněji.

## Úvodní souhrn

- Funkce **onET_(jméno události)** přijímá všechny události s eventName = (jméno události)
- Funkce **onET(jméno události)** přijímá všechny události s eventName = (jméno události) a id = plugin.aliasName
- **Plugin s plugin.aliasName = ''** přijímá všechny události do funkce **onET(jméno události)** nebo **onET_(jméno události)**

⚠️ V pluginu je doporučeno mít jen jednu obsluhu z těchto:

- onET(jméno události)
- onET_(jméno události)

## Jak rozhodnout nastavení?

Plugin by neměl poslouchat všechny události, ale budou se zasílat jen některé přímo jemu, proto dostane konkrétní id a eventIdStrict = true.

EventIdStrict na **true** nastavte minimálně v těchto případech:

- Plugin bude (nebo může) běžet ve více než jedné instanci (například 📇 slovník klíčových slov a 🔎 fulltext hledání)
- Plugin bude součástí procesu (🖼️ [pTRPhasePlugin][pTRPhasePlugin] - vypisování obsahu kapitoly)
- Plugin bude součástí většího funkčního celku (🔹 [pIndexFile:fulltextList][pIndexFile] - dynamické vytvoření fulltext indexu nápovědy)

📘 K této kapitole je k dispozici [podrobná příloha][appendix].

[pTRPhasePlugin]: pTRPhasePlugin.md "pTRPhasePlugin"
[pIndexFile]: :inst:pIndexFile:fulltextList.md "pIndexFile:fulltextList"
[appendix]: eventFilterD.md "Rozbor filtrování událostí v pluginech"