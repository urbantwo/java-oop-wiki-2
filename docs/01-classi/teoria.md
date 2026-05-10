# Classi & Oggetti — Teoria

## Cos'è una Classe?

Una **classe** è un modello (*blueprint*) che descrive le caratteristiche e i comportamenti di un insieme di oggetti. Pensa alla classe come allo stampo, e agli oggetti come alle copie concrete prodotte da quello stampo.

```
Classe Auto  →  oggetto Ferrari, oggetto Fiat, oggetto BMW
     ↑                   ↑              ↑              ↑
  (stampino)          (istanze concrete)
```

---

## Struttura di una Classe

Ogni classe è composta da tre elementi fondamentali:

| Elemento | Descrizione | Esempio |
|---|---|---|
| **Campi** (fields) | Le proprietà dell'oggetto | `String marca` |
| **Costruttore** | Metodo speciale che inizializza l'oggetto | `Auto(String m, int v)` |
| **Metodi** | I comportamenti dell'oggetto | `void accelera(int delta)` |

---

## Parole chiave fondamentali

- `class` — definisce una nuova classe
- `new` — crea un'istanza (un oggetto) di quella classe
- `this` — riferimento all'oggetto corrente all'interno della classe

---

## Esempio completo

```java title="Auto.java"
public class Auto {

    // ── Campi ──────────────────────────────────
    String marca;
    int    velocita;

    // ── Costruttore ────────────────────────────
    public Auto(String marca, int velocita) {
        this.marca    = marca;     // this distingue campo da parametro
        this.velocita = velocita;
    }

    // ── Metodi ─────────────────────────────────
    public void accelera(int delta) {
        velocita += delta;
    }

    public void frena(int delta) {
        velocita = Math.max(0, velocita - delta);
    }

    public String toString() {
        return marca + " @ " + velocita + " km/h";
    }
}
```

```java title="Main.java"
public class Main {
    public static void main(String[] args) {

        Auto a = new Auto("Ferrari", 0);  // crea un oggetto
        a.accelera(100);
        System.out.println(a);            // Ferrari @ 100 km/h

        Auto b = new Auto("Fiat", 50);    // altro oggetto, indipendente
        b.frena(20);
        System.out.println(b);            // Fiat @ 30 km/h
    }
}
```

!!! note "Oggetti indipendenti"
    `a` e `b` sono due oggetti **separati**. Modificare `a` non influenza `b`, anche se sono entrambi di tipo `Auto`.

---

## Modificatori di accesso

```java
public class Persona {
    public    String nome;      // accessibile da ovunque
    private   int    eta;       // accessibile solo dentro la classe
    protected String cognome;   // accessibile da classe e sottoclassi
}
```

!!! tip "Buona pratica"
    Rendi i campi `private` e fornisci metodi `get`/`set` pubblici per accedervi (incapsulamento).

---

[:octicons-arrow-right-24: Esempi pratici](esempi.md)
