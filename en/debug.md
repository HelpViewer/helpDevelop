# 🐞 Debug mode

- Debug mode is automatically disabled in production.
- Enable it by changing **DEBUG_MODE** to **true** in **hvdata/appmain.js**.

## Features available in debug mode

- 🧩 [Object explorer][oexplorer]
- 📜 Logging to the browser's DevTools console
- ⚡ Sent events are also duplicated into the [DebugEventEvent][DebugEventEvent] event, which is processed by the object explorer in order to capture event transfers between application entities during runtime

[DebugEventEvent]: :_evt:DebugEventEvent.md "DebugEventEvent"
[oexplorer]: oexplorer.md "Object Explorer"
