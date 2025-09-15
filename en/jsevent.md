# ⭐ JavaScript event processing

JavaScript event processing is used to connect the plugin to a system JavaScript event.

## Definition

### pConvertSysEventToEvent and configuration

If possible, prioritize the plugin instance 🔌 [pConvertSysEventToEvent][pConvertSysEventToEvent], which you can modify through configuration. The result of this procedure is a translated system event that can be captured by any plugin via 👂 [event handler][handler].

### Definition inside your own plugin

```javascript
class pSysEventHandling extends IPlugin {
  constructor(aliasName, data) {
    super(aliasName, data);
  }

  init() {
    const T = this.constructor;
    const TI = this;

    TI.SEVT_POPSTATE = new SystemEventHandler('', undefined, window, 'popstate', this._handlePopstate);
    TI.SEVT_POPSTATE.init();

    super.init();
  }

  _handlePopstate(e) {
  }
}
Plugins.catalogize(pSysEventHandling);
```

### Meaning of elements

- TI.SEVT_POPSTATE - contains an instance of 🔌 [SystemEventHandler][SystemEventHandler], a plugin that handles pairing with JavaScript system events. Here is an example of pairing with the **window** object, **popstate** event. 
- _handlePopstate - handler when capturing the **popstate** event
- e - JavaScript system event object

#### SystemEventHandler constructor parameters

| Parameter | Description |
|---|---|
| aliasName | plugin id (can remain '') |
| data | object with configuration data (can remain undefined) |
| target | target system object to which the plugin should connect |
| eventName | name of the JavaScript system event |
| handler | handler for the event on the application side |

Plugin configuration documentation 🔌 [pConvertSysEventToEvent][pConvertSysEventToEvent] is also valid here.

### Further information

For more information on JavaScript system events, see the documentation for the **ES2021** (**ECMA script**) JavaScript standard.  
The introduction at [geeksforgeeks][geeksforgeeks1] can help you get a basic overview.

[pConvertSysEventToEvent]: pConvertSysEventToEvent.md "pConvertSysEventToEvent"
[handler]: handler.md "Event handler"
[SystemEventHandler]: :_plg:SystemEventHandler.md "SystemEventHandler"
[geeksforgeeks1]: https://www.geeksforgeeks.org/javascript/javascript-events/ "JavaScript Events"
