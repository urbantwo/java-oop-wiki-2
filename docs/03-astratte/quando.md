# Quando usare le Classi Astratte?

## Guida rapida sì/no

!!! success "✔ Usala quando..."
    - Vuoi **condividere codice** tra classi simili (stessi campi, stessa logica di base)
    - Le classi hanno uno **stato comune** (campi in comune)
    - Vuoi imporre un **contratto parziale**: alcune cose già fatte, alcune obbligatorie
    - Ha senso dire *"X è un tipo di Y"* (relazione IS-A forte)

!!! failure "✘ Non usarla quando..."
    - Le classi **non sono correlate** tra loro (meglio un'interfaccia)
    - Devi ereditare da **più fonti diverse** (le interfacce permettono ereditarietà multipla)
    - Vuoi solo definire un **contratto puro** senza nessuna implementazione

---

## Confronto rapido

=== "Classe Astratta ✔"

    ```java
    // Ha senso: Veicolo condivide targa, velocità e metodi comuni
    abstract class Veicolo {
        String targa;
        int velocitaMax;

        public void mostraTarga() {           // condiviso
            System.out.println(targa);
        }

        public abstract String descrivi();    // ognuno lo fa a modo suo
    }

    class Auto extends Veicolo { ... }
    class Moto extends Veicolo { ... }
    ```

=== "Interfaccia ✔"

    ```java
    // Ha senso: Stampabile non ha stato — è solo una capacità
    interface Stampabile {
        void stampa();
    }

    // Classi non correlate possono tutte "essere stampabili"
    class Fattura    implements Stampabile { ... }
    class Foto       implements Stampabile { ... }
    class Documento  implements Stampabile { ... }
    ```

---

## Regola pratica

> Se condividi **codice e stato** → classe astratta.
> Se definisci una **capacità** trasversale tra classi non correlate → interfaccia.

!!! warning "Ereditarietà singola"
    Una classe può estendere **una sola** classe astratta. Se hai bisogno di più fonti usa le interfacce — magari insieme a una classe astratta.

---

[:octicons-arrow-right-24: Prossima sezione: Interfacce](../04-interfacce/teoria.md)
