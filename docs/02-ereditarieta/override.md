# Override & super

## Ridefinire un metodo ereditato

La sottoclasse può **sovrascrivere** (override) un metodo della superclasse per cambiarne il comportamento.

```java
class Animale {
    public String descrivi() {
        return "Sono un animale";
    }
}

class Cane extends Animale {

    @Override                           // (1)
    public String descrivi() {
        return "Sono un cane!";         // (2)
    }
}

class Gatto extends Animale {

    @Override
    public String descrivi() {
        return super.descrivi()         // (3)
               + " e sono un gatto.";
    }
}
```

1. `@Override` avvisa il compilatore che stai ridefinendo un metodo esistente. Non è obbligatorio ma è **buona pratica**: se sbagli il nome del metodo il compilatore ti segnala l'errore.
2. Questa versione **sostituisce** completamente quella di `Animale`.
3. `super.descrivi()` chiama la versione del **genitore**, poi ci aggiunge qualcosa.

---

## Confronto: sostituire vs estendere

=== "Sostituisce il comportamento"

    ```java
    class Cane extends Animale {
        @Override
        public String descrivi() {
            return "Sono un cane!";
            // ignora completamente Animale.descrivi()
        }
    }
    // Output: "Sono un cane!"
    ```

=== "Estende il comportamento"

    ```java
    class Gatto extends Animale {
        @Override
        public String descrivi() {
            return super.descrivi() + " e sono un gatto.";
            // riusa Animale.descrivi() e ci aggiunge
        }
    }
    // Output: "Sono un animale e sono un gatto."
    ```

---

## Regole dell'Override

| Regola | Dettaglio |
|---|---|
| Stesso nome | Il metodo deve avere lo stesso nome |
| Stessa firma | Stessi parametri (tipo e numero) |
| Accesso uguale o più ampio | Non puoi restringere la visibilità |
| `@Override` | Non obbligatorio ma sempre consigliato |

!!! danger "Errore comune"
    Se scrivi `descivi()` invece di `descrivi()`, Java non ti avverte — crea un nuovo metodo invece di sovrascrivere. Con `@Override` il compilatore lancia un errore.

---

[:octicons-arrow-right-24: Prossima sezione: Classi Astratte](../03-astratte/teoria.md)
