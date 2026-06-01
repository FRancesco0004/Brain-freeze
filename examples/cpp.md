# Brain-Freeze — C++ Examples

Questi esempi coprono tre concetti fondamentali di C++: **template**, **RAII e smart pointer**, e **overloading degli operatori**.

---

## Esempio 1 — Template: coppia generica

Obiettivo: implementare una classe template `Coppia<T, U>` che contiene due valori di tipo diverso e un metodo `scambia()` che inverte i valori (assumendo `T == U`).

### 🟢 Easy

```cpp
#include <utility>

// TOCCA A TE: dichiara la classe come template con due parametri di tipo T e U
// usando `template <typename T, typename U>`
class Coppia {
public:
    T primo;
    U secondo;

    Coppia(T p, U s) : primo(p), secondo(s) {}

    // TOCCA A TE: usa std::swap(primo, secondo) per scambiare i due valori
    void scambia() {

    }
};
```

**Cosa devi completare:**

1. **Dichiarazione template**: L'hint ti dà già la sintassi esatta da mettere sulla riga prima della classe.
2. **scambia**: `std::swap` scambia due valori in-place. Passagli i due campi della coppia.

---

### 🟡 Medium

```cpp
#include <utility>

// TOCCA A TE: rendi questa classe generica su due tipi
class Coppia {
public:
    T primo;
    U secondo;

    Coppia(T p, U s) : primo(p), secondo(s) {}

    // TOCCA A TE: scambia i valori dei due campi
    void scambia() {

    }
};
```

**Cosa devi completare:**

1. **Template declaration**: In C++ i template si dichiarano con una riga prima della classe. Come dici al compilatore che `T` e `U` sono tipi generici?
2. **scambia**: La libreria standard offre una funzione per scambiare due valori senza scrivere la variabile temporanea manualmente. Sai qual è?

---

### 🔴 Hard

```cpp
#include <utility>

// TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
class Coppia {
public:
    void scambia() { }
};
```

**Cosa devi completare:**

1. **Logica completa** — Template, typename, initializer list, `std::swap`.

---

## Esempio 2 — Smart Pointer e RAII: buffer gestito

Obiettivo: implementare una classe `Buffer` che gestisce un array dinamico di interi usando `std::unique_ptr` — senza `delete` esplicito.

### 🟢 Easy

```cpp
#include <memory>
#include <stdexcept>

class Buffer {
private:
    // TOCCA A TE: dichiara un membro `dati` di tipo std::unique_ptr<int[]>
    // e un membro `dimensione` di tipo size_t

    size_t dimensione;

public:
    // TOCCA A TE: nel costruttore, inizializza `dati` con
    // std::make_unique<int[]>(dim) e `dimensione` con dim
    Buffer(size_t dim) {

    }

    int& operator[](size_t i) {
        if (i >= dimensione) throw std::out_of_range("indice fuori range");
        return dati[i];
    }

    size_t size() const { return dimensione; }
};
```

**Cosa devi completare:**

1. **Membro dati**: `std::unique_ptr<int[]>` è lo smart pointer per array. Dichiaralo come campo privato.
2. **Costruttore**: `std::make_unique<int[]>(dim)` alloca l'array. Puoi usare la initializer list `: dati(...), dimensione(...)` oppure assegnarlo nel corpo.

---

### 🟡 Medium

```cpp
#include <memory>
#include <stdexcept>

class Buffer {
private:
    // TOCCA A TE: dichiara i campi necessari per gestire un array dinamico
    // senza usare new/delete esplicitamente

public:
    // TOCCA A TE: inizializza il buffer allocando memoria in modo sicuro
    Buffer(size_t dim) {

    }

    int& operator[](size_t i) {
        if (i >= dimensione) throw std::out_of_range("indice fuori range");
        return dati[i];
    }

    size_t size() const { return dimensione; }
};
```

**Cosa devi completare:**

1. **Campi**: Hai bisogno di tenere traccia dei dati e della dimensione. RAII significa che la memoria deve essere gestita automaticamente — quale tipo della libreria standard ti evita il `delete`?
2. **Costruttore**: La memoria deve essere allocata al momento della costruzione. Come inizializzi uno smart pointer che gestisce un array?

---

### 🔴 Hard

```cpp
#include <memory>
#include <stdexcept>

class Buffer {
    // TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere

public:
    int& operator[](size_t i) {
        if (i >= dimensione) throw std::out_of_range("indice fuori range");
        return dati[i];
    }

    size_t size() const { return dimensione; }
};
```

**Cosa devi completare:**

1. **Logica completa** — `unique_ptr`, RAII, gestione automatica della memoria, costruttore.

---

## Esempio 3 — Overloading degli operatori: vettore 2D

Obiettivo: implementare una classe `Vec2` con overloading di `operator+`, `operator*` (scalare) e `operator<<` per la stampa.

### 🟢 Easy

```cpp
#include <iostream>

struct Vec2 {
    float x, y;

    Vec2(float x, float y) : x(x), y(y) {}

    // TOCCA A TE: ritorna un nuovo Vec2 con x e y sommati componente per componente
    Vec2 operator+(const Vec2& altro) const {

    }

    // TOCCA A TE: ritorna un nuovo Vec2 con x e y moltiplicati per `scalare`
    Vec2 operator*(float scalare) const {

    }
};

// TOCCA A TE: implementa operator<< come funzione friend che stampa
// il vettore nel formato "(x, y)" su os, poi ritorna os
std::ostream& operator<<(std::ostream& os, const Vec2& v) {

}
```

**Cosa devi completare:**

1. **operator+**: Crea un `Vec2` con `x + altro.x` e `y + altro.y`.
2. **operator***: Crea un `Vec2` con `x * scalare` e `y * scalare`.
3. **operator<<**: Scrivi su `os` con `os << "(" << v.x << ", " << v.y << ")"` e ritorna `os` per permettere il chaining.

---

### 🟡 Medium

```cpp
#include <iostream>

struct Vec2 {
    float x, y;

    Vec2(float x, float y) : x(x), y(y) {}

    // TOCCA A TE: somma due vettori componente per componente
    Vec2 operator+(const Vec2& altro) const {

    }

    // TOCCA A TE: scala il vettore per un valore float
    Vec2 operator*(float scalare) const {

    }
};

// TOCCA A TE: permetti la stampa del vettore con cout
std::ostream& operator<<(std::ostream& os, const Vec2& v) {

}
```

**Cosa devi completare:**

1. **operator+**: L'overloading di `+` deve ritornare un nuovo oggetto — non modificare `this`. Come costruisci un `Vec2` sommando le componenti?
2. **operator***: Stesso principio di `+`, ma con una moltiplicazione scalare.
3. **operator<<**: Deve ricevere uno `std::ostream&` e ritornarlo per permettere `cout << v1 << v2`. Come scrivi su uno stream in C++?

---

### 🔴 Hard

```cpp
#include <iostream>

struct Vec2 {
    float x, y;

    Vec2(float x, float y) : x(x), y(y) {}

    // TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
};

std::ostream& operator<<(std::ostream& os, const Vec2& v) {
    // TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
}
```

**Cosa devi completare:**

1. **operator+ e operator***: Overloading di operatori aritmetici, oggetti immutabili, costruzione per valore.
2. **operator<<**: Overloading dell'operatore di stream, chaining, formato di output.
