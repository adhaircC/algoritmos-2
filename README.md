# algoritmos-2
algoritmos-2
## 1. De ejemplos de otras estructuras de datos no vistas en esta semana, y sus respectivos ejemplos de uso. (maximo 3)

Arboles binarios:
esta estructura es similar a arboles, pero al ser binaria solo admite dos enlaces que bien podrian ser dos nodos o enlaces vacios.
el primer nodo del arbol seria llamado raiz, el cual tendria dos hijos derecho e izquierdo, entonces cada hijo seria raiz de un subarbol
de cada nodo, siendo el hijo derecho(nodo) raiz del subarbol derecho y lo mimso con el izquierdo.
esta estructura siendo deribada de la estructura arbol tambien deriva la estructura arbol binario de busaqueda,arbol balanceado, estas variaciones
solo avrian en la impletacion de esta clase para obtener los resultados deceados

un arbol dinamicamente se veria de esta forma:
*                                                          5<-- nodo raiz                                           1er.-nivel
*                                                         /  \  
*hijoIzquierdo(nodo izquierdo,raiz suabarbol izquierdo)-->3     7<--hijoDerecho(nodo derecho,raiz suabarbol derecho)  2do.-nivel
*                                                        / \   / \ 
*                                                       1   4 6   8
*                                                            .
*                                                            .
*                                                            .
*                                       (esto seguira crecioendo de la misma forma)
                                      
en un arbol balanceado se evita que un subarbol sea mas largo que el otro con una toleracia maxima de un nivel de diferencia entre 
alturas de subarboles derecho e izquiero.

este seria el codigo de la estructura arbol binario en c#
esta solo es la estructura basica debido a que se req uieren mas metodos como mostrar un arbol inorden,postorden,preorden,
o eliminar nodos con diferentes variaciones como el caso de eliminar una raiz, la funcion de crera un arbol 
balanceado y verificar 
si esta balanceado, entre otros.

```c#
using System;
namespace ArbolBB
{
public class CArbolBB
{
#region *********************** Atributos *************************
private CArbolBB aSubArbolIzq;
private Object aRaiz;
private CArbolBB aSubArbolDer;
#endregion Atributos

#region ********************* Constructores ***********************
/* -------------------------------------------------------------- */
public CArbolBB()
{
aSubArbolIzq = null;
aRaiz = null;
aSubArbolDer = null;
}
/* -------------------------------------------------------------- */
public CArbolBB( CArbolBB pSubArbolIzq, Object pRaiz, CArbolBB pSubArbolDer)
{
aSubArbolIzq = pSubArbolIzq;
aRaiz = pRaiz;
aSubArbolDer = pSubArbolDer;
}
/* -------------------------------------------------------------- */
public static CArbolBB Crear()
{
return new CArbolBB();
}
/* -------------------------------------------------------------- */
public static CArbolBB Crear( CArbolBB pSubArbolIzq, Object pRaiz, CArbolBB pSubArbolDer)
{
return new CArbolBB(pSubArbolIzq, pRaiz, pSubArbolDer);
}

#endregion Constructores
#region ********************* Propiedades ***********************
/* ---------------------------------------------------------- */
public CArbolBB SubArbolIzq
{
get
{
return aSubArbolIzq;
}
set
{
aSubArbolIzq = value;
}
}
/* ---------------------------------------------------------- */
public object Raiz
{
get
{
return aRaiz;
}
set
{
aRaiz = value;
}
}
/* ---------------------------------------------------------- */
public CArbolBB SubArbolDer
{
get
{
return aSubArbolDer;
}
set
{
aSubArbolDer = value;
}
}

#endregion Propiedades
#region *********************** Metodos *************************
/* -------------------------------------------------------------- */
public bool EstaVacio()
{
// completar código
}
/* -------------------------------------------------------------- */
public virtual void Agregar( object Elemento)
{
if (aRaiz == null)
{
aRaiz = Elemento;
}
else
if (Elemento.ToString().CompareTo(aRaiz.ToString())<0)
{
if (aSubArbolIzq == null)
aSubArbolIzq = new CArbolBB(null,Elemento,null);
else
aSubArbolIzq.Agregar(Elemento);

}
else
{
if (aSubArbolDer == null)
aSubArbolDer = new CArbolBB(null,Elemento,null);
else
aSubArbolDer.Agregar(Elemento);

}

}

```
## 2. Problema (Usar pilas)
## este codigo lo hice en c# compilenlo y saldra la pila de respuesta genera a partir de la pila dada
```c#
class Program
	{
		static void imprimePila(Stack<int> pila)
		{
			Stack<int> s = pila;
			while (s.Count>0)
			{
				Console.WriteLine(s.Pop());
			}
		}
		static void comparar(Stack<int> pila, Stack<int> aux,Stack<int> respuesta)
		{
			int var = pila.Peek();
			pila.Pop();
			while (pila.Count > 0)
			{
				if (pila.Count == 0)
				{
					break;
				}
				aux.Push(pila.Peek());
				if (var < pila.Peek())
				{
					respuesta.Push(pila.Pop());
					break;
				}
				else
				{
					pila.Pop();
					if (pila.Count() > 0)
					{
						aux.Push(pila.Peek());
					}
				}
			}
		}
		static void apilar(Stack<int> pila, Stack<int> aux)
		{
			while (aux.Count > 0)
			{
				int var = aux.Pop();
				pila.Push(var);
			}
		}
		static void Main(string[] args)
		{
			int n = int.Parse(Console.ReadLine());
			// ponemos cantidad de elementos en n
			Stack<int> pila = new Stack<int>();
			for (int k = 0; k < n; k++)
			{
				//ponemos elementos a la pila
				pila.Push(int.Parse(Console.ReadLine()));
			}
			//creamos otra pila
			Stack<int> aux = new Stack<int>();
			Stack<int> respuesta = new Stack<int>();
			while (n > 0)
			{
				comparar(pila, aux, respuesta);
				if (pila.Count() == 0)
				{
					respuesta.Push(-1);
				}
				apilar(pila, aux);
				n--;
			}
			Stack < int > respuestaNueva = new Stack<int>();
			apilar(respuestaNueva, respuesta);
			//imprime la pila que genera la primera pila osea la pila de respuesta de SGE
			imprimePila(respuestaNueva);
			Console.ReadKey();
		}
	}
```
5
Dada un vector, imprima el Siguiente Gran Elemento (SGE) para cada elemento. El siguiente elemento mayor para un elemento x es el primer elemento mayor en el lado derecho de x en el conjunto. Elementos para los que no existe un elemento mayor, considere el siguiente elemento más grande como -1.
6
 
7
Ejemplos: 
8
* Para cualquier vector, el elemento situado más a la derecha siempre tiene el siguiente elemento más grande como -1. 
9
* Para un vector ordenado en orden decreciente, todos los elementos tienen el siguiente elemento más grande como -1. 
10
* Para el vector de entrada {4, 5, 2, 25}, los siguientes elementos mayores para cada elemento son los siguientes.
11
Siguiente Gran Elemento:
12
```c++
13
   4 - 5
14
   5 - 25
15
   2 - 25
16
   25 - -1
17
```
18
* Para el vector de entrada {13, 7, 6, 12}, los siguientes elementos mayores para cada elemento son los siguientes.
19
Siguiente Gran Elemento:
20
```c++
21
   13 - -1
22
   7 - 12
23
   6 - 12
24
   12 - -1
25
```
@alvarorcu
Como entregar el reto
17 days ago
26
