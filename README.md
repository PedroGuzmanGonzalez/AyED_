# Algoritmos y estructuras de datos
## clase 02/09
### Listas
En este codigo, **template &lt;class T&gt;** esta creando un clase T generica, que va a parametrizar a la clase Nodo, por ejemplo:  
Nodo&lt;int&gt; tendrá un int como dato, Nodo&lt;float&gt; tendrá un float, etc.  
Tenemos además, metodos publicos:  
- Dos constructores: uno no acepta parametros y el otro tiene el dato de tipo T como parametro (los dos dejan como NULL al puntero next)
- Dos setters: uno para el dato de tipo T y otro para el puntero
- Dos getters: uno para el dato de tipo T y otro para el puntero
- Y otro método para saber si el puntero es NULL o no
```cpp
template <class T> class Nodo {
private:
    T dato;
    Nodo* next;
public:
    Nodo() { next = NULL; };
    Nodo(T a) { dato = a; next = NULL; };
    void set_dato(T a) { dato = a; };
    void set_next(Nodo* n) { next = n; };
    T get_dato() { return dato; };
    Nodo* get_next() { return next; };
    bool es_vacio() { return next == NULL; }
};
```
Esta otra clase lista tambien esta parametrizada por un dato de tipo T genérico  
```cpp
template <class T> class Lista {
private: Nodo<T>* czo;
     
public:
    Lista() { czo = new Nodo<T>(); };
    Lista(Nodo<T>* n) { czo = n; };
    //~Lista(void);
    void add(T d); //sumar nodos a la lista
    bool esvacia(void);
    T cabeza(void); //retorna el dato del primer nodo
    Lista* resto(void); //retorna el puntero al "resto" de la lista
                        //resto= lo que queda de la lista sin la cabeza
    string toPrint(string p);
    T suma(T i);
    int size();
    void borrar(void); //borra la cabeza
    void borrar_last();//borra el ultimo
    void concat(Lista<T>* l1);// le transfiere los datos de l1 a this
    Lista<T>* copy(void);// hace una copia de la lista
    void tomar(int n);//deja "vivos" los n primeros nodos y borra el resto
   
};
```
