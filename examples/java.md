# Brain-Freeze — Java Examples

Questi esempi coprono tre concetti fondamentali di Java: **generics**, **streams e lambda**, e **pattern Observer**.

---

## Esempio 1 — Generics: stack generico

Obiettivo: implementare una classe `Stack<T>` con metodi `push`, `pop` e `isEmpty`, usando una `ArrayList` interna.

### 🟢 Easy

```java
import java.util.ArrayList;

public class Stack<T> {
    private ArrayList<T> elementi = new ArrayList<>();

    // TOCCA A TE: aggiungi `elemento` in coda alla lista
    // con il metodo add() di ArrayList
    public void push(T elemento) {

    }

    // TOCCA A TE: rimuovi e ritorna l'ultimo elemento della lista
    // con remove(elementi.size() - 1)
    public T pop() {

    }

    // TOCCA A TE: ritorna true se la lista non contiene elementi
    // con il metodo isEmpty() di ArrayList
    public boolean isEmpty() {

    }
}
```

**Cosa devi completare:**

1. **push**: L'hint ti dice già il metodo da usare e dove aggiungere l'elemento.
2. **pop**: `remove(index)` rimuove l'elemento all'indice dato e lo ritorna. L'ultimo indice valido è `size() - 1`.
3. **isEmpty**: `ArrayList` ha già un metodo `isEmpty()` — delegaci direttamente.

---

### 🟡 Medium

```java
import java.util.ArrayList;

public class Stack<T> {
    private ArrayList<T> elementi = new ArrayList<>();

    // TOCCA A TE: inserisci un elemento in cima allo stack
    public void push(T elemento) {

    }

    // TOCCA A TE: rimuovi e ritorna l'elemento in cima allo stack
    public T pop() {

    }

    // TOCCA A TE: indica se lo stack è vuoto
    public boolean isEmpty() {

    }
}
```

**Cosa devi completare:**

1. **push**: Uno stack è LIFO — l'ultimo entrato è il primo a uscire. Come modelli questo con una lista?
2. **pop**: Devi sia rimuovere che ritornare l'elemento. `ArrayList` ha metodi per entrambe le operazioni — ce n'è uno che fa entrambe le cose insieme?
3. **isEmpty**: Una sola riga. Pensa a cosa significa "stack vuoto" in termini della lista interna.

---

### 🔴 Hard

```java
import java.util.ArrayList;

public class Stack<T> {
    private ArrayList<T> elementi = new ArrayList<>();

    // TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
    public void push(T elemento) { }

    public T pop() { }

    public boolean isEmpty() { }
}
```

**Cosa devi completare:**

1. **Logica completa** — Generics, LIFO, delegazione a `ArrayList`.

---

## Esempio 2 — Streams e Lambda: filtraggio e trasformazione

Obiettivo: data una lista di stringhe, restituire una lista con solo quelle che iniziano per lettera maiuscola, convertite in minuscolo e ordinate alfabeticamente.

Input: `["Banana", "mela", "Arancia", "kiwi", "Limone"]`
Output atteso: `["arancia", "banana", "limone"]`

### 🟢 Easy

```java
import java.util.List;
import java.util.stream.Collectors;

public List<String> filtraETrasforma(List<String> parole) {
    return parole.stream()
        // TOCCA A TE: usa .filter() con Character.isUpperCase(s.charAt(0))
        // per tenere solo le stringhe che iniziano con maiuscola

        // TOCCA A TE: usa .map() con String::toLowerCase
        // per convertire ogni stringa in minuscolo

        // TOCCA A TE: usa .sorted() per ordinare alfabeticamente

        .collect(Collectors.toList());
}
```

**Cosa devi completare:**

1. **filter**: L'hint ti dà già la condizione esatta da passare alla lambda.
2. **map**: `String::toLowerCase` è un method reference — passalo direttamente a `map()`.
3. **sorted**: `.sorted()` senza argomenti usa l'ordine naturale (alfabetico per stringhe).

---

### 🟡 Medium

```java
import java.util.List;
import java.util.stream.Collectors;

public List<String> filtraETrasforma(List<String> parole) {
    return parole.stream()
        // TOCCA A TE: escludi le parole che non iniziano con la maiuscola

        // TOCCA A TE: trasforma ogni parola in minuscolo

        // TOCCA A TE: ordina il risultato alfabeticamente

        .collect(Collectors.toList());
}
```

**Cosa devi completare:**

1. **filter**: Riceve una lambda `stringa -> condizione`. Come controlli il primo carattere di una stringa in Java?
2. **map**: Trasforma ogni elemento dello stream in qualcos'altro. `String` ha già un metodo per la conversione in minuscolo.
3. **sorted**: Lo stream può essere ordinato prima della raccolta. Qual è il metodo più semplice per farlo?

---

### 🔴 Hard

```java
import java.util.List;
import java.util.stream.Collectors;

public List<String> filtraETrasforma(List<String> parole) {
    // TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
}
```

**Cosa devi completare:**

1. **Logica completa** — Stream API, lambda, method references, collectors.

---

## Esempio 3 — Pattern Observer: sistema di notifiche

Obiettivo: implementare il pattern Observer con un `EventBus` che permette a più `Listener` di iscriversi e ricevere notifiche quando viene pubblicato un evento.

### 🟢 Easy

```java
import java.util.ArrayList;
import java.util.List;

public interface Listener {
    void onEvent(String evento);
}

public class EventBus {
    private List<Listener> listeners = new ArrayList<>();

    // TOCCA A TE: aggiungi `listener` alla lista `listeners`
    public void subscribe(Listener listener) {

    }

    // TOCCA A TE: itera su `listeners` e chiama onEvent(evento)
    // su ognuno usando un for-each
    public void publish(String evento) {

    }
}
```

**Cosa devi completare:**

1. **subscribe**: Una sola riga — aggiungi il listener alla lista.
2. **publish**: Per ogni listener registrato, notificalo chiamando il metodo dell'interfaccia.

---

### 🟡 Medium

```java
import java.util.ArrayList;
import java.util.List;

public interface Listener {
    void onEvent(String evento);
}

public class EventBus {
    private List<Listener> listeners = new ArrayList<>();

    // TOCCA A TE: registra un nuovo listener
    public void subscribe(Listener listener) {

    }

    // TOCCA A TE: notifica tutti i listener registrati dell'evento
    public void publish(String evento) {

    }
}
```

**Cosa devi completare:**

1. **subscribe**: Come si aggiunge un elemento a una lista in Java? Una riga sola.
2. **publish**: Tutti i listener registrati devono sapere dell'evento. Come li raggiungi tutti senza ignorare il contratto dell'interfaccia?

---

### 🔴 Hard

```java
import java.util.ArrayList;
import java.util.List;

public interface Listener {
    void onEvent(String evento);
}

public class EventBus {
    private List<Listener> listeners = new ArrayList<>();

    // TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
    public void subscribe(Listener listener) { }

    public void publish(String evento) { }
}
```

**Cosa devi completare:**

1. **Logica completa** — Pattern Observer, interfacce, iterazione su collezioni.
