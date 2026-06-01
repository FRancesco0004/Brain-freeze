# Brain-Freeze — Python Examples

Questi esempi mostrano come Brain-Freeze si comporta ai tre livelli di difficoltà su due concetti fondamentali di Python: **ricorsione** e **list comprehension con filtraggio**.

---

## Esempio 1 — Ricorsione: Fibonacci

### 🟢 Easy

```python
def fibonacci(n: int) -> int:
    """Restituisce l'n-esimo numero della sequenza di Fibonacci."""

    # TOCCA A TE: se n è 0, ritorna 0; se n è 1, ritorna 1

    # TOCCA A TE: ritorna la somma di fibonacci(n - 1) e fibonacci(n - 2)
```

**Cosa devi completare:**

1. **Riga 4 — caso base doppio**: Fibonacci ha due casi base. L'hint ti dice già i valori esatti da controllare e cosa ritornare per ciascuno.
2. **Riga 6 — chiamata ricorsiva**: La definizione matematica è `F(n) = F(n-1) + F(n-2)`. Traducila direttamente in Python.

---

### 🟡 Medium

```python
def fibonacci(n: int) -> int:
    """Restituisce l'n-esimo numero della sequenza di Fibonacci."""

    # TOCCA A TE: gestisci i casi base della sequenza

    # TOCCA A TE: combina i due sottoproblemi ricorsivi
```

**Cosa devi completare:**

1. **Riga 4 — casi base**: Fibonacci ne ha due, non uno solo. Pensa a quali valori di `n` la sequenza è definita direttamente.
2. **Riga 6 — chiamata ricorsiva**: Ogni numero di Fibonacci dipende dai due che lo precedono. Esprimi questa relazione in codice.

---

### 🔴 Hard

```python
def fibonacci(n: int) -> int:
    """Restituisce l'n-esimo numero della sequenza di Fibonacci."""

    # TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
```

**Cosa devi completare:**

1. **Logica completa** — Ricorsione con casi base multipli.

---

## Esempio 2 — List Comprehension: filtraggio e trasformazione

Obiettivo: data una lista di stringhe, restituire una nuova lista con solo quelle che hanno più di 4 caratteri, convertite in maiuscolo.

Input: `["cane", "gatto", "bue", "elefante", "ratto"]`  
Output atteso: `["GATTO", "ELEFANTE", "RATTO"]`

### 🟢 Easy

```python
def parole_lunghe(parole: list[str]) -> list[str]:
    """Restituisce le parole con più di 4 caratteri, in maiuscolo."""

    # TOCCA A TE: usa una list comprehension — per ogni `p` in `parole`,
    # includi `p.upper()` solo se `len(p) > 4`
```

**Cosa devi completare:**

1. **List comprehension con filtro**: La sintassi è `[espressione for elemento in lista if condizione]`. L'hint ti indica già espressione, elemento e condizione.

---

### 🟡 Medium

```python
def parole_lunghe(parole: list[str]) -> list[str]:
    """Restituisce le parole con più di 4 caratteri, in maiuscolo."""

    # TOCCA A TE: trasforma e filtra la lista in una sola espressione
```

**Cosa devi completare:**

1. **List comprehension**: Python permette di filtrare e trasformare una lista in una sola riga. Pensa a come combinare la trasformazione (maiuscolo) con la condizione (lunghezza).

---

### 🔴 Hard

```python
def parole_lunghe(parole: list[str]) -> list[str]:
    """Restituisce le parole con più di 4 caratteri, in maiuscolo."""

    # TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
```

**Cosa devi completare:**

1. **Logica completa** — List comprehension con trasformazione e filtro.

---

## Esempio 3 — Decoratori: misurazione del tempo di esecuzione

Obiettivo: scrivere un decoratore `@timer` che stampa quanto tempo impiega una funzione a eseguire.

### 🟢 Easy

```python
import time
from functools import wraps
from typing import Callable

def timer(func: Callable) -> Callable:
    """Decoratore che misura il tempo di esecuzione di una funzione."""

    @wraps(func)
    def wrapper(*args, **kwargs):
        # TOCCA A TE: salva il tempo corrente in una variabile `start`
        # usando time.time()

        result = func(*args, **kwargs)

        # TOCCA A TE: calcola il tempo trascorso sottraendo `start`
        # dal tempo corrente, salvalo in `elapsed`

        print(f"{func.__name__} ha impiegato {elapsed:.4f} secondi")
        return result

    return wrapper
```

**Cosa devi completare:**

1. **Riga 10 — timestamp iniziale**: `time.time()` restituisce il tempo corrente in secondi. Salvalo prima che la funzione parta.
2. **Riga 14 — tempo trascorso**: Chiama di nuovo `time.time()` dopo l'esecuzione e sottrai `start`. Il risultato è la durata in secondi.

---

### 🟡 Medium

```python
import time
from functools import wraps
from typing import Callable

def timer(func: Callable) -> Callable:
    """Decoratore che misura il tempo di esecuzione di una funzione."""

    @wraps(func)
    def wrapper(*args, **kwargs):
        # TOCCA A TE: registra il momento di inizio

        result = func(*args, **kwargs)

        # TOCCA A TE: calcola la durata e stampala con il nome della funzione

        return result

    return wrapper
```

**Cosa devi completare:**

1. **Riga 10 — inizio**: Hai bisogno di registrare il momento esatto in cui la funzione parte. Guarda cosa offre il modulo `time`.
2. **Riga 14 — durata e output**: Confronta il tempo attuale con quello registrato prima. Usa `func.__name__` per stampare il nome della funzione decorata.

---

### 🔴 Hard

```python
import time
from functools import wraps
from typing import Callable

def timer(func: Callable) -> Callable:
    """Decoratore che misura il tempo di esecuzione di una funzione."""

    @wraps(func)
    def wrapper(*args, **kwargs):
        # TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere

    return wrapper
```

**Cosa devi completare:**

1. **Logica completa** — Pattern decoratore con misurazione del tempo.
