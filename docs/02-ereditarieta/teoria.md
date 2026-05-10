# Ereditarietà — Teoria

## Cos'è l'ereditarietà?

L'**ereditarietà** permette a una classe (*sottoclasse*) di acquisire campi e metodi di un'altra classe (*superclasse*), evitando di riscrivere codice già esistente e permettendo di specializzarlo.

```
Animale          ← superclasse (genitore)
├── Cane         ← sottoclasse (figlio)
├── Gatto        ← sottoclasse (figlio)
└── Uccello      ← sottoclasse (figlio)
```

La relazione si legge **"è un tipo di"**: `Cane` *è un tipo di* `Animale`.

---

## La parola chiave `extends`

```java title="Ereditarieta.java"
class Animale {
    String nome;

    public void mangia() {
        System.out.println(nome + " sta mangiando");
    }
}

// Cane ESTENDE Animale → eredita nome e mangia()
class Cane extends Animale {

    // Aggiunge un campo proprio
    String razza;

    // Aggiunge un metodo proprio
    public void abbaia() {
        System.out.println("Bau! Sono " + nome);
    }
}
```

```java
Cane c = new Cane();
c.nome = "Rex";       // campo ereditato da Animale
c.razza = "Labrador"; // campo proprio di Cane
c.mangia();           // metodo ereditato
c.abbaia();           // metodo proprio
```

---

## Il costruttore e `super()`

Quando la superclasse ha un costruttore con parametri, la sottoclasse **deve chiamarlo** con `super(...)` come prima istruzione del suo costruttore.

```java
class Animale {
    String nome;

    public Animale(String nome) {
        this.nome = nome;
    }
}

class Cane extends Animale {
    String razza;

    public Cane(String nome, String razza) {
        super(nome);       // (1) chiama il costruttore di Animale
        this.razza = razza;
    }
}
```

1. `super(nome)` deve essere la **prima riga** del costruttore figlio.

!!! warning "Ereditarietà singola"
    In Java una classe può estendere **una sola** classe. Per ereditarietà multipla si usano le interfacce.

---

[:octicons-arrow-right-24: Override & super](override.md)
