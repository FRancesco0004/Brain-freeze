# Brain-Freeze — C Examples

Questi esempi coprono tre concetti fondamentali di C: **puntatori e aritmetica**, **allocazione dinamica della memoria**, e **ricorsione con array**.

---

## Esempio 1 — Puntatori: inversione di un array in-place

Obiettivo: invertire un array di interi in-place usando due puntatori, senza allocare memoria aggiuntiva.

### 🟢 Easy

```c
#include <stdio.h>

void inverti(int *arr, int n) {
    int *sx = arr;
    int *dx = arr + n - 1;

    while (sx < dx) {
        /* TOCCA A TE: salva il valore puntato da sx in una variabile temporanea `tmp`
           usando la dereferenziazione: int tmp = *sx */

        /* TOCCA A TE: copia il valore puntato da dx in quello puntato da sx:
           *sx = *dx */

        /* TOCCA A TE: copia tmp nel valore puntato da dx:
           *dx = tmp */

        sx++;
        dx--;
    }
}
```

**Cosa devi completare:**

1. **tmp**: L'hint ti dà già la riga esatta. `*sx` dereferenzia il puntatore — accede al valore che contiene.
2. **swap parte 1**: Copia il valore destro nel sinistro tramite dereferenziazione.
3. **swap parte 2**: Completa lo scambio copiando `tmp` nel posto puntato da `dx`.

---

### 🟡 Medium

```c
#include <stdio.h>

void inverti(int *arr, int n) {
    int *sx = arr;
    int *dx = arr + n - 1;

    while (sx < dx) {
        /* TOCCA A TE: scambia i valori puntati da sx e dx */

        sx++;
        dx--;
    }
}
```

**Cosa devi completare:**

1. **Swap tramite puntatori**: Per scambiare due valori in C serve una variabile temporanea. L'operatore `*` dereferenzia un puntatore — usalo sia per leggere che per scrivere il valore a quell'indirizzo.

---

### 🔴 Hard

```c
#include <stdio.h>

void inverti(int *arr, int n) {
    /* TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere */
}
```

**Cosa devi completare:**

1. **Logica completa** — Puntatori, dereferenziazione, aritmetica dei puntatori, swap in-place.

---

## Esempio 2 — Allocazione dinamica: lista concatenata

Obiettivo: definire una struttura `Nodo` e implementare una funzione `aggiungi_in_testa` che inserisce un nuovo nodo all'inizio della lista.

### 🟢 Easy

```c
#include <stdlib.h>

typedef struct Nodo {
    int valore;
    struct Nodo *prossimo;
} Nodo;

Nodo* aggiungi_in_testa(Nodo *testa, int val) {
    /* TOCCA A TE: alloca un nuovo Nodo con malloc(sizeof(Nodo))
       e salvalo in un puntatore `nuovo` */

    /* TOCCA A TE: assegna `val` al campo `nuovo->valore` */

    /* TOCCA A TE: collega il nuovo nodo alla lista esistente:
       nuovo->prossimo = testa */

    return nuovo;
}
```

**Cosa devi completare:**

1. **malloc**: `malloc(sizeof(Nodo))` alloca esattamente la memoria necessaria per un `Nodo`. Il cast `(Nodo*)` converte il puntatore generico restituito.
2. **valore**: L'operatore `->` accede ai campi di una struct tramite puntatore.
3. **collegamento**: Il nuovo nodo deve puntare a chi era la testa prima — così si inserisce in testa.

---

### 🟡 Medium

```c
#include <stdlib.h>

typedef struct Nodo {
    int valore;
    struct Nodo *prossimo;
} Nodo;

Nodo* aggiungi_in_testa(Nodo *testa, int val) {
    /* TOCCA A TE: crea un nuovo nodo allocando memoria dinamicamente */

    /* TOCCA A TE: inizializza i suoi campi e collegalo alla lista */

    return nuovo;
}
```

**Cosa devi completare:**

1. **Allocazione**: In C la memoria per strutture dinamiche si ottiene esplicitamente. Quale funzione usi e quanta memoria richiedi?
2. **Inizializzazione e collegamento**: Il nodo deve contenere il valore e sapere chi viene dopo di lui nella lista. Come si accede ai campi di una struct tramite puntatore?

---

### 🔴 Hard

```c
#include <stdlib.h>

typedef struct Nodo {
    int valore;
    struct Nodo *prossimo;
} Nodo;

Nodo* aggiungi_in_testa(Nodo *testa, int val) {
    /* TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere */
}
```

**Cosa devi completare:**

1. **Logica completa** — `malloc`, `sizeof`, operatore `->`, linked list in C.

---

## Esempio 3 — Ricorsione: ricerca binaria

Obiettivo: implementare la ricerca binaria ricorsiva su un array ordinato. Ritorna l'indice dell'elemento se trovato, -1 altrimenti.

### 🟢 Easy

```c
int ricerca_binaria(int *arr, int sx, int dx, int target) {
    /* TOCCA A TE: caso base — se sx > dx l'elemento non esiste, ritorna -1 */

    int mid = sx + (dx - sx) / 2;

    /* TOCCA A TE: se arr[mid] == target, ritorna mid */

    /* TOCCA A TE: se arr[mid] < target, cerca nella metà destra:
       ricerca_binaria(arr, mid + 1, dx, target) */

    /* TOCCA A TE: altrimenti cerca nella metà sinistra:
       ricerca_binaria(arr, sx, mid - 1, target) */
}
```

**Cosa devi completare:**

1. **Caso base**: Se i due indici si incrociano, lo spazio di ricerca è esaurito.
2. **Trovato**: Se l'elemento centrale è proprio quello cercato, hai finito.
3. **Metà destra**: `arr[mid] < target` significa che il target è a destra di `mid`.
4. **Metà sinistra**: Il caso opposto — il target è a sinistra di `mid`.

---

### 🟡 Medium

```c
int ricerca_binaria(int *arr, int sx, int dx, int target) {
    /* TOCCA A TE: gestisci il caso in cui lo spazio di ricerca è esaurito */

    int mid = sx + (dx - sx) / 2;

    /* TOCCA A TE: controlla se hai trovato il target */

    /* TOCCA A TE: restringi lo spazio di ricerca alla metà corretta */
}
```

**Cosa devi completare:**

1. **Caso base**: Ogni funzione ricorsiva deve sapere quando fermarsi. Quando è impossibile che il target esista nell'intervallo `[sx, dx]`?
2. **Confronto centrale**: L'elemento a `mid` può essere uguale, minore o maggiore del target. Solo uno di questi casi termina la ricerca immediatamente.
3. **Dimezzamento**: A seconda del confronto, la prossima chiamata ricorsiva deve coprire solo metà dell'intervallo attuale. Quale metà?

---

### 🔴 Hard

```c
int ricerca_binaria(int *arr, int sx, int dx, int target) {
    /* TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere */
}
```

**Cosa devi completare:**

1. **Logica completa** — Ricorsione, divide et impera, ricerca binaria su array.
