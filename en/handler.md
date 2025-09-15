# 👂 Event handler

The handler defines the system's response to a specific event.

If you have ⚡ [defined the event with a handler][eventWH], this procedure no longer makes sense for you within a single plugin.

## Definition

1. Define the function inside another plugin:

```javascript
  onET_ClickHandlerRegister(evt) {
  }
```

- evt will contain an instance of the **ClickHandlerRegister** class with event data.

## Meaning of the function name

- onET_ClickHandlerRegister (underscore) - receives **ClickHandlerRegister** events for any plugin id, even if 🔺 [filtering][filter] is defined.
- onETClickHandlerRegister - receives **ClickHandlerRegister** events with [id][IEvent-ID] that matches **plugin.aliasName**. The id '' is also considered a match in this method.

### Additional information

- Event structure ⚡ [IEvent][IEvent]
- 🔺 [Filtering][filter] events on the plugin side
- More detailed description of 🔺 [event filtering][filter2]

[IEvent]: :_evt:IEvent.md "IEvent"
[IEvent-ID]: :_evt:IEvent.md#h-4-4 "IEvent id"
[eventWH]: event.md#h-3-0 "Event with handler"
[filter]: eventFilter.md "Filtering"
[filter2]: eventFilterD.md "Detailed description of event filtering"
