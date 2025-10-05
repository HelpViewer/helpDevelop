# 📥 Vlastní balíček

V **helpHello** nápovědě je k dispozici funkce **📥 Vlastní balíček**.

Funkcionalitu zajišťuje plugin 🖥️ [puiButtonCustPackage][puiButtonCustPackage].

Podrobnosti o konfiguraci pluginu naleznete v následujících kapitolách.

## Přehled

Konfigurace je rozdělena mezi následující umístění:

| Soubor | Význam |
| --- | --- |
| plugins-config/puiButtonCustPackage__tree.cfg | Strom závislostí |
| plugins-config/puiButtonCustPackage_.cfg | Data o komponentách |
| puiButtonCustPackage/*/lstr.txt | 🌐 [Překlady][ViewerNewLang] interních jmen komponent pro uživatele. Hvězdička zastupuje zkratku jazyka. |

Pouze přidáním potřebných informací do všech těchto míst vytvoříte plnohodnotnou novou komponentu.

## Strom závislostí

- Soubor **plugins-config/puiButtonCustPackage__tree.cfg** obsahuje [hierarchický strom][treedata] pouze s interními názvy komponent.
- Každá mezera zleva označuje jednu úroveň vnoření - komponenta je tedy podřízena té, která je nad ní a má o jednu mezeru méně.

## Překlady

- Soubor **puiButtonCustPackage/(zkratka-jazyka)/lstr.txt** obsahuje překladový klíč, který má název podle jména komponenty ze [stromu závislostí][treedep].
- Hodnotou klíče je překlad, který se zobrazuje uživateli.
- Vše je dále popsáno v kapitole 🌐 [Nový jazyk][ViewerNewLang].

## Data o komponentách

Soubor **plugins-config/puiButtonCustPackage_.cfg** obsahuje standardní formát [konfigurace][cfgPlug] pro plugin.

### Pravidla formátu

- ⚠️ Tento formát je velmi přísný, prosím, dodržujte pravidla přesně.
- Seznamy v tomto souboru nekončí středníky.
- Jednotlivé položky seznamů v klíčích jsou odděleny středníky.
- Celé adresáře končí lomítkem **/**.
- Soubory i adresáře jsou uváděny v relativních cestách ke kořeni balíčku (**hvdata/data.zip**). Nezačínají žádným prefixem.  
  Například **styles/** je odkaz na složku **styles** uvnitř tohoto zip souboru.

### Základní data

Každá komponenta zde definuje základní 3 klíče:

- **I**-JMENO - Ikona komponenty
- **P**-JMENO - Seznam pluginů (plugin) a instancí pluginu (plugin:id)
- **F**-JMENO  
  Seznam souborů a adresářů v datech celého balíčku, které ke komponentě patří. Soubory jsou uváděny v relativních cestách. Celé adresáře končí lomítkem **/**. Běžný adresář s daty pro plugin (./jmeno-tridy-pluginu hledá puiButtonCustPackage automaticky).

JMENO = jméno komponenty ze [stromu závislostí][treedep]

### Další data

- **C**-JMENO  
  Komponenta JMENO může záviset na dalších komponentách uvedených v seznamu. Tyto závislé komponenty se automaticky připojí k výběru, pokud si uživatel zvolí komponentu JMENO jako součást balíčku. Cílem tohoto zápisu je poskytnout vedle [stromu závislostí][treedep] i paralelní textovou definici, která lépe vystihuje případy, kdy komponenta závisí na více dalších komponentách současně. Tento klíč je nepovinný a nemusí být uveden.
- **DE**  
  Seznam pluginů, které jsou vždy odebrány z výsledného balíčku, který připraví tato funkcionalita pro uživatele.  
  Například po provedení této funkcionality uživatel vždy získá balíček, který již nepodporuje další vytvoření vlastního balíčku.
- **DE-(jmeno-tridy-pluginu)**  
  Seznam pluginů, které jsou odebrány, pokud je plugin **(jmeno-tridy-pluginu)** zcela odebrán z balíčku.  
  Například **pIndexFile** a jeho podpora pro **práci s klíčovými slovy a přehledové stránky slovníku**.

[puiButtonCustPackage]: :_plg:puiButtonCustPackage.md "puiButtonCustPackage"
[ViewerNewLang]: newLangViewer.md#h-3-1 "Nový jazyk prohlížeče"
[treedata]: ?d=hlp-aguide/Help-__.zip&p=mdata%2Ftree.lst.md "Formát dat stromových struktur"
[cfgPlug]: pluginConfig.md "Konfigurace pluginů"
[treedep]: #h-2-1 "Strom závislostí"
