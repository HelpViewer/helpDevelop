# 🐞 Debug režim

- Debug režim je v produkci automaticky vypnutý
- Zapnete jej změnou **DEBUG_MODE** na **true** v **index.html**

## Funkce dostupné v debug režimu

- 🧩 [Prohlížeč objektů][oexplorer]
- 📜 Logování do DevTools konzole prohlížeče
- ⚡ zaslané události jsou také zdvojeny do události [DebugEventEvent][DebugEventEvent], která je zpracována prohlížečem objektů s cílem zachytit přenosy událostí mezi celky aplikace při běhu

[DebugEventEvent]: :_evt:DebugEventEvent.md "DebugEventEvent"
[oexplorer]: oexplorer.md "Prohlížeč objektů"
