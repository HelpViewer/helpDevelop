# 🧩 Prohlížeč objektů

HelpViewer obsahuje plugin **puiButtonObjectExplorer**. Tento plugin slouží k procházení aktuálního stavu systému a katalogu vazeb a definovaných objektů.

## Aktivace

⚠️ ObjectExplorer zásuvný modul je načten pouze pokud aplikace běží s **DEBUG_MODE = true** v **hvdata/appmain.js**. V opačném případě není k dispozici žádná funkcionalita ani výstup a aplikace vrací odpověď nenalezeno pro kapitoly, které modul obsluhuje.

⚠️ Pokud plugin nebyl doposud v rámci relace aktivní, část funkcionality ze seznamu funkcí při použití odkazů nebude ještě k dispozici.

Pokud je plugin aktivní, zobrazí se Vám na bočním panelu toto tlačítko:

<button class="pnl-btn" id="downP-ObjectExplorer" title="Prohlížeč objektů" aria-label="Prohlížeč objektů">🧩</button>

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

- Vyhledání objektu podle jeho klíčového jména s přesností na podřízenou definici pluginu
- Vyhledání objektu podle jeho typu je možné zkopírováním symbolu typu (ikonky) do vyhledávacího řádku
- Zobrazení formátovaného výpisu zdrojového kódu pluginu

## Zdroje dat

- vývojářské ruční definice vazeb
- statická analýza (skenování kódu, který je načtený, ale neběží)
- dynamická analýza (automatizované skenování běhu a zaslaných událostí během provozu - ⚡ [DebugEventEvent][DebugEventEvent])

## Omezení

1. Plugin je dostupný pouze v **DEBUG** režimu z důvodu ochrany produkčních prostředí.
2. ⚠️ Pro úplný seznam objektů je nutné, aby byla daná funkcionalita v rámci relace alespoň jednou provedena.
3. Indexovány jsou pouze pojmenované funkce a objekty, které plugin vystavuje přes **this**.

### Ruční indexace volání události

I přes maximální snahu automatizovat indexaci zasílání událostí mezi pluginy může docházet k situacím, kdy všechna volání události nejsou spolehlivě zachycena. 

V takovýchto případech můžete na úrovni pluginu zavést informaci o volání události ručně tímto způsobem:

```javascript
  init() {
    super.init();

    const TI = this;
    TI.catalogizeEventCall(TI._pluginActivated, EventNames.LocAppend);
  }
```

(výpis zkrácen na init funkci)

- EventNames.LocAppend - je jméno zasílané události (LocAppend). Alternativně je možno zapsat i "LocAppend".
- TI._pluginActivated je metoda uvnitř pluginu, která zaslání události provádí (sendEvent)

[PlgsList]: plugins.lst.md "Seznam pluginů"
[OEGroups]: :_/README.md "Seznam kategorií"
[OETree]: :_/tree/TREE.md "Strom dědičností"
[OELoadOrder]: :_/LORDER.md "Pořadí zavádění"
[DebugEventEvent]: :_evt:DebugEventEvent.md "DebugEventEvent"
