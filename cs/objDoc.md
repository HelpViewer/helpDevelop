# 📑 Dokumentace objektů

Pro zachování přehlednosti aplikace i pluginů je doporučeno, aby byly nové objekty vždy, pokud je to možné, zdokumentovány.

V HelpVieweru je dokumentace organizována jako strom objektů a automatické seznamy s možností prokliku na detailní stránku. Vše řídí 🧩 [prohlížeč objektů][oexplorer], který zobrazuje obsah podle aktuálního stavu systému. Na jednotlivých stránkách pak může doplňovat informace z ručně připravené dokumentace (pokud existuje), a tím rozšiřovat automaticky generované kapitoly.

Tuto ruční dokumentaci lze rozšiřovat v repozitáři [helpInternalRef][RhelpInternalRef] (adresář zip/i v projektu HelpViewer). Tento repozitář se stává součástí vydaného balíčku a má strukturu odpovídající standardnímu souboru nápovědy. Formát i postup přípravy jsou popsány v [dokumentaci pro autory][AuthDoc].

V rámci této zvláštní nápovědy přidáváte pouze soubory .md. Strom ani indexy není třeba řešit, protože je dynamicky vytváří 🧩 [prohlížeč objektů][oexplorer] podle stavu systému.

## Jmenná konvence popisných dokumentů

Obecná struktura umístění:  
**i/(jazyk, zkratka dle ISO 639-1)/(zkratka typu objektu)_(jméno třídy pluginu)\_(jméno instance pluginu)\_(jméno objektu).md**

V případě prblémů s nezobrazováním textu můžete přesné předpokládané umístění také získat ze zpráv z **dev konzole prohlížeče** (úroveň Warning, zpráva začíná textem: 'ObjectExplorer: requested path:').

V ukázkách podadresář **en** zastupuje jazyk.

| Typ objektu | Ukázka plné cesty a popis |
|---|---|
| Skupina pluginů | **i/en/grp_UI.md** (UI může být nahrazeno kteroukoli jinou skupinou ze [seznamu skupin][oexplorerGrp] v prohlížeči objektů) |
| 🧩 Třída pluginu | **i/en/plg_pColorTheme.md** (pColorTheme je název třídy pluginu) |
| 🔹 Instance pluginu | **i/en/oeod_inst_puiButtonKeywordIndex_keywordList.md** (puiButtonKeywordIndex je název třídy pluginu, keywordList je název instance nebo není uveden pokud aliasName (id) je prázdné) |
| ⚡ Událost | **i/en/event_PluginsDump.md** (PluginsDump je název události) |
| ⚡ pole události | **i/en/p_PluginsDump_createdAt.md** (PluginsDump je název události, createdAt je název pole)  |
| ⚡ pole události (záložní popis napříč dokumentací) | **i/en/p__createdAt.md** (createdAt je název pole, v cestě jsou dvě podtržítka, tato ponechte) |
| ⚙️ Konfigurační volba | **i/en/cfgopt_puiButtonKeywordIndex_keywordList_CAPTION.md** (puiButtonKeywordIndex je název třídy pluginu, keywordList název instance pluginu, CAPTION je název konfiguračního klíče na straně kódu) |
| 🛰️ [Odesílání události][eventTra] | **i/en/transmitter_puiSidebar_sidebar_ClickHandlerRegister.md** (puiSidebar je název třídy pluginu, sidebar název instance pluginu, ClickHandlerRegister je název odesílané události) |
| 📦 Zdroj/Balíček | **i/en/res_pTRParseMd_-md_MARKED.md** (pTRParseMd je název třídy pluginu, -md je název instance, MARKED je název zdroje) [Zdroj][resource] může mít další popisné informace. |
| 👂 Obsluha události | **i/en/hdl_puiButtonKeywordIndex_keywordList_onETIndexFileLoaded.md** (puiButtonKeywordIndex je název třídy pluginu, keywordList název instance pluginu, onETIndexFileLoaded je úplný název obslužné funkce události na straně kódu) |
| 🔘 UI prvek | **i/en/uiobject_puiButtonKeywordIndex_keywordList_downP-Glossary.md** (puiButtonKeywordIndex je název třídy pluginu, keywordList název instance pluginu, downP-Glossary je id html elementu id prvku) |
| ⭐ Javascript událost | **i/en/sysevent_pConvertSysEventToEvent_pPrePrintEvent_window.beforeprint.md** (pConvertSysEventToEvent je název třídy pluginu, pPrePrintEvent název instance pluginu, window je název html prvku ke kterému byla obsluha připojena, beforeprint je název javascript události) |
| ⇄ Integrovaný proces | **i/en/grpproc_fulltextList.md** (toc je název integrovaného procesu - název instance pluginu) |
| 📄 Výpis zdrojového kódu | **i/en/cpp_pIndexFile.md** (pIndexFile je název třídy pluginu) |
| 🏷️ Funkce třídy | **i/en/method_pIndexFile_keywordList_init.md** (pIndexFile je název třídy pluginu, keywordList název instance pluginu, init je název funkce) |
| 🌐 global | **i/en/g_global.md** |
| 🌐 global -> 🏷️ funkce | **i/en/method_loadPluginList.md** (loadPluginList je název funkce) |

## Konvence odkazu na dokumentaci z vnější nápovědy

⚠️ Aby odkazy fungovaly a kapitola se zobrazila, musí být [prohlížeč objektů][oexplorer] otevřen před přístupem k datům v rámci relace. Indexace totiž probíhá vždy s otevřením záložky stromu tohoto pluginu.

Obecná struktura cesty odkazu:  
**:(typ objektu):(jméno třídy pluginu):(jméno instance pluginu):(jméno objektu).md**

| Typ objektu | Ukázka cesty odkazu |
|---|---|
| Skupina pluginů | **:_grp:UI.md** |
| 🧩 Třída pluginu | **:_plg:pTopicRenderer.md** |
| 🔹 Instance pluginu | **:_inst:pIndexFile:fulltextList.md** |
| ⚡ Událost včetně obsluhy | **:_evt:DebugEventEvent.md** |
| 📄⚡ Událost bez obsluhy | **:_evtD:DebugEventEvent.md** |
| ⚙️ Konfigurační volba | **:_cfg:pIndexFile:keywordList:FILENAMEKW.md** |
| 📄⚙️ Konfigurační volba ([dynamická][cfgDyn]) | **:_cfgE:puiButtonObjectExplorer:-load:RENDER-F.md** |
| 🛰️ [Odesílání události][eventTra] | **:_tra:puiSidebar:sidebar:ClickHandlerRegister.md** |
| 📦 Zdroj/Balíček | **:_res:pTRParseMermaid:-connected:MERMAID.md** |
| 👂 Obsluha události | **:_hdl:puiHeader:header:onETButtonSend.md** |
| 🔘 Tlačítko | **:_btn:puiButtonVersionSearch::downP-ChangeVersion.md** |
| 🎛️ Karta | **:_page:puiButtonObjectExplorer:-load:oexpP.md** |
| 📂 Strom | **:_tree:puiButtonObjectExplorer:-load:objectList.md** |
| ⭐ Javascript událost | **:_evtSys:pConvertSysEventToEvent:pPrePrintEvent:window.beforeprint.md** |
| ⇄ Integrovaný proces | **:_grpproc:fulltextList.md** |
| 📄 Výpis zdrojového kódu | **:_cpp:pui.md** |
| 🏷️ Funkce třídy | **:_fn:pIndexFile:keywordList:init.md** |
| 🌐 global | **:_g:global.md** |
| 🌐 global -> 🏷️ funkce | **:_fn:loadPluginList.md** |

Dokumentace pro autory popisuje jak [přidat odkaz do textu kapitoly][AuthDocLinks].

### Získání cesty odkazu na objekt z prohlížeče objektů

1. Otevřete 🧩 [prohlížeč objektů][oexplorer].
2. Najděte požadovaný objekt:
   - ve **stromu objektů** 
   - nebo zadáním do **řádku vyhledávání** a stisknutím **Enter**
3. Otevřete dev tools prohlížeče.
4. Aktivujte **Select element** a klikněte na odpovídající **a** objekt.
5. V atributu **data-param** najdete celou cestu k objektu.

[RhelpInternalRef]: https://github.com/HelpViewer/helpInternalRef "HelpViewer dokumentace systémových objektů"
[AuthDoc]: ?d=hlp-aguide/Help-__.zip "Dokumentace pro autory"
[oexplorer]: oexplorer.md "Prohlížeč objektů"
[oexplorerGrp]: :_cfg:puiButtonObjectExplorer:-load:GROUPSLIST.md "Seznam skupin v prohlížeči objektů"
[resource]: resource.md#h-2-3 "Zdroj - další informace"
[cfgDyn]: cfgopt.md#h-2-1 "Dynamické konfigurační klíče"
[eventTra]: event.md#h-2-2 "Odesílání události"
[AuthDocLinks]: ?d=hlp-aguide/Help-__.zip&d=hlp-aguide/Help-__.zip&p=links.md#h-3-0 "Odkazy v textu kapitol"
