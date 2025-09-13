# 📄 Seznam pluginů (plugins.lst)

- ⚠️ Tento formát je velmi přísný, prosím, dodržujte pravidla přesně.
- Soubor definuje seznam a pořadí javascript souborů s pluginově organizovaným kódem, které aplikace zavede.
- Jeden řádek = jedna položka
- Zalomení řádku uprostřed definice není povoleno

## Struktura souboru

```text
[1]
[1]:
[1]:[2]
[1]:[2];[2]
```

## Popis pozic

| Pozice | Popis |
|---|---|
| `[1]` | Relativní cesta k souboru bez přípony vzhledem ke kořeni úložiště dat. |
| `[2]` | Název instance (id) pluginu. |

## Popis definic

| Definice | Popis |
|---|---|
| `[1]` | Plugin je pouze načten do paměti. Vhodné pro pluginy ze kterých se pouze odvozují jiné pluginy, ale není záměrem, aby samy byly v aplikaci aktivní. |
| `[1]:` | Plugin je načten a zaveden s id ''. |
| `[1]:[2]` | Plugin je načten a zaveden s id [2]. |
| `[1]:[2];[2]` | Plugin je načten a zaveden ve více instancích. Pořadí zavádění a použití id je podle definic [2]. |

## Další funkce

- Při zavedení každé instance systém automaticky zjišťuje, zda existuje pro instanci pluginu samostatná konfigurace. Jméno souboru je vždy: **plugins-config/[1]_[2].cfg**. Pokud je [2] neuvedeno, pak je použito jméno **plugins-config/[1]_.cfg**.
