# ⚡ Event

An event defines an application event/message.  
An event can be defined with a handler or just defined (without a handler).

## Definition

1. Define the event data object or specify which of the already defined descendants ⚡ [IEvent][IEvent] is suitable for your event:

```javascript
class ClickHandlerRegister extends IEvent {
  constructor() {
    super();
    this.handlerId = undefined;
    this.handler = undefined;
  }
}
```

2. Define the plugin class for the event:

```javascript
class pEventPlugin extends IPlugin {
  static EVT_CLICK_HANDLER_REGISTER = 'ClickHandlerRegister';

  init() {
    const T = this.constructor;
    const TI = this;

    // (B)

    super.init();
  }
}
Plugins.catalogize(pEventPlugin);
```

3. Decide whether you can have the handler directly in the plugin or whether you need to have it outside the plugin. Depending on your case, choose the necessary procedure according to the following chapters.

4. Always insert the source code of the chapter into the comment **(B)**.

### ⚡ Event with handler

```javascript
    const h_EVT_CLICK_HANDLER_REGISTER = (reply) => {
      // ...
      reply.result = 'replyValue';
    }
    TI.eventDefinitions.push([T.EVT_CLICK_HANDLER_REGISTER, ClickHandlerRegister, h_EVT_CLICK_HANDLER_REGISTER]);
```

### 📄⚡ Event only defined

```javascript
    TI.eventDefinitions.push([T.EVT_CLICK_HANDLER_REGISTER, ClickHandlerRegister, null]); // outside event handlers
```

### Meaning of elements

- class ClickHandlerRegister - event data object (it is possible to use the same class for multiple events or inherit from any IEvent descendant)
- ClickHandlerRegister.constructor - contains the default values of the message object. It is desirable that the values be pre-filled with the default value according to the planned type, if possible. This data is used in the [object explorer][oexplorer] as part of the system's automatic documentation.
- const h_EVT_CLICK_HANDLER_REGISTER - event handler
- reply.result - standard event property (⚡ [IEvent][IEvent]), which is automatically taken over by the application logic as the handler's response to the event. It can be any object.
- TI.eventDefinitions.push([T.EVT_CLICK_HANDLER_REGISTER, ClickHandlerRegister, null]) - creates an event definition prescription (event name, event data object, and handler method, or null if the event is only to be defined). The processing of definitions is handled by the ancestor 🔌 [IPlugin][IPlugin].
- super.init(); - performs standard initialization of bindings. It must be the last command in order for everything defined to be initialized properly.

## Sending an event

In the handler code, you can then trigger events as follows:

```javascript
      const eventName = EventNames.MyNewEvent; //or: 'MyNewEvent'

      sendEvent(eventName, (r) => {
        r.id = aliasName;
        r.result = loadedCount;
        //fill another data of event
      });
```

In the **appmainBaseLogic.js** file, you will find examples of functions that encapsulate similar calls.  
> [!WARNING]
> It is recommended to create a similar set of functions for your plugin in a separate file (which you will add to the [list of scripts](js.lst.md "List of scripts")). Calls to the **sendEvent** method are not indexed for the [object explorer](oexplorer.md "Object explorer"), but these functions will be indexed.

## Records 🛰️

A record in the 🛰️ [object explorer][oexplorer] means that:

- in the plugin instance overview: the plugin sends the event ...
- in the list of event communication paths: the event is sent from ...

[IEvent]: :_evt:IEvent.md "IEvent"
[oexplorer]: oexplorer.md "Object explorer"
[IPlugin]: :_plg:IPlugin.md "IPlugin"
