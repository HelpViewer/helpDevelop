# 🎛️ UI prvky

Následující podkapitoly stromu popisují komponenty, které aplikace běžně používá.

Prvky, které ve stromě uvedené nejsou, je možné založit jako standardní javascript **input** elementy. Se založením těchto elementů pomohou funkce níže.

Pokud je to možné, upřednostněte použití celého pluginu (například s tlačítkem a akcí).

## Podpora na straně aplikace

V těchto podkapitolách je vždy rozebraná jednotlivá funkce a její parametry.

### appendField

Vytvoří nové **INPUT** pole s popiskem, který prvek označí, pokud se na popisek klikne.

| Parametr | Výchozí | Popis |
|---|---|---|
| target | povinný | Cílový rodičovský prvek |
| id | povinný | id nového prvku. Lokalizační systém id prvku používá pro automatické párování svých klíčů na UI |
| defaultV | '' | Vyýchozí hodnota prvku |
| type | FormFieldType.TEXT | Typ pole. FormFieldType obsahuje hodnoty, které je možné použít. Hodnoty: TEXT, CHECKBOX, FILE |

### appendFieldComboBox

Vytvoří nové pole **select/combobox** s popiskem, který prvek označí, pokud se na popisek klikne.

| Parametr | Výchozí | Popis |
|---|---|---|
| target | povinný | Cílový rodičovský prvek |
| id | povinný | id nového prvku. Lokalizační systém id prvku používá pro automatické párování svých klíčů na UI |

### appendComboBoxItems

K existujícímu **select/combobox** poli přidá seznam položek.

| Parametr | Výchozí | Popis |
|---|---|---|
| combobox | povinný | HTML element comboboxu |
| items | povinný | Pole jmen položek. |
| defaultV | povinný | Hodnota, která má být označena za výchozí (předvybranou). Může být specifikována textem položky nebo indexem (vnitřní logika automaticky čísluje položky indexem v items). |
