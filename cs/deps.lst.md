# 📄 Seznam externích závislostí (deps.lst)

- > [!WARNING] Tento formát je velmi přísný, prosím, dodržujte pravidla přesně.
- Soubor definuje seznam externích souborů nebo balíčků, které CI skript připojí k balíčku vydání.
- Jeden řádek = jedna položka
- Zalomení řádku uprostřed definice není povoleno

## Struktura souboru

```text
[1]|[2][|]
```

## Popis pozic

| Pozice | Popis |
|---|---|
| `[1]` | Jméno souboru na straně balíčku aplikace |
| `[2]` | Jméno souboru na straně zdroje externího souboru/balíčku |
| `[\|]` | Pokud řádek končí svislou čarou, kopíruje se do adresáře **hvdata**, jinak se soubor vloží do **hvdata/data.zip**. |
