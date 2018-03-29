
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

## Repasemos algunos detalles sobre herencia

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
  B b01;
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

* Los member functions de la clase Hijo NO pueden acceder protected data members de objetos de clase Padre.

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
  void bfunc(B z) {z.x;}
};
```

* Los member functions de la clase Hijo NO pueden acceder protected data members de objetos de clase Padre.

---


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

---

## La importancia de sobrecargar operator<


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

## La importancia de sobrecargar operator< (cont)


* La operación de sort depende de comparaciones entre elementos del vector.

* Si defines operator<, la función `sort` podrá operar sobre objetos de tu clase.

---

## Ejemplo:

[https://repl.it/@rafaelarceupr/Sorting-a-vector-of-frac](https://repl.it/@rafaelarceupr/Sorting-a-vector-of-frac)


--- 



