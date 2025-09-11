# 🌐 Nový jazyk prohlížeče

- Pro nový jazyk prohlížeče je potřeba v [repozitáři lokalizací][Localiz] na hlavní úrovni založit nový adresář se zkratkou jazyka.
- Zvolte zkratku podle standardu **ISO 639-1**.
- Váš jazykový překlad pro **HelpViewer** bude po schválení PR automaticky distribuován s nejbližším vydáním.

## Význam souborů v lokalizaci

- Všechny soubory vytvořte ve znakové sadě **UTF-8 no BOM (65001)**.

| Soubor | Popis |
|---|---|
| lname.txt | Název jazyka v daném jazyce. |
| lstr.js | Klíče obsahující dynamické informace. |
| lstr.txt | Klíče se statickými texty. |

## Struktura souborů

### lstr.js

```javascript
var _lstr = {
  'klic' : () => `hodnota ${globalni-promenna}`,
}; 
```

### lstr.txt

```
klic(id html prvku)|hodnota
klic(id html prvku)__placeholder|popisek vstupního pole
klic(id html prvku)__aria-label|popisek pro přístupnost
klic(id html prvku)__*|hodnota atributu HTML elementu
```

[Localiz]: https://github.com/HelpViewer/Translations "Lokalizace HelpViewer"
