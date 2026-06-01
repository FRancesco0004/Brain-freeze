# Brain-Freeze — Rust Examples

Questi esempi coprono due dei concetti più caratteristici di Rust: **ownership & borrowing** e **gestione degli errori con `Result`**.

---

## Esempio 1 — Ownership: inversione di una stringa

Obiettivo: scrivere una funzione che inverte una stringa senza usare `.chars().rev()` direttamente — costruendo il risultato manualmente carattere per carattere.

### 🟢 Easy

```rust
fn inverti_stringa(s: &str) -> String {
    let mut risultato = String::new();

    // YOUR TURN: itera sui caratteri di `s` con `.chars()`
    // e per ognuno usa `risultato.insert(0, c)` per aggiungerlo in testa

    risultato
}
```

**What you need to fill in:**

1. **Loop con insert in testa**: L'hint ti dice già il metodo da usare e il punto di inserimento. `insert(0, c)` aggiunge il carattere `c` all'indice 0 della stringa, spostando gli altri.

---

### 🟡 Medium

```rust
fn inverti_stringa(s: &str) -> String {
    let mut risultato = String::new();

    // YOUR TURN: scorri i caratteri di `s` e costruisci `risultato` al contrario

    risultato
}
```

**What you need to fill in:**

1. **Iterazione e costruzione inversa**: Ci sono più modi per scorrere i caratteri di una `&str` in Rust. Pensa a come aggiungere ogni carattere in modo che l'ordine finale sia invertito.

---

### 🔴 Hard

```rust
fn inverti_stringa(s: &str) -> String {
    // YOUR TURN: from here on, think about what could happen
}
```

**What you need to fill in:**

1. **Logica completa** — Ownership, `String` mutabile, iterazione su `&str`.

---

## Esempio 2 — Result: parsing e propagazione degli errori

Obiettivo: leggere un numero intero da una stringa e restituire il suo doppio, propagando l'errore di parsing se la stringa non è un numero valido.

### 🟢 Easy

```rust
use std::num::ParseIntError;

fn doppio_da_stringa(s: &str) -> Result<i32, ParseIntError> {
    // YOUR TURN: usa `s.trim().parse::<i32>()` per ottenere un Result,
    // poi usa `?` per propagare l'errore automaticamente e salvare il valore in `n`

    // YOUR TURN: ritorna Ok(n * 2)
}
```

**What you need to fill in:**

1. **Parsing con `?`**: `.parse::<i32>()` restituisce un `Result<i32, ParseIntError>`. Aggiungere `?` dopo la chiamata propaga automaticamente l'errore se il parsing fallisce, altrimenti estrae il valore.
2. **Wrap nel Result**: Quando tutto va bene, il valore di ritorno deve essere wrappato in `Ok(...)`.

---

### 🟡 Medium

```rust
use std::num::ParseIntError;

fn doppio_da_stringa(s: &str) -> Result<i32, ParseIntError> {
    // YOUR TURN: fai il parsing della stringa gestendo il possibile errore

    // YOUR TURN: ritorna il risultato corretto
}
```

**What you need to fill in:**

1. **Parsing e gestione errore**: Rust non ha eccezioni — gli errori viaggiano nel tipo di ritorno. Pensa a come estrarre il valore da un `Result` e cosa succede se il parsing fallisce.
2. **Valore di ritorno**: La firma dice `Result<i32, ParseIntError>`. Il valore finale deve essere wrappato di conseguenza.

---

### 🔴 Hard

```rust
use std::num::ParseIntError;

fn doppio_da_stringa(s: &str) -> Result<i32, ParseIntError> {
    // YOUR TURN: from here on, think about what could happen
}
```

**What you need to fill in:**

1. **Logica completa** — `Result`, operatore `?`, error propagation.

---

## Esempio 3 — Lifetimes: funzione che ritorna il riferimento più lungo

Obiettivo: scrivere una funzione che, date due stringhe slice, restituisce quella più lunga. Il lifetime annotation è necessario.

### 🟢 Easy

```rust
fn piu_lunga<'a>(x: &'a str, y: &'a str) -> &'a str {
    // YOUR TURN: confronta la lunghezza di `x` e `y` con `.len()`
    // e ritorna `x` se è più lungo, altrimenti `y`
}
```

**What you need to fill in:**

1. **Confronto e ritorno**: La signature con il lifetime `'a` è già scritta — dice al compilatore che il riferimento restituito vivrà tanto quanto il più corto tra `x` e `y`. Tu devi solo scrivere il confronto.

---

### 🟡 Medium

```rust
fn piu_lunga<'a>(x: &'a str, y: &'a str) -> &'a str {
    // YOUR TURN: determina quale delle due stringhe è più lunga e ritornala
}
```

**What you need to fill in:**

1. **Confronto con lifetime**: Il compilatore sa già quanto vivono i riferimenti grazie alla firma. Il corpo della funzione è logicamente semplice — l'unica difficoltà è capire *perché* il lifetime annotation è necessario nella firma.

---

### 🔴 Hard

```rust
fn piu_lunga<'a>(x: &'a str, y: &'a str) -> &'a str {
    // YOUR TURN: from here on, think about what could happen
}
```

**What you need to fill in:**

1. **Logica completa** — Lifetime annotations, borrowing, ritorno di riferimenti.
