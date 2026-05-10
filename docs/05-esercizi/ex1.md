# Esercizio 1 — Classe base

!!! abstract "Consegna"
    Crea una classe `Studente` con i campi `nome`, `eta` e `matricola`.
    Aggiungi un costruttore e un metodo `presentati()` che stampa i dati.

**Livello:** Base &nbsp;·&nbsp; **Tempo stimato:** ~10 min

---

## Skeleton da completare

```java title="Studente.java"
public class Studente {

    // TODO 1: dichiara i campi
    //   nome      (String)
    //   eta       (int)
    //   matricola (String)


    // TODO 2: costruttore con tutti e tre i parametri
    public Studente(/* parametri */) {
        // usa this.campo = parametro
    }


    // TODO 3: metodo presentati()
    public void presentati() {
        // stampa nome, eta e matricola in modo leggibile
    }
}
```

```java title="Main.java"
public class Main {
    public static void main(String[] args) {

        Studente s = new Studente("Luca", 20, "MAT001");
        s.presentati();
        // Output atteso:
        // Mi chiamo Luca, ho 20 anni. Matricola: MAT001
    }
}
```

---

## Step guidati

- [x] **Step 1** — Dichiara i 3 campi con i tipi corretti
- [ ] **Step 2** — Scrivi il costruttore usando `this.campo = parametro`
- [ ] **Step 3** — Implementa `presentati()` con `System.out.printf` o `println`
- [ ] **Step 4** — Crea il `main` e verifica l'output
- [ ] **BONUS** — Aggiungi un metodo `promuovi()` che stampa "Promosso all'anno successivo!"

---

## Soluzione

??? success "Mostra la soluzione"

    ```java title="Studente.java — soluzione"
    public class Studente {

        private String nome;
        private int    eta;
        private String matricola;

        public Studente(String nome, int eta, String matricola) {
            this.nome      = nome;
            this.eta       = eta;
            this.matricola = matricola;
        }

        public void presentati() {
            System.out.printf("Mi chiamo %s, ho %d anni. Matricola: %s%n",
                              nome, eta, matricola);
        }

        // BONUS
        public void promuovi() {
            System.out.println(nome + " — Promosso all'anno successivo!");
        }
    }
    ```

---

[:octicons-arrow-right-24: Esercizio 2](ex2.md)
