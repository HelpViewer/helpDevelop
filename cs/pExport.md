# 🖼️ pExport

## Účel pluginu

Tento plugin definuje základní rozhraní pro export zobrazeného textu kapitoly.

Odvozený plugin je obvykle zapouzdřením mezi:

- **HelpViewer** (🖥️ [puiButtonExport][puiButtonExport]) a
- převodníkem z **HTML** na požadovaný formát, který je obvykle řešen externím skriptem. 

Načtení převodníku v případě potřeby zajistí plugin 📦 [Zdroj][resource].

## Implementace

1. Nový plugin vždy bude mít 🖼️ [pExport][pExport] jako svou bázovou třídu.
2. Implementace bude vypadat přibližně takto:

```javascript
class pExportNEW extends pExport {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.RES_HTMLTONEW = new Resource('HTMLTONEW', undefined, STO_DATA, 'HTMLToNEW/HTMLToNEW.js;HTMLToNEW/LICENSE;HTMLToNEW/README.md');
  }
  
  async onETPrepareExport(evt) {
    let promise = Promise.resolve(true);

    if (typeof HTMLTONEW !== 'function')
      promise = this.RES_HTMLTONEW?.init(promise);

    promise = promise.then(async() => {
      const ctx = { listStack: [], i_img: 0, i_svg: 0, embeds: evt.embeds };
      const converted = HTMLTONEW(evt.parent, ctx);
      evt.output.file('output.txt', converted);
  
      if (evt.doneHandler)
        evt.doneHandler();

    });
  }
}

Plugins.catalogize(pExportNEW);
```

3. Nový plugin musí být zaveden do 📄 [seznamu pluginů][pluginslst] :

```text
pExportNEW:NEW
```

v pořadí, které je v seznamu níže než **pExport**.

ID za dvojtečkou (zde NEW) se nabídne ve výběrovém seznamu tlačítka 📥 Export.

## Popis funkčnosti

- Uživatel klikne na tlačítko 📥 Export
- Obsluha tlačítka založí ZIP archiv a shromáždí do něj obrázky a další vnořené prvky, které v textu najde a pošle data jako odkaz na plochu pro text kapitoly nebo handler **doneHandler**, který zajistí vystavení ZIP souboru pro uživatele
- Obsluha tlačítka odešle událost ⚡ [PrepareExport][PrepareExport]
- Odvozený plugin (**pExportNEW**) definuje obsluhu 👂 **onETPrepareExport**, která převezme připravený mezivýsledek
- Obsluha exportu (může být asynchronní) pracuje především s:
  - **evt.embeds** - vnořené prvky, obrázky, SVG
  - **evt.parent** - nadřízený HTML objekt (zobrazovací plocha pro text kapitoly)
- Obsluha exportu provolá funkci převodníku, které předá potřebný objekt kontextu s prázdnými nebo výchozími hodnotami, odkaz na HTML objekt, který obsahuje úplný vstup, případně další vstup podle implementace
- Obsluha exportu převezme výsledek převodu a provolá **evt.output.file('name.txt', result);**, pro zápis do ZIP výstupu
- Obsluha exportu nakonec provolá **evt.doneHandler();**. Tímto vydá ZIP soubor uživateli do prohlížeče pro standardní stažení

## Předexportní konverze

V případě některých pluginů (konvence pro pojmenování v systému **pExtension**\* - například: 🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions]) lze předpokládat, že provádějí transformaci do HTML kódu, kterou obecné **HTMLTo**\* (**HTMLToMD**, **HTMLToTeX**) převodníky nerozpoznají.

### Postup

1. V odvozené třídě **pExport**\* v **onETPrepareExport** bude definována proměnná **corrections** (pole), která bude evidovat budoucí změny v DOM struktuře textu kapitoly.
2. Spustíte událost ⚡ [PreExportCorrection][PreExportCorrection] s tím, že **x.temporaryObjects** budou propojeny na **corrections**
3. Proběhnou provolání **onET_PreExportCorrection** na pluginech a konverze výstupů z **pExtension**\* pluginů podle typu exportního formátu, který se připravuje - extension plugin znovu transformuje svou konverzi do zjednodušeného výstupu pro **HTMLTo**\* převodník.
4. V **corrections** budou obsaženy prvky, které konverzí vznikly
5. Provolá se samotná konverze z HTML na požadovaný formát
6. **corrections** projdete v cyklu a smažete všechny obsažené prvky - dočasné úpravy se vyčistí z viditelného vstupu.

### Ukázková implementace

```javascript
  //...
  async onETPrepareExport(evt) {
    //...
    promise = promise.then(async() => {
      //...
      const corrections = [];
      sendEvent(EventNames.PreExportCorrection, (x) => {
        x.exportType = this.aliasName;
        x.parent = evt.parent;
        x.temporaryObjects = corrections;
      });

      const converted = HTMLTONEW(evt.parent, ctx);
      corrections.forEach(x => x.remove());
      //...
    }
  }
```

Událost ⚡ [PreExportCorrection][PreExportCorrection] má obsluhu na straně 🧩 [pExtension][pExtension]\*, která zajistí bod 3 [Postupu][H30].

## Příklady implementací

- 🖼️ [pExportHTM][pExportHTM] a další potomci třídy 🖼️ [pExport][pExport], kteří svým jménem začínají na **pExport**.
- Převodníky: [HTMLToTeX][HTMLToTeX], [HTMLToMD][HTMLToMD]

[puiButtonExport]: :_plg:puiButtonExport.md "puiButtonExport"
[pExportHTM]: :_plg:pExportHTM.md "pExportHTM"
[pExtension]: pExtension.md#h-3-0 "pExtension"
[pExtensionMarkedAdmonitions]: :_plg:pExtensionMarkedAdmonitions.md "pExtensionMarkedAdmonitions"
[PrepareExport]: :_evt:PrepareExport.md "PrepareExport"
[PreExportCorrection]: :_evt:PreExportCorrection.md "PreExportCorrection"
[pExport]: :_plg:pExport.md "pExport"
[resource]: resource.md "Zdroj"
[pluginslst]: plugins.lst.md "Seznam pluginů (plugins.lst)"
[HTMLToTeX]: https://github.com/HelpViewer/HTMLToTeX "HTML -> TeX"
[HTMLToMD]: https://github.com/HelpViewer/HTMLToMD "HTML -> md"
[H30]: #h-3-0 "Postup"
