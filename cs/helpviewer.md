# 🔎 Projekt HelpViewer

## Organizace

Organizace [HelpViewer][HelpViewer] obsahuje 2 základní typy repozitářů:

- Základní repozitáře projektu - prohlížeč, překlady, další servisní repozitáře
- Repozitáře nápověd (**help\***)

## Seznam základních repozitářů

| Repozitář | Obsah |
|---|---|
| [HelpViewer][RHelpViewer] | Základní repozitář projektu - prohlížeč nápovědy. |
| [Translations][RTranslations] | Jazykové překlady UI prohlížeče nápovědy. Repozitář je vložený do **HelpViewer** jako submodul. Je částečně zdrojem seznamu jazyků, které se uživateli nabízejí pro přepnutí nápovědy. |
| [.github][R.github] | Základní repozitář organizace s provozními informacemi. |
| [helpviewer.github.io][RWebHello] | GitHub Pages projekt webové prezentace. [Nasazovací skript][RWebHelloDeploy] provede aktualizaci stránky s použitím nastavené verze nasazení. |
| [fulltextSearchDBBuilder][FTSIndexBuilder] | Generátor fulltext indexu. Tento Bash skript je používán nasazovacími skripty nápověd při přípravě fulltext indexů. |
| [helpTemplate][RhelpTemplate] | Šablona projektu souboru nápovědy. Je určená pro autory nápověd jako základní prázdný projekt. |
| [prism][RPrism] | PrismJS sestavená pomocí download průvodce projektu. Repozitář je vložený do **HelpViewer** jako submodul. |

## Seznam repozitářů nápověd

Repozitáře bývají pojmenovány **help\***. Vzhledem k pojmenování projektu existují vyjímky, které byly popsány výše.

| Repozitář | Obsah |
|---|---|
| [helpHello][RhelpHello] | Představení projektu pro veřejnou webovou prezentaci. |
| [helpUser][RhelpUser] | Nápověda pro uživatele prohlížeče. Popisuje základní práci s prohlížečem. |
| [helpAuthorsGuide][RhelpAuthorsGuide] | (Tato) Nápověda pro autory nápověd. Popisuje vyškeré kroky, které jsou potřebné k vytvoření a vydání nápovědy. |

## Vydávání verzí

- Verze se vydávají nepravidelně
- Číslem verze je vždy datum daného vydání ve formátu rokměsícden (například: 20250621)
- Pokud se v daný den vydá více verzí, pak první má formát rokměsícden a každá další má příponu **-číslo** od 1 s krokem 1, tedy například: 20250606-1, 20250606-2
- Data pro popis změn verzí se získávají z **CHANGELOG.md** v kořeni repozitáře. Popis pro nejnovější verzi se připojuje vždy na začátek souboru. Nejstarší verze bývají ve výpisu nejníže. Poslední sekci s "**File introduced**" neměňte a neodebírejte - slouží i pro Vaši informaci
- Tento postup platí jak pro **HelpViewer**, tak i další nástroje a vydávané nápovědy
- Postup je doporučován i pro autory nápověd, přestože mají možnost si tento bod rozhodnout po svém

[HelpViewer]: https://github.com/HelpViewer "HelpViewer"
[RHelpViewer]: https://github.com/HelpViewer/HelpViewer "HelpViewer"
[RTranslations]: https://github.com/HelpViewer/Translations "Překlady"
[RWebHello]: https://github.com/HelpViewer/helpviewer.github.io "Webová prezentace projektu"
[RWebHelloDeploy]: https://github.com/HelpViewer/helpviewer.github.io/actions/workflows/toPages.yml "Webová prezentace projektu - nasazení"
[FTSIndexBuilder]: https://github.com/HelpViewer/fulltextSearchDBBuilder "Generátor fulltext indexu"
[RhelpTemplate]: https://github.com/HelpViewer/helpTemplate "Šablona projektu souboru nápovědy"
[RhelpHello]: https://github.com/HelpViewer/helpHello
[RhelpUser]: https://github.com/HelpViewer/helpUser
[RhelpAuthorsGuide]: https://github.com/HelpViewer/helpAuthorsGuide
[R.github]: https://github.com/HelpViewer/.github "Repozitář se základními informacemi"
[RPrism]: https://github.com/HelpViewer/prism
