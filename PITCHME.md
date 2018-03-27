
## Repaso sobre clases CCOM3034

---

### Clase fraccion

* Supon que estamos creando una aplicacion que va 
a realizar calculos matematicos sobre enteros y 
fracciones. 

* Tu estas a cargo de diseNar la parte del programa que trabaja con fracciones
(capaz de realizar operaciones aritmeticas sobre fracciones)

* Para simplificar tu vida y la de tus compaNeros decides crear un ADT fraccion.

--- 

## ADT Fraccion

* ?que datos?

* ?que operaciones?

---

### Crearemos la declaracion de la clase fraccion en C++

---

### Crearemos la implementacion de algunas funciones de la clase C++

* constructor(es)
* setters y getters?
* display

---

### Crearemos la implementacion de mas funciones de la clase C++

* suma (implementacion charra)
    * `fraccion f3 = f1.suma(f2);`
* reciproco
    * `fraccion f4 = f1.reciproco(f1);` 
* lessthan
    * `if ( f1.lessthan(f2) )`  

---

### Y ahora implementaremos usando operator overloading

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

## La importancia de sobrecargar operator<

* STL incluye una función `sort` que funciona para los vectores y otras estructuras de datos.

* La operación de sort depende de comparaciones entre elementos del vector.

* Si defines operator<, la función `sort` podrá operar sobre objetos de tu clase.

---

## Ejemplo:

[https://repl.it/@rafaelarceupr/Sorting-a-vector-of-frac](https://repl.it/@rafaelarceupr/Sorting-a-vector-of-frac)
