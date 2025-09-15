# 🔌 pConvertSysEventToEvent

## Purpose of the plugin

The plugin converts a defined JavaScript event into an application event that can be captured by another plugin.

## Implementation

### 1) Configuration with automatic sending of ConvertedSystemEvent

1. In the **plugins.lst** file, add the following line:  
   pConvertSysEventToEvent:[instanceid]
2. In the **plugins-config/pConvertSysEventToEvent_[instanceid].cfg** file, define, for example:

```text
SYSEVENTNAME|click
SYSOBJECT|body
EVENTBUSEVENT|ClickedEvent
EVENTBUSEVENTID|
```

| Name | Description |
|---|---|
| SYSEVENTNAME | Name of JavaScript system events (addEventListener). |
| SYSOBJECT | System object to which the plugin should be linked. Values: window, document, body, #xxx = HTML element with a specific id |
| EVENTBUSEVENT | Name of the event on the application side. |
| EVENTBUSEVENTID | Id property of the converted event being sent. Based on this property, the system can filter delivery to all (🟢) or to specific plugins that have the same id as the message (🔺). |

The JavaScript event will be automatically converted to a ⚡ [ConvertedSystemEvent][ConvertedSystemEvent] event, which will be sent with an **id** corresponding to **EVENTBUSEVENTID** and **eventName** matching the value of **EVENTBUSEVENT**.

### 2) Programmatic solution with custom conversion to another event object

1. Follow the steps in Chapter 1.
2. Prepare the following code in the **plugins/[plugin name].js** file, for example:

```javascript
class ClickedEvent extends IEvent {
  constructor() {
    super();
    this.elementId = '';
    this.elementIdRoot = '';
    this.elementIdVal = '';
    this.target = null;
    this.event = null;
    this.forwarded = false;
  }
}

ClickedEvent.register();

class pClickConverter extends pConvertSysEventToEvent {
  constructor(aliasName, data) {
    super(aliasName, data);

    this.DEFAULT_KEY_CFG_SYSEVENTNAME = 'click';
    this.DEFAULT_KEY_CFG_SYSOBJECT = 'body';
    this.DEFAULT_KEY_CFG_EVENTBUSEVENT = 'ClickedEvent';
  }

  _fillEventObject(d, evt) {
    d.event = evt;
    d.target = d.event?.target;
    d.elementId = d.target?.id
    const splits = d.elementId?.replace('-', '|').split('|').filter(Boolean) ?? [];
    d.elementIdRoot = splits[0];
    d.elementIdVal = splits[1];
  }
}

Plugins.catalogize(pClickConverter);
```

- ClickedEvent is the target event object on the application side.
- **ClickedEvent.register()** registers the event object in the catalog (information about this entry can be found in **puiButtonObjectExplorer** in **Inheritance Tree**, chapter **Reference**). This is necessary because JavaScript cannot perform extended object detection by name. You must also include this name in the configuration in **EVENTBUSEVENT**.
- You can either leave the **this.DEFAULT_KEY_CFG_** lines in the code or remove them completely. The configuration from point 1 overwrites them.
- The _fillEventObject(d, evt) function performs the actual conversion of evt (JavaScript system event) to d (target event on the application side).
- Calling **Plugins.catalogize(pMinPlugin);** is mandatory. It adds the plugin to the catalog of loaded plugins.

The result of one processing will be an event ⚡ ClickedEvent with the content of the ClickedEvent class type from the example.

### ClickedEvent.register()

The IEvent.register() function ensures that the event class is added to the catalog so that it can later be linked to the name in the configuration.

| Parameter | Mandatory | Description |
|---|---|---|
| evtName | No | Event name if you want to link a specific class to a different event name. Specifying a (different) name is a kind of substitute for class inheritance. If necessary, you can logically link one class to multiple event names multiple times. |
| convertMethod | No | Function in the prescription (x, e), where x is the target instance of the application event and e is the JavaScript system event. |

## Examples of implementations

- 🔌 [pClickConverter][pClickConverter]

[pClickConverter]: :inst:pClickConverter:.md "pClickConverter"
[ConvertedSystemEvent]: :_evt:ConvertedSystemEvent.md "ConvertedSystemEvent"
