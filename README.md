# OOP in Java — Wiki

Wiki didattica su Classi, Ereditarietà, Classi Astratte e Interfacce in Java.
Costruita con [MkDocs](https://www.mkdocs.org/) + [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

## Avvio rapido

### 1. Installa le dipendenze

```bash
pip install mkdocs-material
```

### 2. Avvia il server locale

```bash
mkdocs serve
```

Apri il browser su **http://127.0.0.1:8000** — si aggiorna in automatico quando modifichi i file.

### 3. Build del sito statico

```bash
mkdocs build
```

Genera la cartella `site/` con l'HTML statico pronto per essere pubblicato.

---

## Pubblicare su GitHub Pages

### Metodo automatico (consigliato)

```bash
mkdocs gh-deploy
```

Questo comando:
1. Builda il sito
2. Fa push del risultato sul branch `gh-pages`
3. GitHub Pages lo pubblica automaticamente

Il sito sarà disponibile su `https://tuonome.github.io/java-oop-wiki`.

### Prima di pubblicare

1. Crea il repository su GitHub
2. Fai il primo push del codice sorgente:
   ```bash
   git init
   git add .
   git commit -m "prima versione wiki OOP Java"
   git remote add origin https://github.com/tuonome/java-oop-wiki.git
   git push -u origin main
   ```
3. Poi esegui `mkdocs gh-deploy`
4. Vai su **Settings → Pages** del repository e verifica che GitHub Pages sia abilitato sul branch `gh-pages`

### Aggiornare il sito

Ogni volta che modifichi i contenuti:

```bash
mkdocs gh-deploy
```

---

## Struttura del progetto

```
java-oop-wiki/
├── mkdocs.yml              # configurazione principale
├── README.md               # questo file
└── docs/
    ├── index.md            # home page
    ├── riepilogo.md        # riepilogo finale
    ├── 01-classi/
    │   ├── teoria.md
    │   └── esempi.md
    ├── 02-ereditarieta/
    │   ├── teoria.md
    │   └── override.md
    ├── 03-astratte/
    │   ├── teoria.md
    │   └── quando.md
    ├── 04-interfacce/
    │   ├── teoria.md
    │   ├── confronto.md
    │   └── polimorfismo.md
    └── 05-esercizi/
        ├── ex1.md
        ├── ex2.md
        └── ex3.md
```

## Aggiungere contenuti

Aggiungi un file `.md` nella cartella `docs/` e registralo in `mkdocs.yml` sotto la sezione `nav:`.
