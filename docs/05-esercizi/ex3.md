# Esercizio 3 — Abstract + Interface

!!! abstract "Consegna"
    Crea una classe astratta `Dipendente` con `nome` e `stipendioBase`, e il metodo astratto `calcolaStipendio()`.
    Crea l'interfaccia `Tassabile` con il metodo `calcolaTasse()`.
    Implementa `Manager` (+30% di bonus, tasse 35%) e `Sviluppatore` (+15%, tasse 30%).
    Solo `Manager` implementa `Tassabile`.

**Livello:** Avanzato &nbsp;·&nbsp; **Tempo stimato:** ~20 min

---

## Schema da costruire

```
Dipendente (abstract)
├── Manager      extends Dipendente implements Tassabile
└── Sviluppatore extends Dipendente

Tassabile (interface)
└── Manager implements Tassabile
```

---

## Skeleton da completare

```java title="Azienda.java"
interface Tassabile {
    double calcolaTasse();
}

abstract class Dipendente {
    String nome;
    double stipendioBase;

    // TODO: costruttore(nome, stipendioBase)

    // Ogni dipendente calcola lo stipendio a modo suo
    public abstract double calcolaStipendio();

    // Metodo concreto condiviso — già implementato
    public void stampaPaga() {
        System.out.printf("%s guadagna %.2f€%n",
                          nome, calcolaStipendio());
    }
}

// Manager: stipendioBase * 1.30, tasse 35%
class Manager extends Dipendente implements Tassabile {
    // TODO: costruttore
    // TODO: @Override calcolaStipendio()
    // TODO: @Override calcolaTasse()
}

// Sviluppatore: stipendioBase * 1.15, NON paga tasse separatamente
class Sviluppatore extends Dipendente {
    // TODO: costruttore
    // TODO: @Override calcolaStipendio()
}
```

```java title="Main.java — BONUS"
Dipendente[] team = {
    new Manager("Alice", 3000),
    new Sviluppatore("Bob", 2500),
    new Manager("Carlo", 3500)
};

double totalePaga  = 0;
double totaleTasse = 0;

for (Dipendente d : team) {
    d.stampaPaga();
    totalePaga += d.calcolaStipendio();

    // instanceof per verificare se implementa Tassabile
    if (d instanceof Tassabile t) {         // Java 16+ pattern matching
        totaleTasse += t.calcolaTasse();
    }
}

System.out.printf("Totale paga:  %.2f€%n", totalePaga);
System.out.printf("Totale tasse: %.2f€%n", totaleTasse);
```

---

## Step guidati

- [ ] **Step 1** — Definisci l'interfaccia `Tassabile`
- [ ] **Step 2** — Implementa la classe `abstract Dipendente` con costruttore e `stampaPaga()`
- [ ] **Step 3** — Crea `Manager` con `extends` **e** `implements` insieme
- [ ] **Step 4** — Crea `Sviluppatore` (solo `extends`, niente tasse)
- [ ] **BONUS** — Array `Dipendente[]`, calcola i totali usando `instanceof`

---

## Soluzione

??? success "Mostra la soluzione"

    ```java title="Azienda.java — soluzione"
    interface Tassabile {
        double calcolaTasse();
    }

    abstract class Dipendente {
        String nome;
        double stipendioBase;

        public Dipendente(String nome, double stipendioBase) {
            this.nome          = nome;
            this.stipendioBase = stipendioBase;
        }

        public abstract double calcolaStipendio();

        public void stampaPaga() {
            System.out.printf("%s guadagna %.2f€%n",
                              nome, calcolaStipendio());
        }
    }

    class Manager extends Dipendente implements Tassabile {

        public Manager(String nome, double stipendioBase) {
            super(nome, stipendioBase);
        }

        @Override
        public double calcolaStipendio() {
            return stipendioBase * 1.30;
        }

        @Override
        public double calcolaTasse() {
            return calcolaStipendio() * 0.35;
        }
    }

    class Sviluppatore extends Dipendente {

        public Sviluppatore(String nome, double stipendioBase) {
            super(nome, stipendioBase);
        }

        @Override
        public double calcolaStipendio() {
            return stipendioBase * 1.15;
        }
    }
    ```

---

[:octicons-arrow-right-24: Vai al riepilogo](../riepilogo.md)
