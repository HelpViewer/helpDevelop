# 👂 Obsluha události

Obsluha definuje reakci systému na konkrétní událost.

Pokud jste ⚡ [událost definovali s obsluhou][eventWH], tento postup pro vás již nemá v rámci jednoho pluginu smysl.

## Definice

1. Uvnitř jiného pluginu definujte funkci:

```javascript
  onET_ClickHandlerRegister(evt) {
  }
```

- evt bude obsahovat instanci třídy **ClickHandlerRegister** s daty události.

## Význam jména funkce

- onET_ClickHandlerRegister (podtržítko) - příjímá události **ClickHandlerRegister** pro jakékoli id pluginu a to i když bude definováno 🔺 [filtrování][filter].
- onETClickHandlerRegister - příjímá události **ClickHandlerRegister** s [id][IEvent-ID], které se shoduje s **plugin.aliasName**.

### Další informace

- Struktura události ⚡ [IEvent][IEvent]
- 🔺 [Filtrování][filter] událostí na straně pluginu
- Podrobnější popis k 🔺 [filtrování událostí][filter2]

[IEvent]: :_evt:IEvent.md "IEvent"
[IEvent-ID]: :_evt:IEvent.md#h-4-4 "IEvent id"
[eventWH]: event.md#h-3-0 "Událost s obsluhou"
[filter]: eventFilter.md "Filtrování"
[filter2]: eventFilterD.md "Podrobnosti k filtrování"
