# ⚙️ Konfigurace pluginů

Aplikace automaticky při načítání pluginů zajišťuje propis konfigurace do jednotlivých instancí pluginů při jejich zavádění.

Při zavádění instance pluginu je automaticky ve stejném datovém souboru z jakého pochází plugin (aplikace nebo souboru nápovědy) hledáno umístění:  

- **zip/plugins-config/[jméno třídy]_[jméno instance].cfg** (v datech aplikace)
- **plugins-config/[jméno třídy]_[jméno instance].cfg** (ve základních datech nápovědy **Help-.zip** nebo **kořen adresáře bez jazyka**)

Pokud existuje, načte se a předá se instanci pluginu. Pokud neexistuje, hodnoty jsou předvyplněny logikou a hodnotami konstant **DEFAULT_KEY_CFG_**... .

## Pravidla formátu

- ⚠️ Tento formát je velmi přísný, prosím, dodržujte pravidla přesně.
- Jeden řádek = jedna položka
- Zalomení řádku uprostřed definice není povoleno
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
