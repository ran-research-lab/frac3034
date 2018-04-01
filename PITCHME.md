
## Repaso sobre clases CCOM3034

#### CCOM 3034 - 2017-2018 - Sem 2

---

### Clase fraccion

* Supón que estamos creando una aplicación que va a realizar cálculos matemáticos sobre enteros y fracciones. 

* Tu estas a cargo de diseñar la parte del programa que trabaja con fracciones (capaz de realizar operaciones aritméticas sobre fracciones)

* Para simplificar tu vida y la de tus compañeros decides crear un **ADT fracción**.

--- 

## ADT Fraccion

* ¿qué datos?

* ¿qué operaciones?

---

## Vamos a crear la declaración de la clase fracción en C++

* ¿qué datos hay que guardar en cada objeto que reprente una fracción?
	* ¿qué privilegios debe tener sobre esos datos alguien que use un objeto *fraccion*?

---

## Vamos a implementar algunos de los member functions

* constructor(es)
* setters y getters?
* display

---

## ... más member functions ... 

* suma (implementacion charra)
    * `fraccion f3 = f1.suma(f2);`
* reciproco
    * `fraccion f4 = f1.reciproco();` 
* lessthan
    * `if ( f1.lessthan(f2) )`  

---

## Y ahora implementaremos usando operator overloading

Para que funcionen expresiones como

* `fraccion f3 = f1 + f2;` 
* `fraccion f4 = ~f1;` 
* `if (f1 < f2)` 

---


![](https://scontent-mia3-2.xx.fbcdn.net/v/t1.0-9/13312854_912222522223356_4593980285730674675_n.jpg?_nc_cat=0&oh=360329839bcf46f4eabde8afc0334ff4&oe=5B3A9621) 


---

## Sobrecargando el operador de output stream


* `cout` es un **objeto** de clase *ostream*.
* `<<` es un **operador** usado en combinación con objetos de clase *ostream*

* las operaciones como `cout  << "hello"; ` se convierten en:
    * `operator<<(cout,"hello");`
---


## Sobrecargando a << (cont)

* una operación como `cout << a << "hello`" se convierte en una composición de funciones:
    * `operator<<(operator<<(cout,a),"hello");`

* por lo tanto, cada invocación de `operator<<(cout,a);` debe devolver un ostream.

---

## Sobrecargando a << (cont)


[https://repl.it/@rafaelarceupr/EjemploPuntos-OOP](https://repl.it/@rafaelarceupr/EjemploPuntos-OOP)

* Observe la member function `display()` y la función **externa** que sobrecarga el `operator<<`.

---

## Herencia

Ahora supongamos que te piden crear una clase fracPropia para fracciones propias que luego de
cada operación valide si su contenido es una fracción propia.

Crearemos una clase hija de la clase frac.

* El primer cambio que debemos hacer es en la clase `frac`: cambiar el acceso de sus data members a 
**protected** para que las clases hijas de frac puedan tener acceso a esos miembros.

---

### Herencia 

* Método de reusar código haciendo que un objeto tome propiedades de otro objeto mientras añade las suyas propias.

* Facilita la creación de clases más elaboradas a partir de clases más sencillas

---


## Repasemos algunos detalles sobre herencia

![](https://docs.google.com/drawings/d/e/2PACX-1vTuEX6Y8_lO-atx_PyOWVXXnW47xbntEb4tnFYT3HgZD-159RBZ7f-5sRt0oS3XDfgf6wOXU0BrZChK/pub?w=1440&h=1080)


---

#### Constructores

```cpp
class A {
public: 
  A() { cout << "I am A's constructor\n"; }
};


class B : public A {
public: 
  B() { cout << "I am B's constructor\n"; }
};


int main() {
  B b01; // Prints "I am A's constructor"
         // Then prints: "I am B's constructor"
}
```
* El constructor de B automaticamente invoca al de A (antes de ejecutar las instrucciones del constructor de B).

---

#### Acceso en member functs de clase hija

```cpp
class A {
protected:
  int x;
public: 
  A() { cout << "I am A's constructor\n"; }
};


class B : public A {
public: 
  B() { cout << "I am B's constructor\n"; }
  void bfunc() { x = 10; }
};
```

* No hay problema


---

#### Acceso a paremetro de clase padre

```cpp
class A {
protected:
  int x;
public: 
  A() { cout << "I am A's constructor\n"; }
};


class B : public A {
public: 
  B() { cout << "I am B's constructor\n"; }
  void bfunc(A z) {z.x;}
};
```

* Los member functions de la clase Hijo NO pueden acceder protected data members de **parámetros** de clase Padre.


---


## Declaración y constructor

```cpp

class fracPropia : public frac {
public:
  fracPropia(int n, int d) : frac(n,d) {
    if (n >= d) cerr << "No es propia\n";
  }  
};
```

* Hasta ahora todo bien....

---

#### Habiendo declarado el constructor....

```cpp
  frac       f1(1,1);     // funciona
  fracPropia fp01(8,9);   // funciona

  cout << fp01 << endl;   // funciona
  
  fracPropia fp02 = f1;   //No funciona
```

```
main.cpp:23:21: error: conversion from ‘frac’ to 
          non-scalar type ‘fracPropia’ requested
          fracPropia fp02 = f1;
```

* C++ no es capaz de "castear" un objeto padre a un objeto hijo

* Si pretendemos hacer eso, la clase padre debe ofrecer getters y . . . 

---

### ... debemos sobrecargar el copy constructor..

* El *copy constructor* es un constructor que es invocado durante las conversiones entre una clase y otra 

```cpp
frac f1;
fracParcial fp01;

fp01 = f1;   // conversion de frac a fracParcial! 
```

* implementación de un copy constr para fracPropia (de forma que podamos asignar un `frac` a un `fracPropia`)

```cpp
fracPropia(const frac &f) : frac(f.getNum(),f.getDen()) {}
```

--- 

#### Polimorfismo

* Work in the same manner with different objects, which define a specific implementation of some abstract behavior.

* For example,

    * Being able to create an array of different objects and apply an operation over all of them.

    * A GIS software keeps a collection of shapes and must compute the combined area of the shapes.
 
      * But wait, C++ arrays are homogenous, right??

---

### Ejemplo de polimorfismo

* Un arreglo objetos de diferentes clases y realice operación sobre todos.

![](https://i.imgur.com/J0rp761.png)


[https://gist.github.com/ccom3033/6318333](https://gist.github.com/ccom3033/6318333)

---


### Virtual function

* A **virtual function** is a member function that you expect to be redefined in derived classes. When you refer to a derived class object using a pointer or a reference to the base class, you can call a virtual function for that object and execute the derived class's version of the function.

---

```cpp
class Base {
public:
  virtual void foo() { cout << "The Base class foo\n"; }
};

class Derived : public Base {
public:
  void foo() { cout << "The Derived class foo\n"; }
};

int main() {
  Base *b01, *b02;
  b01 = new Derived;
  b02 = new Base;
  b01->foo(); // prints "The Derived class foo"
  b02->foo(); // prints "The Base class foo"
}
```

---

* Cuando sobrecargamos member functions que **no** son **virtual**, la decisión sobre qué member function llamar se toma at **compile time** ...


---

```cpp
#include <iostream>
using namespace std;

class Base {
public:
  // esta función NO ES VIRTUAL
  void foo() { cout << "The Base class foo\n"; }
};

class Derived : public Base {
public:
  void foo() { cout << "The Derived class foo\n"; }
};

int main() {
  Base *b01, *b02;
  b01 = new Derived;
  b02 = new Base;
  b01->foo(); // prints "The Base class foo"
  b02->foo(); // prints "The Base class foo"
}
```

---


* A **pure virtual** function is a virtual function whose declaration ends in =0 : ... Derived classes need to override/implement all inherited pure virtual functions. If they do not, they too will become abstract. An interesting 'feature' of C++ is that a class can define a pure virtual function that has an implementation.

---

```cpp
#include <iostream>
using namespace std;

class Base {
public:
  // THIS IS A PURE VIRTUAL FUNCTION, THEREFORE
  // BASE IS AN **ABSTRACT CLASS**
  virtual void foo() = 0;
};

int main() {
  Base *b01;
  b01 = Base; //Error, can't instance an abstract class
}
```
---


```cpp
#include <iostream>
using namespace std;

class Base {
public:
  // ESTA FUNCION ES PURE VIRTUAL!!!!
  virtual void foo() = 0;
};

class Derived : public Base {
public:
};

int main() {
  Base *b01;
  b01 = new Derived; // No funciona, pues
                     // Derived no ha implementado 
                     // la función foo
}
```



---


### La importancia de sobrecargar operator<


* STL incluye una función `sort` que funciona para los vectores y otras estructuras de datos.

```cpp
vector<int> s = {5, 7, 4, 2, 8, 6, 1, 9, 0, 3}; 

// sort using the default operator<
std::sort(s.begin(), s.end());
for (auto a : s) {
    std::cout << a << " ";
}  
```

---

### La importancia de sobrecargar operator< (cont)


* La operación de sort depende de comparaciones entre elementos del vector.

* Si defines operator<, la función `sort` podrá operar sobre objetos de tu clase.

---

### Ejemplo:

[https://repl.it/@rafaelarceupr/Sorting-a-vector-of-frac](https://repl.it/@rafaelarceupr/Sorting-a-vector-of-frac)


--- 



