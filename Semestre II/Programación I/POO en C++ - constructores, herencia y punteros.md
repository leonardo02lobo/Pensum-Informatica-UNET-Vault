---
tags: [tema, semestre-II]
---
# POO en C++ - constructores, herencia y punteros

Unidad III de [[Programación I]]; la sintaxis base viene de [[Computación I]] (C).

## Clase con constructores y destructor
```cpp
class Persona {
    string nombre; int edad;
public:
    Persona() : nombre("N/A"), edad(0) {}
    Persona(string n, int e) : nombre(n), edad(e) {}
    ~Persona() { cout << "Destruyendo " << nombre << endl; }
    void mostrar() const { cout << nombre << " " << edad << endl; }
};
```

## Memoria dinámica y punteros
```cpp
Persona* p = new Persona("Ana", 20);
p->mostrar();
delete p;
int* v = new int[10]; delete[] v;
```
Operadores: `&` dirección, `*` desreferencia, `->` acceso a miembro. Evitar fugas de memoria y punteros colgantes.

## Herencia
Simple (`class B : public A`) y múltiple (`class C : public A, public B`). Modos `public`, `protected`, `private`.

## Polimorfismo
Funciones `virtual`, clases abstractas con `= 0` (virtuales puras), destructor virtual. Funciones amigas (`friend`).

## Sobrecarga de operadores
```cpp
class Vec { public: int x, y;
  Vec operator+(const Vec& o) const { return {x + o.x, y + o.y}; } };
```

## Bits
Operadores `& | ^ ~ << >>`: máscaras y desplazamientos (ver TemaVI-C07 en el Material).

Comparar con [[Programación I - Java C04 Clases, objetos y métodos]]. Aplicación posterior en [[Estructura de Datos]].
