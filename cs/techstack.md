# 🛠️ Použité technologie

- 📄 HTML 5
- 🎨 CSS 3 (čistý)
- ⚡ JavaScript ES2021 (čistý)
- 🛢️ Local storage
- 🛢️ IndexedDB (pouze pro plugin ✏️ Poznámky)

## 🗃️ Repozitář

- [HelpViewer][HVRepo]

## 🧩 Knihovny třetích stran

| Knihovna | Licence | Status integrace |
| --- | :---: | --- |
| [JSZip library][JSZIP] | MIT | 🔗 pevná |
| [Marked][Marked] | MIT | 🧩 plugin, odebratelné |
| [Mermaid][Mermaid] | MIT | 🧩 plugin, odebratelné |
| [Prism][Prism] | MIT | 🧩 plugin, odebratelné |
| [DOMPurify][DOMPurify] | Apache License Version 2.0 | 🧩 plugin, odebratelné |

## 📦 Distribuce

- 🗜️ [ZIP archiv][DZIP]
  - 📥 [Vlastní balíček][HelpViewer] (ZIP)
- 🐳 [Kontejner pro Docker/Podman][DCONT]

## ⚙️ Sestavení

- 🤖 CI/CD : GitHub Actions

[JSZIP]: http://jszip.org/ "JSZip - práce se ZIP soubory"
[Marked]: https://marked.js.org/ "Marked - vypisování a formátování md souborů do HTML formátu"
[Mermaid]: https://mermaid.js.org/ "Mermaid - vykresluje grafy a schémata podle speciálních textových definic"
[Prism]: https://prismjs.com/ "Prism - zvýraznění syntaxe výpisů kódu"
[HVRepo]: https://github.com/HelpViewer/HelpViewer "HelpViewer"
[DZIP]: https://github.com/HelpViewer/HelpViewer/releases "ZIP"
[DCONT]: https://github.com/HelpViewer/HelpViewer/pkgs/container/helpviewer "Kontejner"
[HelpViewer]: https://helpviewer.github.io/ "HelpViewer"
[DOMPurify]: https://github.com/cure53/DOMPurify "DOMPurify - ochrana výstupu proti XSS (Apache License Version 2.0)"
