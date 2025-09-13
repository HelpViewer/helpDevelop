# ⚙️ Konfigurace pluginů

Aplikace automaticky zajišťuje propis konfigurace do jednotlivých instancí pluginů při jejich zavádění.

Ve stejném datovém souboru z jakého je načten plugin (aplikace nebo souboru nápovědy) je hledáno umístění:  

- **zip/plugins-config/[jméno třídy]_[jméno instance].cfg** (v datech aplikace)
- **plugins-config/[jméno třídy]_[jméno instance].cfg** (ve základních datech nápovědy **Help-.zip** nebo **kořen adresáře bez jazyka**)

Pokud existuje, načte se a předá se instanci pluginu. Pokud neexistuje, hodnoty jsou předvyplněny logikou a hodnotami konstant **DEFAULT_KEY_CFG_**... .

## Pravidla formátu

- ⚠️ Tento formát je velmi přísný, prosím, dodržujte pravidla přesně.
- Jeden řádek = jedna položka
- Zalomení řádku uprostřed definice není povoleno a to ani u hodnot
- V případě shody názvů klíče se propisuje vždy poslední definovaná hodnota
- V případě vícehodnotových výčtů je výčet hodnot uveden na jednom řádku a oddělovačem je obvykle **;**. Zpracování a rozdělení hodnot si zajišťuje každý plugin sám (může mít tedy vlastní oddělovač, avšak oddělovači **|** je doporučeno se vyhnout)

## Struktura souboru

```text
[1]|[2]
```

## Popis pozic

| Pozice | Popis |
|---|---|
| `[1]` | Název konfiguračního klíče |
| `[2]` | Hodnota konfiguračního klíče |
