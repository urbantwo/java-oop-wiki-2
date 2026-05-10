# Classi & Oggetti — Esempi

## Esempio 1 — Studente

```java title="Studente.java"
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

    // getter
    public String getNome() { return nome; }
    public int    getEta()  { return eta;  }
}
```

```java title="Main.java"
Studente s1 = new Studente("Luca", 20, "MAT001");
Studente s2 = new Studente("Anna", 22, "MAT002");

s1.presentati(); // Mi chiamo Luca, ho 20 anni. Matricola: MAT001
s2.presentati(); // Mi chiamo Anna, ho 22 anni. Matricola: MAT002
```

---

## Esempio 2 — Conto Bancario

```java title="ContoBancario.java"
public class ContoBancario {
    private String intestatario;
    private double saldo;

    public ContoBancario(String intestatario, double saldoIniziale) {
        this.intestatario = intestatario;
        this.saldo        = saldoIniziale;
    }

    public void deposita(double importo) {
        if (importo > 0) saldo += importo;
    }

    public boolean preleva(double importo) {
        if (importo > saldo) {
            System.out.println("Saldo insufficiente!");
            return false;
        }
        saldo -= importo;
        return true;
    }

    public void stampaSaldo() {
        System.out.printf("[%s] Saldo: %.2f€%n", intestatario, saldo);
    }
}
```

```java
ContoBancario c = new ContoBancario("Mario", 1000.0);
c.deposita(500.0);
c.preleva(200.0);
c.stampaSaldo();  // [Mario] Saldo: 1300.00€
```

---

## Punti da ricordare

!!! success "✔ Fai così"
    - Usa `private` per i campi
    - Inizializza tutto nel costruttore
    - Ogni metodo fa **una cosa sola**

!!! warning "✘ Evita"
    - Campi pubblici modificabili direttamente
    - Costruttori senza parametri quando i dati sono obbligatori
    - Metodi che fanno troppe cose

---

[:octicons-arrow-right-24: Prossima sezione: Ereditarietà](../02-ereditarieta/teoria.md)
