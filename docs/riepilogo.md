# Riepilogo

## Mappa dei concetti

```
OOP in Java
│
├── Classe                   → blueprint, new, this
│   ├── Campi               → stato dell'oggetto
│   ├── Costruttore         → inizializzazione
│   └── Metodi              → comportamento
│
├── Ereditarietà (extends)
│   ├── Sottoclasse         → eredita + aggiunge
│   ├── super()             → costruttore genitore
│   └── @Override           → ridefinisce un metodo
│
├── Classe Astratta (abstract)
│   ├── Non istanziabile    → new vietato
│   ├── Metodi astratti     → obbligatori per le figlie
│   └── Metodi concreti     → condivisi da tutte
│
├── Interfaccia (interface / implements)
│   ├── Solo contratto      → nessuno stato
│   ├── Ereditarietà multipla → implements A, B, C
│   └── default (Java 8+)  → implementazione opzionale
│
└── Polimorfismo
    └── Tipo base → comportamento del tipo reale a runtime
```

---

## Tabella comparativa completa

| | Classe normale | Classe astratta | Interfaccia |
|---|---|---|---|
| `new` | ✅ | ❌ | ❌ |
| Campi di stato | ✅ | ✅ | ❌ (solo `final`) |
| Costruttore | ✅ | ✅ | ❌ |
| Metodi concreti | ✅ | ✅ | ✅ (`default`) |
| Metodi astratti | ❌ | ✅ | ✅ (tutti) |
| Ereditarietà | singola | singola | **multipla** |
| Parola chiave | — | `extends` | `implements` |

---

## Quando usare cosa?

!!! success "Classe normale"
    Quando l'oggetto ha senso da solo e non ha bisogno di essere esteso.

!!! warning "Classe astratta"
    Quando un gruppo di classi condivide **stato e comportamento** di base, ma ognuna specializza qualcosa.

!!! info "Interfaccia"
    Quando vuoi definire una **capacità** che può essere aggiunta a classi non correlate, o quando hai bisogno di ereditarietà multipla.


---

## Checklist finale

- [ ] So cos'è una classe e come creare un oggetto con `new`
- [ ] Capisco la differenza tra campi, costruttori e metodi
- [ ] So usare `extends` per ereditare da un'altra classe
- [ ] So usare `@Override` e `super` correttamente
- [ ] Capisco cos'è una classe astratta e quando usarla
- [ ] So definire e implementare un'interfaccia
- [ ] Capisco il polimorfismo e so usarlo con array di tipo base
