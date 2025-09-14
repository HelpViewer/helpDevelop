# 📦 Zdroj

Cílem pluginu 📦 [Resource][Resource] je zajistit základní definici a proces zavádění externích balíčků. K inicializaci postačí pouhý seznam souborů oddělených středníkem. Plugin není schopný zcela samostatné práce, protože proces zavádění je specifický v konkrétním scénáři. Z pluginu je sice možno vytvořit novou třídu, doporučuje se však jeho pouhé použití s tím, že o zavádění a kontrolu stavu zavedení se postará nadřízený plugin, který řídí procesní krok.

## Definice

1. V pluginu v init definujete objekt zdroje takto (výpis zkrácen na init funkci):

```javascript
  init() {
    const T = this.constructor;
    const TI = this;
    
    const filename = 'marked.min.js;LICENSE-marked.md';
    TI.RES_MARKED = new Resource('MARKED', undefined, STO_DATA, filename);

    super.init();
  }

  onETShowChapterResolutions(r) {
    if (!window.marked)
      r.result = this.RES_MARKED?.init(r.result);

    r.result = (!r.content || r.content.length == 0) ? r.result : r.result.then(() => r.content = marked.parse(r.content));
  }
```

## Význam prvků

- const filename - seznam souborů balíčku oddělený středníky. Cesty jsou relativní vzhledem k základnímu adresáři úložiště. Může být přebírán z konfigurace pluginu.
- this.RES_MARKED?.init provede inicializaci zdroje (zavedení souborů **js** a **css** ze seznamu)

## Vytvoření instance pluginu

new Resource('MARKED', undefined, STO_DATA, filename):

| Parametr | Výchozí | Popis |
|---|---|---|
| aliasName | povinný | id pluginu. Definujete alias, který bude použit jako název tohoto zdroje/balíčku v [prohlížeči objektů][oexplorer] |
| data | povinný | Zadejte undefined. Jedná se o data konfigurace - klíč hodnota. Plugin nepočítá s žádnou konfigurací |
| source | STO_DATA | Jméno zdrojového souboru dat. Hodnoty: STO_DATA (aplikace), STO_HELP (nápověda/datový soubor) |
| fileList | '' | Seznam souborů oddělených středníky |

Ukázka v příkaldu založí instanci pluginu 📦 [Resource][Resource] s názvem MARKED, bez konfigurace. Data hledá v datech aplikace (**data.zip**). Obsahem balíčku jsou soubory z fileList.

## Funkce pluginu Resource

Plugin Resource zapouzdřuje:

- vypočítání součtu velikosti vyjmenovaných souborů
- zavedení a odebrání načtených souborů
- nalezení readme a licenčního souboru ([prohlížeč objektů][oexplorer] je používá ve stránce detailu tohoto typu zdroje, pokud v seznamu existují)

## Příklady implementací

Příklady implementací tohoto pluginu se v jednotlivých implementacích liší především z hlediska okamžiku zavádění a kontrol zda je plugin již zaveden.

- 🖼️ [pTRParseMd][pTRParseMd] - Konverze Markdown souboru do HTML výstupu
- 🖼️ [pTRParsePrism][pTRParsePrism] - Vyznačení syntaxe v kódovém výpisu
- 🖼️ [pTRParseMermaid][pTRParseMermaid] - Vykreslení Mermaid grafu z textové definice

[Resource]: :_plg:Resource.md "Resource"
[oexplorer]: oexplorer.md "Prohlížeč objektů"
[pTRParseMd]: :_plg:pTRParseMd.md "pTRParseMd"
[pTRParsePrism]: :_plg:pTRParsePrism.md "pTRParsePrism"
[pTRParseMermaid]: :_plg:pTRParseMermaid.md "pTRParseMermaid"
