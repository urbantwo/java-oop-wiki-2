# Classi Astratte — Teoria

## Cos'è una classe astratta?

Una **classe astratta** è una classe che non può essere istanziata direttamente. Serve da base comune per un gruppo di classi, fornendo:

- Alcuni metodi **già implementati** (condivisi da tutte le sottoclassi)
- Alcuni metodi **astratti** (che ogni sottoclasse *deve* implementare)

```java
abstract class Forma {           // (1)
    String colore;

    // Metodo CONCRETO — già implementato, ereditato da tutti
    public void mostraColore() {
        System.out.println("Colore: " + colore);
    }

    // Metodo ASTRATTO — nessun corpo, ogni sottoclasse lo deve implementare
    public abstract double calcolaArea();  // (2)
}
```

1. La parola chiave `abstract` davanti a `class` rende la classe non istanziabile.
2. Un metodo `abstract` non ha corpo `{}`. Termina con `;`.

---

## Non si può istanziare

```java
Forma f = new Forma();   // ❌ ERRORE di compilazione!
```

Ha senso: una `Forma` generica non esiste — esiste un `Cerchio`, un `Rettangolo`, ecc.

---

## Le sottoclassi concrete

```java
class Cerchio extends Forma {
    double raggio;

    public Cerchio(double raggio, String colore) {
        this.raggio = raggio;
        this.colore = colore;
    }

    @Override
    public double calcolaArea() {          // obbligatorio!
        return Math.PI * raggio * raggio;
    }
}

class Rettangolo extends Forma {
    double base, altezza;

    public Rettangolo(double base, double altezza, String colore) {
        this.base    = base;
        this.altezza = altezza;
        this.colore  = colore;
    }

    @Override
    public double calcolaArea() {          // obbligatorio!
        return base * altezza;
    }
}
```

```java
// Uso
Cerchio c = new Cerchio(5.0, "rosso");
c.mostraColore();                          // ereditato da Forma
System.out.println(c.calcolaArea());       // 78.53...

Rettangolo r = new Rettangolo(4, 6, "blu");
System.out.println(r.calcolaArea());       // 24.0
```

!!! info "Regola fondamentale"
    Se una sottoclasse non implementa **tutti** i metodi astratti della superclasse, deve essere dichiarata `abstract` a sua volta.

---

[:octicons-arrow-right-24: Quando usarle](quando.md)
