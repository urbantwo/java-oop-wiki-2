# Polimorfismo

## Cos'è il polimorfismo?

Il **polimorfismo** (dal greco: "molte forme") è la capacità di un riferimento di tipo base di puntare a oggetti di tipi diversi, ognuno con il proprio comportamento.

In pratica: lo stesso codice funziona con oggetti diversi **senza sapere il loro tipo esatto**.

---

## Esempio base

```java
abstract class Animale {
    public abstract String parla();
}

class Cane  extends Animale {
    public String parla() { return "Bau!";  }
}
class Gatto extends Animale {
    public String parla() { return "Miao!"; }
}
class Mucca extends Animale {
    public String parla() { return "Muuu!"; }
}
```

```java
// Array di tipo Animale — contiene oggetti diversi
Animale[] zoo = {
    new Cane(),
    new Gatto(),
    new Mucca(),
    new Cane()
};

// Lo stesso codice funziona per tutti
for (Animale a : zoo) {
    System.out.println(a.parla()); // (1)
}
// Output:
// Bau!
// Miao!
// Muuu!
// Bau!
```

1. Java decide **a runtime** quale versione di `parla()` chiamare in base al tipo reale dell'oggetto.

---

## Polimorfismo con le interfacce

```java
interface Stampabile {
    void stampa();
}

class Fattura   implements Stampabile {
    public void stampa() { System.out.println("[FATTURA]  ..."); }
}
class Contratto implements Stampabile {
    public void stampa() { System.out.println("[CONTRATTO] ..."); }
}

// Stesso codice per oggetti completamente diversi
List<Stampabile> documenti = List.of(new Fattura(), new Contratto());
for (Stampabile doc : documenti) {
    doc.stampa();   // il tipo esatto non ci interessa
}
```

---

## Perché è potente?

Senza polimorfismo dovresti scrivere:

```java
// ❌ Senza polimorfismo — fragile e ripetitivo
if (a instanceof Cane)  ((Cane)  a).parla();
if (a instanceof Gatto) ((Gatto) a).parla();
if (a instanceof Mucca) ((Mucca) a).parla();
// ... e ogni volta che aggiungi un animale devi modificare questo codice
```

Con il polimorfismo:

```java
// ✅ Con polimorfismo — robusto ed estendibile
a.parla();  // funziona per qualsiasi Animale, ora e in futuro
```

!!! success "Principio chiave"
    Scrivi codice che parla con il **tipo base** (superclasse o interfaccia). Quando aggiungi nuove classi, il codice esistente funziona senza modifiche.

---

[:octicons-arrow-right-24: Vai agli esercizi](../05-esercizi/ex1.md)
