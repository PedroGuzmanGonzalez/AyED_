# Algoritmos y estructuras de datos
## clase 02/09
### Listas
En este codigo, **template &lt;class T&gt;** esta creando un clase T generica, que va a parametrizar a la clase Nodo, por ejemplo:  
- Nodo&lt;int&gt; tendrá un int como dato, Nodo&lt;float&gt; tendrá un float, etc.

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
Tiene un solo campo que es un puntero a Nodo&lt;T&gt;  
Luego tiene los métodos publicos:
- Dos constructores: uno no acepta parametros y crea con **new** el puntero **czo** y el otro tiene el puntero **czo** como parametro
- Y también tiene todos los metodos que vimos en la **signatura** (add, esVacia, cabeza, etc).
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
Vemos cada método: En cada uno de los metodos vamos a tener que poner a donde pertenece el metodo (template &lt;class T&gt;> void Lista&lt;T&gt;::nombreMetodo)
- add(T d)
```cpp
template <class T>
void Lista<T>::add(T d) //100
{
    Nodo<T>* nuevo = new Nodo<T>(d);
    nuevo->set_next(czo);
    czo = nuevo;
}
```
- esVacia(void)
```cpp
template <class T>
bool Lista<T>::esvacia(void)
{
    return czo->es_vacio();
}
```
- cabeza(void)
```cpp
template <class T>
T Lista<T>::cabeza(void)
{
    if (this->esvacia()) {
        cout << " Error, Cabeza de lista vacia";
        return NULL;
    }
    return czo->get_dato();
}
```
- resto(void)
```cpp
template <class T>
Lista<T>* Lista<T>::resto(void)
{
    Lista* l = new Lista(czo->get_next());
    return (l);
}
```

- Método toPrint: puede ser implementado de forma iterativa o recursiva

  - **De forma iterativa:**
  
    - usando cout:

    ```cpp
    template <class T>
    void Lista<T>::toPrint2(String p)
    {
        Nodo<T>* aux;
        aux = this -> czo;
    
        while (aux ->get_next()!=NULL){
            cout << aux -> get_dato() << " ":
            aux = aux -> get_next();
        }
    
        cout << p << endl;
    }
    ```
    - usando ostringstream:
    ```cpp
    template <class T>
    void Lista<T>::toPrint2(String p)
    {
        Nodo<T>* aux;
        aux = this -> czo;
        ostringstream stm;
    
        while (aux ->get_next()!=NULL){
            stm << aux -> get_dato() << " ":
            aux = aux -> get_next();
        }
    
        stm << p << endl;
        return stm.str();
    }
    ```


  - **De forma recursiva:**
    ```cpp
    template <class T>
    string Lista<T>::toPrint(string p)
    {
    if (this->esvacia()) {
        return p;
    }
    else {
        //std::ostringstream stm;
        ostringstream stm;
        stm << this->cabeza() << "-" << this->resto()->toPrint(p) << endl;
        //cout<<endl<<" stm.str()= "<<stm.str()<<endl;
        return stm.str();
    }
    }
    ```


























