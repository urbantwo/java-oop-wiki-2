# 📚 Esercizio Guidato — Sistema di Gestione Biblioteca

!!! info "Obiettivo"
    Costruirai un sistema di gestione per una biblioteca **da zero**, step dopo step.
    Ogni fase introduce un nuovo problema reale, e imparerai **perché** esistono certi strumenti Java — non solo come usarli.

    **Tempo stimato:** 60–90 minuti  
    **Modalità:** esercizio guidato in aula

---

## 🗺️ Panoramica del percorso

| Step | Argomento | Cosa introduce |
|------|-----------|----------------|
| 1 | Variabili e tipi | Rappresentare un libro con dati |
| 2 | Array | Gestire più libri, e i loro limiti |
| 3 | Classi e ArrayList | Strutturare i dati, usare collections |
| 4 | Enum | Categorizzare con sicurezza |
| 5 | Classe astratta | Condividere struttura tra tipi diversi |
| 6 | Interfacce | Definire contratti e comportamenti |
| 7 | Integrazione | Un sistema funzionante completo |

---

## Step 1 — Il primo libro

!!! question "Il problema"
    La biblioteca vuole tenere traccia di un libro. Come lo rappresentiamo nel codice?

### Concetti coinvolti

`variabili` · `tipi primitivi` · `String` · `boolean` · `System.out.println`

---

### 📋 Compiti

**1.1 — Dichiara le variabili**

In una classe `Main`, dichiara le seguenti variabili per rappresentare un libro:

| Variabile | Tipo | Descrizione |
|-----------|------|-------------|
| `titolo` | `String` | Titolo del libro |
| `autore` | `String` | Nome dell'autore |
| `isbn` | `String` | Codice identificativo univoco |
| `annoPubblicazione` | `int` | Anno di pubblicazione |
| `numeroPagine` | `int` | Numero di pagine |
| `prezzo` | `double` | Prezzo di copertina |
| `disponibile` | `boolean` | Se è disponibile per il prestito |

**1.2 — Assegna i valori**

Assegna questi valori al libro:

- Titolo: `"Il Nome della Rosa"`
- Autore: `"Umberto Eco"`
- ISBN: `"978-8845292613"`
- Anno: `1980`
- Pagine: `502`
- Prezzo: `12.50`
- Disponibile: `true`

**1.3 — Stampa la scheda**

Stampa a console una scheda formattata così:

```
=============================
📚 Il Nome della Rosa
   Autore: Umberto Eco
   ISBN:   978-8845292613
   Anno:   1980
   Pagine: 502
   Prezzo: €12.50
   Stato:  ✅ Disponibile
=============================
```

!!! tip "Suggerimento"
    Per `disponibile`, usa un operatore ternario per stampare `"✅ Disponibile"` oppure `"❌ Non disponibile"`:
    ```java
    String stato = disponibile ? "✅ Disponibile" : "❌ Non disponibile";
    ```

**1.4 — Operazioni sui dati**

- Calcola e stampa quanti anni fa è stato pubblicato il libro (usa l'anno `2025`).
- Calcola il prezzo con IVA al 4% (libri: aliquota ridotta) e stampalo.
- Simula un prestito: imposta `disponibile = false` e ristampa lo stato.

---

??? success "Risultato atteso"
    Il programma stampa la scheda, poi mostra l'età del libro, il prezzo con IVA, e infine lo stato aggiornato a "Non disponibile".

---

## Step 2 — Il catalogo con gli Array

!!! question "Il problema"
    Abbiamo un solo libro. Ma la biblioteca ne ha 500. Creare 500 variabili separate è impossibile → servono gli **array**.

### Concetti coinvolti

`array` · `ciclo for` · `for-each` · `Scanner` · `array paralleli e loro limiti`

---

### 📋 Compiti

**2.1 — Crea gli array del catalogo**

```java
String[] titoli   = new String[5];
String[] autori   = new String[5];
String[] isbn     = new String[5];
int[]    anni     = new int[5];
boolean[] disponibili = new boolean[5];
```

Riempi gli array con questi 5 libri:

| # | Titolo | Autore | ISBN | Anno | Disponibile |
|---|--------|--------|------|------|-------------|
| 0 | Il Nome della Rosa | Umberto Eco | 978-8845292613 | 1980 | true |
| 1 | 1984 | George Orwell | 978-8804668237 | 1949 | true |
| 2 | Il Piccolo Principe | Antoine de Saint-Exupéry | 978-8845292614 | 1943 | false |
| 3 | Harry Potter e la Pietra Filosofale | J.K. Rowling | 978-8877827029 | 1997 | true |
| 4 | La Divina Commedia | Dante Alighieri | 978-8804123456 | 1320 | false |

**2.2 — Stampa il catalogo**

Con un ciclo `for` classico, stampa il catalogo numerato:

```
CATALOGO BIBLIOTECA (5 libri)
───────────────────────────────────────
[1] Il Nome della Rosa — Umberto Eco          ✅
[2] 1984 — George Orwell                      ✅
[3] Il Piccolo Principe — A. de Saint-Exupéry ❌
...
```

**2.3 — Statistiche del catalogo**

Scrivi un ciclo che calcoli e stampi:

- Totale libri nel catalogo
- Quanti sono disponibili
- Quanti non sono disponibili
- Percentuale di disponibilità

**2.4 — Cerca per titolo**

Chiedi all'utente di inserire un titolo (o parte di esso) tramite `Scanner`. Cerca negli array e stampa:

- Se trovato: posizione nel catalogo, autore, stato disponibilità
- Se non trovato: `"⚠️ Nessun libro trovato con questo titolo."`

!!! tip "Suggerimento ricerca"
    Usa `titoli[i].toLowerCase().contains(query.toLowerCase())` per una ricerca case-insensitive e parziale.

**2.5 — Filtra i disponibili**

Stampa solo i libri con `disponibili[i] == true`, usando un ciclo con condizione `if`.

---

!!! warning "Riflessione — I limiti degli array"
    Prova a rispondere a queste domande (scrivile come commento nel codice):

    - Cosa succede se vuoi aggiungere un **sesto** libro?
    - Come fai a **rimuovere** un libro dal mezzo dell'array senza lasciare "buchi"?
    - Se dimentichi di aggiornare uno degli array paralleli quando aggiungi un libro, cosa succede?
    
    👉 Questi problemi hanno una soluzione: le **classi** e le **collections**. È quello che faremo nel prossimo step.

---

## Step 3 — La classe `Libro`

!!! question "Il problema"
    Gli array paralleli sono fragili: titoli, autori e disponibilità sono collegati solo per **posizione**, ma niente lo garantisce nel codice. Se sbaglio un indice, il programma non dà errore ma produce dati sbagliati.
    
    Una **classe** raggruppa i dati correlati in un'unica struttura coerente.

### Concetti coinvolti

`class` · `costruttore` · `private` · `getter` · `setter` · `toString()` · `ArrayList` · `for-each`

---

### 📋 Compiti

**3.1 — Crea la classe `Libro`**

Crea un nuovo file `Libro.java`. La classe deve avere questi campi, tutti `private`:

```java
public class Libro {
    private String titolo;
    private String autore;
    private String isbn;
    private int annoPubblicazione;
    private int numeroPagine;
    private double prezzo;
    private boolean disponibile;
    private String presaInCaricoDA; // chi ha il libro in prestito (null se disponibile)
}
```

**3.2 — Costruttore**

Aggiungi un costruttore che riceve tutti i parametri **tranne** `disponibile` e `presaInCaricoDA`:
un libro appena aggiunto alla biblioteca è sempre disponibile, e nessuno lo ha in prestito.

```java
public Libro(String titolo, String autore, String isbn, int annoPubblicazione, int numeroPagine, double prezzo) {
    // ...
    this.disponibile = true;
    this.presaInCaricoDA = null;
}
```

**3.3 — Getter e Setter**

Aggiungi i getter per tutti i campi. Per i setter, rifletti su questi:

- `setTitolo()` — ha senso? Il titolo di un libro cambia mai?
- `setDisponibile()` — ha senso? O meglio creare metodi più specifici?
- `setIsbn()` — ha senso? L'ISBN è un identificatore univoco permanente.

!!! tip "Buona pratica"
    Invece di un generico `setDisponibile(boolean)`, crea due metodi con nomi più significativi:
    ```java
    public void prendiInPrestito(String nomeUtente) { ... }
    public void restituisci() { ... }
    ```
    Il codice diventa più leggibile: si capisce l'**intenzione**, non solo l'operazione.

**3.4 — Metodo `prendiInPrestito(String nomeUtente)`**

Implementa la logica di prestito:

- Se il libro **non è disponibile**: stampa un messaggio di errore e non fare nulla
- Se il libro **è disponibile**: segna come non disponibile, salva il nome dell'utente

**3.5 — Metodo `restituisci()`**

- Segna il libro come disponibile
- Azzera `presaInCaricoDA`
- Stampa un messaggio di conferma

**3.6 — Override di `toString()`**

```java
@Override
public String toString() {
    // restituisce una stringa formattata con tutte le info del libro
}
```

Deve produrre qualcosa del tipo:
```
📚 "Il Nome della Rosa" — Umberto Eco (1980)
   ISBN: 978-8845292613 | 502 pag. | €12.50
   Stato: ✅ Disponibile
```

**3.7 — Metodo `getEtaLibro()`**

Aggiungi un metodo che calcola e restituisce quanti anni ha il libro.

**3.8 — Sostituisci gli array con `ArrayList<Libro>`**

Nel `Main`, crea un `ArrayList<Libro>`, aggiungi i 5 libri dello Step 2 e stampa il catalogo con un for-each chiamando `toString()` su ogni libro.

**3.9 — Ricerca e filtraggio**

Riscrivi la ricerca dello Step 2 usando la lista di oggetti `Libro`.
Aggiungi anche:

- Un metodo `cercaPerIsbn(String isbn)` che restituisce il libro trovato (o `null`)
- Un metodo `filtraDisponibili()` che stampa solo i libri disponibili

---

??? example "Come usare ArrayList"
    ```java
    import java.util.ArrayList;

    ArrayList<Libro> catalogo = new ArrayList<>();
    catalogo.add(new Libro("Il Nome della Rosa", "Umberto Eco", "978-...", 1980, 502, 12.50));

    for (Libro libro : catalogo) {
        System.out.println(libro); // chiama toString() automaticamente
    }

    System.out.println("Totale libri: " + catalogo.size());
    ```

---

## Step 4 — Categorizzare con `enum`

!!! question "Il problema"
    La biblioteca non ha solo libri: ci sono anche riviste e DVD. Come distinguiamo i tipi di materiale in modo **sicuro** e **leggibile**?
    
    Con una `String` potremmo scrivere `"libro"`, `"Libro"`, `"LIBRO"`, `"libros"` — tutti diversi, tutti sbagliati silenziosamente.
    Con un `int` (0 = libro, 1 = rivista...) il codice diventa incomprensibile.
    
    → L'**enum** definisce un insieme chiuso di valori validi.

### Concetti coinvolti

`enum` · `campi nell'enum` · `costruttore enum` · `metodi nell'enum` · `switch`

---

### 📋 Compiti

**4.1 — Crea l'enum `TipoMateriale`**

```java
public enum TipoMateriale {
    LIBRO,
    RIVISTA,
    DVD
}
```

**4.2 — Aggiungi campi e costruttore**

Ogni tipo ha una descrizione leggibile e un numero massimo di giorni di prestito:

```java
public enum TipoMateriale {
    LIBRO("Libro cartaceo", 30),
    RIVISTA("Rivista periodica", 7),
    DVD("Disco video digitale", 14);

    private final String descrizione;
    private final int giorniPrestito;

    TipoMateriale(String descrizione, int giorniPrestito) {
        this.descrizione = descrizione;
        this.giorniPrestito = giorniPrestito;
    }

    public String getDescrizione() { return descrizione; }
    public int getGiorniPrestito() { return giorniPrestito; }
}
```

**4.3 — Aggiungi un metodo all'enum**

Aggiungi il metodo `String getIcona()` che restituisce:

- `"📚"` per LIBRO
- `"📰"` per RIVISTA
- `"💿"` per DVD

Usa uno `switch` dentro l'enum.

**4.4 — Aggiungi `TipoMateriale` alla classe `Libro`**

- Aggiungi il campo `private TipoMateriale tipo;` alla classe `Libro`
- Aggiornare il costruttore per riceverlo
- Aggiorna `toString()` per mostrare tipo e icona

**4.5 — Usa le informazioni del tipo**

Aggiorna `prendiInPrestito()` per stampare la data di scadenza del prestito:

```
✅ "Il Nome della Rosa" preso in prestito da Mario Rossi
   Scadenza: entro 30 giorni (tipo: Libro cartaceo)
```

**4.6 — Statistiche per tipo**

Scrivi un metodo che conti quanti materiali ci sono per ogni tipo e stampi:

```
📊 Statistiche catalogo:
   📚 Libri:   3
   📰 Riviste: 1
   💿 DVD:     2
```

!!! tip "Iterare sui valori di un enum"
    ```java
    for (TipoMateriale tipo : TipoMateriale.values()) {
        // tipo assume LIBRO, poi RIVISTA, poi DVD
    }
    ```

---

## Step 5 — La classe astratta `MaterialeBiblioteca`

!!! question "Il problema"
    Adesso vogliamo aggiungere `Dvd` e `Rivista` come classi separate, perché hanno campi diversi (un DVD ha `regia` e `durata`, una rivista ha `numeroEdizione`).
    
    Ma tutti i materiali condividono: titolo, disponibilità, tipo, la logica di prestito...
    
    Duplicare tutto questo codice in ogni classe è un errore: se domani cambia la logica del prestito, dobbiamo aggiornare 3 classi invece di 1.
    
    → La **classe astratta** contiene la parte comune, e lascia ai figli solo ciò che è specifico.

### Concetti coinvolti

`abstract class` · `extends` · `metodo astratto` · `super()` · `@Override` · `polimorfismo`

---

### 📋 Compiti

**5.1 — Crea la classe astratta `MaterialeBiblioteca`**

```java
public abstract class MaterialeBiblioteca {

    private String titolo;
    private TipoMateriale tipo;
    private boolean disponibile;
    private String presaInCaricoDA;

    public MaterialeBiblioteca(String titolo, TipoMateriale tipo) {
        this.titolo = titolo;
        this.tipo = tipo;
        this.disponibile = true;
        this.presaInCaricoDA = null;
    }

    // Metodo astratto: ogni sottoclasse lo implementa a modo suo
    public abstract String getScheda();

    // Metodo concreto: la logica di prestito è uguale per tutti
    public boolean prendiInPrestito(String nomeUtente) {
        if (!disponibile) {
            System.out.println("❌ Materiale non disponibile (in prestito a: " + presaInCaricoDA + ")");
            return false;
        }
        disponibile = false;
        presaInCaricoDA = nomeUtente;
        System.out.println("✅ \"" + titolo + "\" preso in prestito da " + nomeUtente
            + " — scadenza: " + tipo.getGiorniPrestito() + " giorni");
        return true;
    }

    public void restituisci() {
        System.out.println("↩️  \"" + titolo + "\" restituito da " + presaInCaricoDA);
        disponibile = true;
        presaInCaricoDA = null;
    }

    // getter
    public String getTitolo() { return titolo; }
    public TipoMateriale getTipo() { return tipo; }
    public boolean isDisponibile() { return disponibile; }
    public String getPresaInCaricoDA() { return presaInCaricoDA; }

    @Override
    public String toString() {
        return getScheda();
    }
}
```

**5.2 — Fai estendere `Libro` da `MaterialeBiblioteca`**

`Libro` ora **estende** `MaterialeBiblioteca`. Mantiene i suoi campi specifici (`autore`, `isbn`, `numeroPagine`, `prezzo`) ma non riduplica quelli comuni.

```java
public class Libro extends MaterialeBiblioteca {

    private String autore;
    private String isbn;
    private int numeroPagine;
    private double prezzo;

    public Libro(String titolo, String autore, String isbn,
                 int annoPubblicazione, int numeroPagine, double prezzo) {
        super(titolo, TipoMateriale.LIBRO); // chiama il costruttore della classe madre
        this.autore = autore;
        this.isbn = isbn;
        this.numeroPagine = numeroPagine;
        this.prezzo = prezzo;
    }

    @Override
    public String getScheda() {
        return getTipo().getIcona() + " \"" + getTitolo() + "\" — " + autore
            + "\n   ISBN: " + isbn + " | " + numeroPagine + " pag. | €" + prezzo
            + "\n   Stato: " + (isDisponibile() ? "✅ Disponibile" : "❌ In prestito a " + getPresaInCaricoDA());
    }

    // getter specifici
    public String getAutore() { return autore; }
    public String getIsbn() { return isbn; }
    public int getNumeroPagine() { return numeroPagine; }
    public double getPrezzo() { return prezzo; }
}
```

**5.3 — Crea la classe `Dvd`**

La classe `Dvd` estende `MaterialeBiblioteca` e aggiunge:

| Campo | Tipo | Descrizione |
|-------|------|-------------|
| `regia` | `String` | Nome del regista |
| `durataminuti` | `int` | Durata in minuti |
| `annoProduzione` | `int` | Anno di produzione |

Implementa `getScheda()` in modo appropriato:

```
💿 "Parasite" — regia di Bong Joon-ho (2019)
   Durata: 132 min
   Stato: ✅ Disponibile
```

**5.4 — Crea la classe `Rivista`**

La classe `Rivista` estende `MaterialeBiblioteca` e aggiunge:

| Campo | Tipo | Descrizione |
|-------|------|-------------|
| `editore` | `String` | Casa editrice |
| `numeroEdizione` | `int` | Numero dell'edizione |
| `meseAnno` | `String` | Es. "Marzo 2025" |

**5.5 — Il potere del polimorfismo**

Nel `Main`, crea un `ArrayList<MaterialeBiblioteca>` che contiene libri, DVD e riviste insieme.
Stampa tutto il catalogo con un unico for-each:

```java
ArrayList<MaterialeBiblioteca> catalogo = new ArrayList<>();
catalogo.add(new Libro(...));
catalogo.add(new Dvd(...));
catalogo.add(new Rivista(...));

for (MaterialeBiblioteca materiale : catalogo) {
    System.out.println(materiale.getScheda()); // polimorfismo!
    System.out.println("---");
}
```

!!! warning "Domanda di riflessione"
    Perché `getScheda()` è **astratto** in `MaterialeBiblioteca` e non ha un'implementazione di default?
    Cosa succederebbe se provassi a creare un oggetto `new MaterialeBiblioteca(...)` direttamente?

---

## Step 6 — Interfacce

!!! question "Il problema"
    Abbiamo la logica di prestito nella classe astratta. Ma cosa succede se in futuro vogliamo aggiungere materiali che **non si prestano** (es. enciclopedie di consultazione in sede)?
    O materiali che si **ricercano** in modi diversi?
    
    Le interfacce definiscono **capacità** (cosa sa fare un oggetto) separate dall'**identità** (cosa è un oggetto).
    Una classe può implementare più interfacce → può avere più capacità.

### Concetti coinvolti

`interface` · `implements` · `default method` · `instanceof` · tipo come contratto

---

### 📋 Compiti

**6.1 — Interfaccia `Ricercabile`**

```java
public interface Ricercabile {
    
    /**
     * Restituisce true se questo materiale corrisponde alla query di ricerca.
     * La ricerca deve essere case-insensitive e parziale.
     */
    boolean corrispondeA(String query);

    /**
     * Restituisce le parole chiave associate al materiale (per la ricerca avanzata).
     */
    String[] getParoleChiave();
}
```

Implementa `Ricercabile` in tutte e tre le classi (`Libro`, `Dvd`, `Rivista`):

- `Libro`: cerca per titolo, autore, ISBN
- `Dvd`: cerca per titolo, regia
- `Rivista`: cerca per titolo, editore, meseAnno

**6.2 — Interfaccia `Stampabile`**

```java
public interface Stampabile {
    
    void stampaScheda();

    // default method: implementazione di default, le classi possono sovrascriverla
    default void stampaSeparatore() {
        System.out.println("─".repeat(50));
    }
}
```

Implementa `Stampabile` in tutte le classi. Il metodo `stampaScheda()` deve stampare `getScheda()` con separatori.

**6.3 — Aggiorna le dichiarazioni di classe**

```java
public class Libro extends MaterialeBiblioteca implements Ricercabile, Stampabile {
    // ...
}
```

**6.4 — Metodo di ricerca nel catalogo**

Scrivi un metodo `cerca(ArrayList<MaterialeBiblioteca> catalogo, String query)` che:

1. Itera sul catalogo
2. Per ogni elemento, verifica se implementa `Ricercabile` (con `instanceof`)
3. Se sì, chiama `corrispondeA(query)`
4. Raccoglie e restituisce i risultati in una nuova lista

```java
public static ArrayList<MaterialeBiblioteca> cerca(
        ArrayList<MaterialeBiblioteca> catalogo, String query) {

    ArrayList<MaterialeBiblioteca> risultati = new ArrayList<>();

    for (MaterialeBiblioteca m : catalogo) {
        if (m instanceof Ricercabile) {
            Ricercabile r = (Ricercabile) m;
            if (r.corrispondeA(query)) {
                risultati.add(m);
            }
        }
    }

    return risultati;
}
```

**6.5 — Usa `Stampabile` per la stampa**

Scrivi un metodo `stampaCatalogo(ArrayList<MaterialeBiblioteca> catalogo)` che:

- Stampa un'intestazione con il totale
- Per ogni elemento che implementa `Stampabile`, chiama `stampaScheda()` e `stampaSeparatore()`

**6.6 — Domanda di riflessione**

!!! question "Interfaccia vs Classe Astratta"
    Discuti con il docente:

    - `MaterialeBiblioteca` è una classe **astratta**: perché non un'interfaccia?
    - `Ricercabile` è un'**interfaccia**: perché non una classe astratta?
    - Cosa cambierebbe se `prendiInPrestito()` fosse in un'interfaccia?

---

## Step 7 — Il sistema completo: classe `Biblioteca`

!!! question "Il problema"
    Tutti i pezzi ci sono. È ora di assemblarli in un sistema coerente con una classe che gestisce l'intera biblioteca.

### Concetti coinvolti

`HashMap` · `ArrayList` · `metodi di istanza` · progettazione OOP · `main` completo

---

### 📋 Compiti

**7.1 — Crea la classe `Biblioteca`**

```java
import java.util.ArrayList;
import java.util.HashMap;

public class Biblioteca {

    private String nome;
    private ArrayList<MaterialeBiblioteca> catalogo;
    private HashMap<String, ArrayList<MaterialeBiblioteca>> prestitiPerUtente;

    public Biblioteca(String nome) {
        this.nome = nome;
        this.catalogo = new ArrayList<>();
        this.prestitiPerUtente = new HashMap<>();
    }
}
```

**7.2 — Metodo `aggiungiMateriale()`**

```java
public void aggiungiMateriale(MaterialeBiblioteca materiale) {
    catalogo.add(materiale);
    System.out.println("➕ Aggiunto: " + materiale.getTitolo());
}
```

**7.3 — Metodo `stampaCatalogo()`**

Stampa tutto il catalogo con intestazione, totale e divisori tra un materiale e l'altro. Usa `getScheda()`.

**7.4 — Metodo `cerca(String query)`**

Usa la logica dell'interfaccia `Ricercabile` sviluppata nello Step 6. Stampa i risultati o un messaggio se non trovati.

**7.5 — Metodo `prestaMateriale(String isbn, String nomeUtente)`**

- Cerca il materiale per ISBN nel catalogo
- Se non trovato: messaggio di errore
- Se trovato: chiama `prendiInPrestito(nomeUtente)`
- Aggiorna la `HashMap` dei prestiti per utente:
    - Se l'utente non ha ancora prestiti, crea una nuova lista
    - Aggiungi il materiale alla lista dell'utente

```java
public void prestaMateriale(String isbn, String nomeUtente) {
    // trova il materiale
    MaterialeBiblioteca trovato = null;
    for (MaterialeBiblioteca m : catalogo) {
        if (m instanceof Libro && ((Libro) m).getIsbn().equals(isbn)) {
            trovato = m;
            break;
        }
    }

    if (trovato == null) {
        System.out.println("⚠️ Materiale con ISBN " + isbn + " non trovato.");
        return;
    }

    boolean successo = trovato.prendiInPrestito(nomeUtente);
    
    if (successo) {
        prestitiPerUtente.putIfAbsent(nomeUtente, new ArrayList<>());
        prestitiPerUtente.get(nomeUtente).add(trovato);
    }
}
```

**7.6 — Metodo `riceviRestituzione(String isbn)`**

- Trova il materiale per ISBN
- Chiama `restituisci()`
- Rimuovi il materiale dalla lista prestiti dell'utente nella HashMap

**7.7 — Metodo `stampaStatistiche()`**

Stampa un report completo:

```
╔══════════════════════════════════════╗
║    📊 STATISTICHE — Biblioteca X     ║
╠══════════════════════════════════════╣
║  Totale materiali:  8                ║
║  Disponibili:       5  (62.5%)       ║
║  In prestito:       3  (37.5%)       ║
╠══════════════════════════════════════╣
║  Per tipo:                           ║
║    📚 Libri:        4                ║
║    📰 Riviste:      2                ║
║    💿 DVD:          2                ║
╠══════════════════════════════════════╣
║  Utenti con prestiti attivi:   2     ║
║    • Mario Rossi     → 2 materiali   ║
║    • Anna Bianchi    → 1 materiale   ║
╚══════════════════════════════════════╝
```

!!! tip "Iterare su una HashMap"
    ```java
    for (String utente : prestitiPerUtente.keySet()) {
        ArrayList<MaterialeBiblioteca> prestiti = prestitiPerUtente.get(utente);
        System.out.println("• " + utente + " → " + prestiti.size() + " materiali");
    }
    ```

**7.8 — Metodo `getMaterialeUtente(String nomeUtente)`**

Restituisce la lista di materiali attualmente in prestito a un utente (o una lista vuota se non ne ha).

**7.9 — Il `main` completo**

Scrivi una sessione simulata che dimostri tutto il sistema:

```java
public static void main(String[] args) {

    Biblioteca biblioteca = new Biblioteca("Biblioteca Civica di Milano");

    // 1. Aggiungi materiali
    biblioteca.aggiungiMateriale(new Libro("Il Nome della Rosa", "Umberto Eco",
        "978-8845292613", 1980, 502, 12.50));
    biblioteca.aggiungiMateriale(new Libro("1984", "George Orwell",
        "978-8804668237", 1949, 328, 9.90));
    biblioteca.aggiungiMateriale(new Dvd("Parasite", "Bong Joon-ho", 132, 2019));
    biblioteca.aggiungiMateriale(new Rivista("Le Scienze", "Springer Nature", 420, "Aprile 2025"));
    // aggiungi altri 2 a piacere

    // 2. Stampa il catalogo iniziale
    System.out.println("\n" + "=".repeat(50));
    biblioteca.stampaCatalogo();

    // 3. Esegui prestiti
    System.out.println("\n--- PRESTITI ---");
    biblioteca.prestaMateriale("978-8845292613", "Mario Rossi");
    biblioteca.prestaMateriale("978-8804668237", "Mario Rossi");
    biblioteca.prestaMateriale("978-8804668237", "Anna Bianchi"); // già in prestito!

    // 4. Cerca nel catalogo
    System.out.println("\n--- RICERCA ---");
    biblioteca.cerca("orwell");

    // 5. Statistiche
    System.out.println("\n--- STATISTICHE ---");
    biblioteca.stampaStatistiche();

    // 6. Restituzione
    System.out.println("\n--- RESTITUZIONE ---");
    biblioteca.riceviRestituzione("978-8845292613");

    // 7. Statistiche aggiornate
    System.out.println("\n--- STATISTICHE AGGIORNATE ---");
    biblioteca.stampaStatistiche();
}
```

---

## ⭐ Bonus — Per chi finisce prima

!!! tip "Bonus 1 — Classe `Utente`"
    Crea la classe `Utente` con:

    - `nome`, `cognome`, `email` (String)
    - `maxPrestiti` (int, default 3)
    - `prestitiAttivi` (ArrayList di materiali)
    
    Aggiungi il metodo `boolean puoPrendereInPrestito()` che controlla se ha raggiunto il limite.
    Aggiorna `Biblioteca` per usare `HashMap<Utente, ArrayList<MaterialeBiblioteca>>`.

!!! tip "Bonus 2 — Ordinamento"
    Aggiungi un metodo `ordinaPerTitolo()` che ordina il catalogo alfabeticamente usando `Collections.sort()` e implementa `Comparable<MaterialeBiblioteca>` nella classe astratta.

!!! tip "Bonus 3 — Storico prestiti"
    Crea una classe `RecordPrestito` con: materiale, utente, dataInizio, dataFine (usa `String` per semplicità). Mantieni uno storico completo in `Biblioteca` oltre ai prestiti attivi.

---

## 📋 Criteri di valutazione

| Step completato | Valutazione |
|-----------------|-------------|
| Step 1–2 | ☆☆ — Sufficiente: basi e strutture elementari |
| Step 3–4 | ★☆ — Buono: sa strutturare dati con OOP |
| Step 5 | ★★ — Ottimo: comprende ereditarietà e polimorfismo |
| Step 6 | ★★+ — Molto ottimo: sa usare interfacce come contratti |
| Step 7 | ★★★ — Eccellente: sa integrare tutti i concetti |
| Bonus | 🏆 — Eccellente con iniziativa |

### Requisiti trasversali

- [ ] Il codice **compila ed esegue** senza errori
- [ ] I nomi di classi, metodi e variabili sono **significativi e consistenti**
- [ ] Ogni file `.java` ha il nome uguale alla classe pubblica
- [ ] I campi sono `private` con getter/setter dove appropriato
- [ ] Almeno un commento `// Scelta di design: ...` per ogni classe creata

---

!!! quote "Ricorda"
    L'obiettivo non è arrivare al Step 7 il prima possibile.
    È capire **perché** ogni nuovo strumento risolve un problema che il precedente non poteva risolvere.
