# 🧩 Prohlížeč objektů

HelpViewer obsahuje plugin **puiButtonObjectExplorer**. Tento plugin slouží k procházení aktuálního stavu systému a katalogu vazeb a definovaných objektů.

## Aktivace

⚠️ ObjectExplorer zásuvný modul je načten pouze pokud aplikace běží s **DEBUG_MODE = true** v **hvdata/appmain.js**. V opačném případě není k dispozici žádná funkcionalita ani výstup a aplikace vrací odpověď nenalezeno pro kapitoly, které modul obsluhuje.

⚠️ Pokud plugin nebyl doposud v rámci relace aktivní, část funkcionality ze seznamu funkcí při použití odkazů nebude ještě k dispozici.

## Funkce

Plugin zobrazuje například:

- Přehled [skupin a podporovaných objektů][OEGroups]
- [Strom dědičností][OETree] pluginů a událostí (eventů)
- [Pořadí][OELoadOrder] načtení [instancí pluginů][PlgsList]
- Pluginy v kategoriích (je řízeno konfigurací pluginu)
- Pluginy ve skupinách podle společného id (pluginy tak společně tvoří integrovaný celek - slovník klíčových slov, postup vykreslení textu kapitoly, ...)
- Seznam prvků a objektů, které poskytuje konkrétní instance pluginu
- Seznam konfiguračních voleb instance pluginu
- Dokumentaci prvků, pokud je dostupná (zatím především v angličtině)
- Informace o definovaných filtrech a vazbách v řetězci předání události: odesilatel -> obsluha.

Dále podporuje:

- Vyhledání objektu podle jeho klíčového jména s přesností na podřízenou definici pluginu (vyhledávání podle jména javascript funkce zatím není možné)
- Vyhledání objektu podle jeho typu je možné zkopírováním symbolu typu (ikonky) do vyhledávacího řádku
- Zobrazení formátovaného výpisu zdrojového kódu pluginu

## Zdroje dat

- vývojářské ruční definice vazeb
- statická analýza (skenování kódu, který je načtený, ale neběží)
- dynamická analýza (automatizované skenování běhu a zaslaných událostí během provozu)

## Omezení

1. Plugin je dostupný pouze v **DEBUG** režimu z důvodu ochrany produkčních prostředí.
2. ⚠️ Pro úplný seznam objektů je nutné, aby byla daná funkcionalita v rámci relace alespoň jednou provedena.

[PlgsList]: plugins.lst.md "Seznam pluginů"
[OEGroups]: :_/README.md "Seznam kategorií"
[OETree]: :_/tree/TREE.md "Strom dědičností"
[OELoadOrder]: :_/LORDER.md "Pořadí zavádění"
