# 🗺️ Basic overview

The application is built on **plugins (plug-in modules) and the transfer of events (messages) between them**.

The following can be defined in plugins:

- events (messages),
- their handlers,
- sending events,
- UI elements,
- JavaScript event handlers,
- membership in a communication path (group of recipients)

This ensures that the approaches to the UI and program logic are consistent across the entire application.  
The plugin system and message distribution have been developed from scratch, without the use of third-party frameworks.  

**Technical solution:**

- compressed application data package (with the option to run with unzipped content),
- runs on the client, no server or backend required,
- minimum requirements for deployment: browser with **ES2021** support + local disk (no Internet required) (CORS is recommended to be disabled, although the application includes support for manual data upload by the user)

**Main components of the application:**

- loader (**hvdata/appmain.js + jszip.min.js**),
- application data (**hvdata/data.zip**; **STO_DATA**), where most of the application is stored (about 86% of the package size)
  - low-level code (in **js.lst**),
  - plugin code (in **plugins.lst**).
- third-party libraries (separate, loaded as separate modules)
- implementation data file - a separate archive in the application logically named **STO_HELP**

**⚖️ License**: [MIT][MIT]

[MIT]: https://github.com/HelpViewer/HelpViewer/blob/master/LICENSE "MIT license"
