# Brain-Freeze — Go Examples

Questi esempi coprono due dei concetti più caratteristici di Go: **goroutine e canali** e **interfacce**.

---

## Esempio 1 — Goroutine e canali: somma parallela

Obiettivo: dividere una slice in due metà, calcolare la somma di ciascuna metà in goroutine separate tramite un canale, poi combinare i due risultati.

### 🟢 Easy

```go
func sommaParallela(numeri []int) int {
    ch := make(chan int)
    meta := len(numeri) / 2

    // YOUR TURN: lancia una goroutine con `go func()` che calcola la somma
    // di numeri[:meta] e la invia sul canale con `ch <- somma`

    // YOUR TURN: lancia una seconda goroutine che calcola la somma
    // di numeri[meta:] e la invia sul canale

    primo := <-ch
    secondo := <-ch
    return primo + secondo
}
```

**What you need to fill in:**

1. **Prima goroutine**: Una goroutine anonima in Go si lancia con `go func() { ... }()`. Itera su `numeri[:meta]`, accumula la somma e mandala sul canale.
2. **Seconda goroutine**: Uguale alla prima ma per la seconda metà `numeri[meta:]`.

---

### 🟡 Medium

```go
func sommaParallela(numeri []int) int {
    ch := make(chan int)
    meta := len(numeri) / 2

    // YOUR TURN: calcola la somma della prima metà in una goroutine separata

    // YOUR TURN: calcola la somma della seconda metà in un'altra goroutine

    primo := <-ch
    secondo := <-ch
    return primo + secondo
}
```

**What you need to fill in:**

1. **Goroutine 1**: Go permette di eseguire codice in parallelo con la parola chiave `go`. Come comunica il risultato al chiamante senza condividere memoria?
2. **Goroutine 2**: Stesso pattern della prima, su una porzione diversa dello slice.

---

### 🔴 Hard

```go
func sommaParallela(numeri []int) int {
    // YOUR TURN: from here on, think about what could happen
}
```

**What you need to fill in:**

1. **Logica completa** — Goroutine, canali, slice splitting, comunicazione asincrona.

---

## Esempio 2 — Interfacce: area di forme geometriche

Obiettivo: definire un'interfaccia `Forma` con un metodo `Area() float64`, implementarla per `Cerchio` e `Rettangolo`, e scrivere una funzione che calcola l'area totale di una lista di forme.

### 🟢 Easy

```go
import "math"

type Forma interface {
    // YOUR TURN: dichiara il metodo `Area` che ritorna un float64
}

type Cerchio struct {
    Raggio float64
}

type Rettangolo struct {
    Larghezza, Altezza float64
}

// YOUR TURN: implementa il metodo Area per Cerchio
// usando la formula math.Pi * r * r

// YOUR TURN: implementa il metodo Area per Rettangolo
// usando la formula larghezza * altezza

func areaTotale(forme []Forma) float64 {
    totale := 0.0
    for _, f := range forme {
        totale += f.Area()
    }
    return totale
}
```

**What you need to fill in:**

1. **Interfaccia**: Un'interfaccia in Go è solo un insieme di signature di metodi. L'hint ti dice già il nome e il tipo di ritorno.
2. **Area del cerchio**: La formula è `π * r²`. Go ha `math.Pi` e il raggio è `c.Raggio`.
3. **Area del rettangolo**: La formula è larghezza × altezza. I campi sono già nella struct.

---

### 🟡 Medium

```go
import "math"

type Forma interface {
    // YOUR TURN: definisci il contratto che ogni forma deve rispettare
}

type Cerchio struct {
    Raggio float64
}

type Rettangolo struct {
    Larghezza, Altezza float64
}

// YOUR TURN: rendi Cerchio un'implementazione di Forma

// YOUR TURN: rendi Rettangolo un'implementazione di Forma

func areaTotale(forme []Forma) float64 {
    totale := 0.0
    for _, f := range forme {
        totale += f.Area()
    }
    return totale
}
```

**What you need to fill in:**

1. **Interfaccia**: In Go le interfacce si implementano implicitamente. Pensa a quale metodo deve avere qualsiasi forma per poter calcolare la propria area.
2. **Metodo su Cerchio**: Per implementare un'interfaccia in Go, un tipo deve avere tutti i metodi che essa dichiara. Come si associa un metodo a una struct?
3. **Metodo su Rettangolo**: Stesso meccanismo di Cerchio, formula geometrica diversa.

---

### 🔴 Hard

```go
import "math"

type Cerchio struct{ Raggio float64 }
type Rettangolo struct{ Larghezza, Altezza float64 }

// YOUR TURN: from here on, think about what could happen

func areaTotale(forme []Forma) float64 {
    totale := 0.0
    for _, f := range forme {
        totale += f.Area()
    }
    return totale
}
```

**What you need to fill in:**

1. **Logica completa** — Interfacce implicite, method receivers, polimorfismo in Go.
