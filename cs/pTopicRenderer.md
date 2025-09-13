# 🖼️ pTopicRenderer

## Účel pluginu

Tento plugin je vhodný pro správu jednoduchých, lineárních procesů organizovaných do fází.

## Implementace

Plugin je rozšiřitelný jako ostatní objekty, ale doporučuje se pouze definice konfigurace.

🖼️ [pTopicRenderer][pTopicRenderer]

## Konfigurace

| Název | Výchozí hodnota | Popis |
|---|---|---|
| IDCONTENT | content | Id HTML elementu, který bude obvykle příjemcem výstupu procesu pluginu. |
| PHASELIST | triage;load;%%;... | Seznam a pořadí fází, které mají v rámci procesu proběhnout. |

## Popis funkčnosti

Pokud aplikace běží v [debug režimu][debug], plugin průběh své činnosti i jednotlivé mezikroky fází loguje.

1. Plugin přijme událost ⚡ [ShowChapter][ShowChapter]
2. Plugin připraví objekt události ⚡ [ShowChapterResolutions][ShowChapterResolutions] tak, že poskytne:
   - odkaz na čtení úložiště dat aplikace
   - odkaz na čtení úložiště dat nápovědy
   - odkaz na čtení úložiště síťového umístění originálního GitHub repozitáře, pokud jej data nápovědy obsahují
   - cestu k souboru nápovědy
   - odkaz na HTML element do kterého proběhne závěrečný zápis formátovaného výstupu kapitoly
   - určí datové médium (místní soubor, adresář, zip soubor, síťové umístění)
   - určí typ souboru kapitoly
3. Převezme hodnotu **PHASELIST**, kde:
   - %% je vždy nahrazeno prvními třemi znaky přípony vstupního souboru kapitoly bez tečky (md, htm).
   - rozdělí jména podle středníků
4. Objekt **ShowChapterResolutions** odešle do event systému postupně vždy skupinám pluginů podle jména: **(alias)-(fáze)**. Alias je zde **id** instance pluginu. Pluginy tento objekt v rámci jednotlivé fáze dostávají ke svému zpracování vždy v pořadí v jakém jsou zapsány v [seznamu pluginů][plugList].  
Je doporučeno, aby každá fáze měla definovaný aspoň jeden plugin. Pokud v daném procesu fáze vhodná není, ale nechcete ji odebírat, definujte instanci pluginu 🖼️ [pTREmptyPlugin][pTREmptyPlugin].
5. Po dokončení zpracování všech kroků (odpovídají za ně potomci 🖼️ [pTRPhasePlugin][pTRPhasePlugin]) odešle událost ⚡ [ChapterShown][ChapterShown], kterou obvykle přijímá plugin 🧩 [pAppmainNext][pAppmainNext], který je hlavním pluginem aplikace a má na tuto událost obsluhu.

## Příklady implementací

- Vypisování obsahu kapitoly uživateli
- Příprava fulltext slovníku v případě, že není v nápovědě k dispozici předgenerovaný slovník ze CI/CD skriptu

[pTopicRenderer]: :_plg:pTopicRenderer.md "pTopicRenderer"
[pAppmainNext]: :_plg:pAppmainNext.md "pAppmainNext"
[ShowChapter]: :_evt:ShowChapter.md "ShowChapter"
[ChapterShown]: :_evt:ChapterShown.md "ChapterShown"
[ShowChapterResolutions]: :_evt:ShowChapterResolutions.md "ShowChapterResolutions"
[pTRPhasePlugin]: pTRPhasePlugin.md "pTRPhasePlugin"
[plugList]: plugins.lst.md "Seznam pluginů"
[pTREmptyPlugin]: :_cpp:pTREmptyPlugin.md "Prázdný plugin"
[debug]: debug.md "Debug režim"
