# Interfacce — Teoria

## Cos'è un'interfaccia?

Un'**interfaccia** è un contratto puro: definisce *cosa* un oggetto sa fare, senza specificare *come* lo fa. Chi implementa l'interfaccia si impegna a fornire quella funzionalità.

```java
interface Volante {                      // (1)
    void   vola();                       // (2) astratto per default
    double getAltitudine();              // (2) astratto per default

    // Da Java 8: metodi default (con implementazione)
    default void atterra() {             // (3)
        System.out.println("Atterraggio in corso...");
    }
}
```

1. Si usa `interface` al posto di `class`.
2. Tutti i metodi sono `public abstract` per default — non serve scriverlo.
3. I metodi `default` hanno un'implementazione opzionale che le classi possono sovrascrivere.

---

## Implementare un'interfaccia

```java
class Aereo implements Volante {          // (1)
    private double quota;

    @Override
    public void vola() {
        quota = 10000;
        System.out.println("Aereo in volo a " + quota + "m");
    }

    @Override
    public double getAltitudine() {
        return quota;
    }
    // atterra() è già implementato dall'interfaccia (default)
}

class Uccello implements Volante {
    @Override
    public void vola() {
        System.out.println("L'uccello batte le ali");
    }

    @Override
    public double getAltitudine() { return 50; }
}
```

1. `implements` al posto di `extends`.

---

## Ereditarietà multipla

Una classe può implementare **più interfacce** contemporaneamente — cosa impossibile con `extends`.

```java
interface Volante    { void vola();     }
interface Nuotatore  { void nuota();    }
interface Corridore  { void corri();    }

// Anatra sa fare tutte e tre!
class Anatra implements Volante, Nuotatore, Corridore {

    @Override public void vola()  { System.out.println("Volo!"); }
    @Override public void nuota() { System.out.println("Nuoto!"); }
    @Override public void corri() { System.out.println("Corro!"); }
}
```

---

## Regole riassuntive

| Cosa | Consentito? |
|---|---|
| Campi di stato | ❌ Solo costanti (`public static final`) |
| Costruttore | ❌ No |
| Metodi astratti | ✅ Sì (default) |
| Metodi `default` | ✅ Da Java 8 |
| Metodi `static` | ✅ Da Java 8 |
| Ereditarietà multipla | ✅ Sì |

---

[:octicons-arrow-right-24: Abstract vs Interface](confronto.md)
