# Esercizio 2 — Ereditarietà

!!! abstract "Consegna"
    Crea una gerarchia `Veicolo → Automobile` e `Veicolo → Moto`.
    `Veicolo` ha i campi `targa` e `velocitaMax`.
    `Automobile` aggiunge `numPorte`, `Moto` aggiunge `haCarrozzeria`.
    Ogni classe ha un metodo `descrivi()` che `Automobile` e `Moto` sovrascrivono chiamando `super`.

**Livello:** Medio &nbsp;·&nbsp; **Tempo stimato:** ~15 min

---

## Gerarchia da costruire

```
Veicolo
├── Automobile   (+ numPorte)
└── Moto         (+ haCarrozzeria)
```

---

## Skeleton da completare

```java title="Veicoli.java"
class Veicolo {
    String targa;
    int    velocitaMax;

    // TODO: costruttore(targa, velocitaMax)

    // TODO: metodo descrivi() → "Targa: XX · Max: YY km/h"
}

class Automobile extends Veicolo {
    int numPorte;

    // TODO: costruttore — ricorda super(...)

    // TODO: @Override descrivi()
    //   chiama super.descrivi() e aggiungi " · Porte: N"
}

class Moto extends Veicolo {
    boolean haCarrozzeria;

    // TODO: costruttore — ricorda super(...)

    // TODO: @Override descrivi()
}
```

```java title="Main.java — BONUS polimorfismo"
Veicolo[] garage = {
    new Automobile("AB123CD", 180, 5),
    new Moto("MO999XY", 220, false),
    new Automobile("ZZ000ZZ", 150, 3)
};

for (Veicolo v : garage) {
    System.out.println(v.descrivi());  // polimorfismo!
}
```

---

## Step guidati

- [ ] **Step 1** — Implementa `Veicolo` con costruttore e `descrivi()`
- [ ] **Step 2** — Crea `Automobile extends Veicolo`, usa `super(...)` nel costruttore
- [ ] **Step 3** — Override `descrivi()` chiamando `super.descrivi()` e aggiungendo le porte
- [ ] **Step 4** — Fai lo stesso per `Moto`
- [ ] **BONUS** — Crea l'array `Veicolo[]` e verifica che il polimorfismo funzioni

---

## Soluzione

??? success "Mostra la soluzione"

    ```java title="Veicoli.java — soluzione"
    class Veicolo {
        String targa;
        int    velocitaMax;

        public Veicolo(String targa, int velocitaMax) {
            this.targa       = targa;
            this.velocitaMax = velocitaMax;
        }

        public String descrivi() {
            return "Targa: " + targa + " · Max: " + velocitaMax + " km/h";
        }
    }

    class Automobile extends Veicolo {
        int numPorte;

        public Automobile(String targa, int velocitaMax, int numPorte) {
            super(targa, velocitaMax);
            this.numPorte = numPorte;
        }

        @Override
        public String descrivi() {
            return super.descrivi() + " · Porte: " + numPorte;
        }
    }

    class Moto extends Veicolo {
        boolean haCarrozzeria;

        public Moto(String targa, int velocitaMax, boolean haCarrozzeria) {
            super(targa, velocitaMax);
            this.haCarrozzeria = haCarrozzeria;
        }

        @Override
        public String descrivi() {
            return super.descrivi() + " · Carrozzeria: " + (haCarrozzeria ? "sì" : "no");
        }
    }
    ```

---

[:octicons-arrow-right-24: Esercizio 3](ex3.md)
