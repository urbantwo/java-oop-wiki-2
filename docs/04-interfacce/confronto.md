# Classe Astratta vs Interfaccia

## Tabella comparativa

| Caratteristica | Classe Astratta | Interfaccia |
|---|---|---|
| Parola chiave | `extends` | `implements` |
| Ereditarietà | **Singola** (1 sola) | **Multipla** (quante vuoi) |
| Campi di stato | ✅ Sì | ❌ Solo costanti |
| Costruttore | ✅ Sì | ❌ No |
| Metodi concreti | ✅ Sì | ✅ Con `default` (Java 8+) |
| Metodi astratti | ✅ Sì | ✅ Sì (per default) |
| Uso tipico | Base comune con codice condiviso | Capacità/contratto trasversale |

---

## Esempio parallelo

=== "Classe Astratta"

    ```java
    abstract class Dipendente {
        String nome;           // stato condiviso
        double stipendioBase;

        // logica condivisa
        public void stampaNome() {
            System.out.println("Dipendente: " + nome);
        }

        // ogni tipo calcola a modo suo
        public abstract double calcolaStipendio();
    }

    class Manager extends Dipendente {
        @Override
        public double calcolaStipendio() {
            return stipendioBase * 1.3;  // +30% bonus
        }
    }
    ```

=== "Interfaccia"

    ```java
    interface Tassabile {
        double calcolaTasse();   // solo contratto, nessuno stato
    }

    // Manager è Dipendente (extends) E Tassabile (implements)
    class Manager extends Dipendente implements Tassabile {

        @Override
        public double calcolaStipendio() {
            return stipendioBase * 1.3;
        }

        @Override
        public double calcolaTasse() {
            return calcolaStipendio() * 0.35;
        }
    }
    ```

!!! tip "La regola d'oro"
    Usa la **classe astratta** quando le classi condividono codice e stato.
    Usa l'**interfaccia** per aggiungere capacità trasversali a classi anche non correlate.

---

[:octicons-arrow-right-24: Polimorfismo](polimorfismo.md)
