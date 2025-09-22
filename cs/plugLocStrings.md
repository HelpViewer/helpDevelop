# 🌐 Lokalizace pluginů

## Použití lokalizačního řetězce

Kdekoli v kódu pluginu toto provolání:

```javascript
_T('LokalizacniKlic');
_T('LokalizacniKlic', { dynamickaHodnota: 'pokus'});
```

**\_T** vypíše hodnotu lokalizačního klíče **LokalizacniKlic**. Pokud hodnota chybí, vypíše se jméno klíče s podtržítky \_LokalizacniKlic\_ (v markdown výstupu se zobrazí kurzivou bez podtržítek - _LokalizacniKlic_).

Druhý parametr (objekt) slouží pro předání dynamických hodnot, které se do řetězce mohou dosadit.

Kapitola 🌐 [Nový jazyk prohlížeče][ViewerNewLang] dále popisuje:

- strukturu a význam souborů hlavní lokalizace,
- jejich umístění,
- formát lokalizačních klíčů, který je automaticky mapován na HTML objekty podle shody id a jména vlastnosti se jménem klíče

## Samostatný lokalizační slovník pro plugin

Pomocí komponenty 🧩 [pServiceLocalization][pServiceLocalization] (součást základního balíčku) lze přidat vlastní lokalizace pro každý plugin. Stačí založit příslušné soubory na správném místě.

Povinné soubory:

- **lstr.txt** – pevně dané texty
- **lstr.js** – dynamické řetězce (obsahují proměnné, skládají texty za běhu)

Struktura

- Soubory se ukládají podle jazykových kódů (cs, en, ...).
- Strom adresářů pro jednotlivé jazyky je ukázán v kapitolách dále.
- 🛈 Stromy adresářů dat prohlížeče a dat nápovědy se liší, protože vycházejí z odlišného vnitřního procesu načítání.

Další informace

- Detailní popis struktury a formátu lokalizačních souborů najdete v kapitole 🌐 [Nový jazyk prohlížeče][ViewerNewLang].

Popis činnosti

- Při zavedení instance pluginu se načte jeho lokalizační slovník z příslušných souborů a připojí se k již načtené lokalizaci.
- Při změně jazyka se nejprve načte hlavní lokalizační slovník a poté se postupně načítají slovníky podle [pořadí zavedení][OELoadOrder] jednotlivých instancí pluginů.
- Při kolizi jmen klíčů je rozhodující poslední načtená hodnota, protože přepíše všechny předchozí.

### V datech prohlížeče

```treeview
HelpViewer/
    zip/
        jméno-třídy-pluginu/
            cs/
                lstr.js
                lstr.txt
            en/
                lstr.js
                lstr.txt
```

### V datech nápovědy

```treeview
helpProject/
    cs/
        jméno-třídy-pluginu/
            lstr.js
            lstr.txt
    en/
        jméno-třídy-pluginu/
            lstr.js
            lstr.txt
```

[ViewerNewLang]: newLangViewer.md#h-3-1 "Nový jazyk prohlížeče"
[pServiceLocalization]: :_plg:pServiceLocalization.md "pServiceLocalization"
[OELoadOrder]: :_/LORDER.md "Pořadí zavádění"
