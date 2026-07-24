# 🧩 pExtension

Pluginy s prefixem **pExtension**\* rozšiřují stávající funkcionalitu systému nebo externích knihoven.

## Jmenná konvence

Například:
🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions]

| Část | Význam | Příklad |
| --- | --- | --- |
| **pExtension** | rozšíření | **pExtension** |
| **Marked** | pro co? | **marked.js** - externí knihovna vykreslující markdown |
|  **Admonitions**| co zajišťuje? | **zvýrazněné bloky** |

(stejná knihovna = jedna společná předpona a část společné logiky v předkovi **pExtensionMarked**)

## Implementace

1. Nový plugin vždy bude mít 🧩 [pExtension ("něco")][pExtension] jako svou bázovou třídu ne **pExtension** přímo.
2. Implementace je velmi různorodá podle prvku, který bude rozšiřovat. Postupujte podle kapitoly 🧩 [první plugin][firstPlugin]
3. Nový plugin musí být zaveden do 📄 [seznamu pluginů][pluginslst] například takto:

```text
pExtensionMarked
pExtensionMarkedAdmonitions:
```

v pořadí, které je v seznamu níže než **pExtension**.

## Možné odpovědnosti

Tyto pluginy mohou mít odpovědnosti, které jsou rozebrány v dalších podkapitolách.

### Předexportní konverze

V případě některých pluginů lze předpokládat, že provádějí transformaci do HTML kódu, kterou obecné **HTMLTo**\* (**HTMLToMD**, **HTMLToTeX**) převodníky nerozpoznají.

Na straně pluginů proto musí být definována obsluha **onET_PreExportCorrection** události ⚡ [PreExportCorrection][PreExportCorrection] s tím, že její **x.temporaryObjects** budou propojeny na **corrections** v místě požadavku na export. **Za způsob výstupu do exportu odpovídá tento plugin.** Typ exportu dostává z dat volání. Měl by také zajistit záložní obsluhu pro nový nebo neznáný formát (**\***).

Ukázka obsluhy:

```javascript
  onET_PreExportCorrection(e) {
    if (!e || !e.parent) return;

    const cssClass = this.cfgROOTCSSCLASS;
    const willBeUpdated = [...$A(`.${cssClass}`, e.parent)];
    const exportFormatting = new Map([
      ['MD', (id) => `> [!${id}]`],
      ['TEX', (id) => `<strong>[!${id}]</strong> `],
      ['*', (id) => ''],
    ]);
    
    willBeUpdated.forEach(x => {
      const typeClass = x.className.split(' ').filter(Boolean).find(c => c.startsWith(cssClass) && c !== cssClass) || '';
      if (typeClass) {
        const correctionText = (exportFormatting.get(e.exportType) || exportFormatting.get('*'))?.(typeClass.toUpperCase().substring(cssClass.length + 1));
        if (correctionText) {
          const correction = document.createElement('span');
          correction.className = e.CSSClassName;
          correction.innerHTML = correctionText;

          x.prepend(correction);
          e.temporaryObjects.push(correction);
          e.manipulatedObjects.push(x);  
        }
      }
    });
  }
```

(🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions])

## Příklady implementací

- 🧩 [pExtensionMarkedAdmonitions][pExtensionMarkedAdmonitions], 🧩 [pExtensionMarked][pExtensionMarked] a další potomci třídy 🧩 [pExtension][pExtension], kteří svým jménem začínají na **pExtension**.

[pExtension]: :_plg:pExtension.md "pExtension"
[pExtensionMarkedAdmonitions]: :_plg:pExtensionMarkedAdmonitions.md "pExtensionMarkedAdmonitions"
[pExtensionMarked]: :_plg:pExtensionMarked.md "pExtensionMarked"
[firstPlugin]: firstPlugin.md "První plugin"
[pluginslst]: plugins.lst.md "Seznam pluginů (plugins.lst)"
[PreExportCorrection]: :_evt:PreExportCorrection.md "PreExportCorrection"
