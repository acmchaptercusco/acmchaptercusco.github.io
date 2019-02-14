---
layout: post
title: CusContest XV
subtitle: 8 DE FEBRERO
bigimg: /img/banner-cuscontest.png
image: /img/CCXV-bold.jpg
tags: [cuscontest]
---

## Problemset

<iframe src="https://app.box.com/embed/s/yuipgijnb06o6g789deu8grve0du4k70?sortColumn=date&view=list" width="730" height="670" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

1. [Problema A. Noé y la barca](#problema-a-noé-y-la-barca)
2. [Problema B. La travesía de Jarencio](#problema-b-la-travesía-de-jarencio)
3. [Problema C. El último rey](#problema-c-el-último-rey)
4. [Problema D. Tarkin (Fácil)](#problema-d-tarkin-fácil)
5. [Problema E. Tarkin (Difícil)](#problema-e-tarkin-difícil)
6. [Problema F. Traducción de nokia a humano](#problema-f-traducción-de-nokia-a-humano)
7. [Problema G. Shaggy Overpowered y las Scooby Galletas](#problema-g-shaggy-overpowered-y-las-scooby-galletas)
8. [Problema H. Detección de manos](#problema-h-detección-de-manos)
9. [Problema I. Chusky El Aventurero (Medio)](#problema-i-chusky-el-aventurero-medio)
10. [Problema J. Chusky El Aventurero (Difícil)](#problema-j-chusky-el-aventurero-difícil)
11. [Problema K. Kyber](#problema-k-kyber)
12. [Problema L. Berthincio y su quinua](#problema-l-berthincio-y-su-quinua)

### Problema A. Noé y la barca

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/kkc8qs0hsrhfwkw8ogkagpqo9z88q2x3?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
	El problema pide determinar el pareo de animales, es decir, cuantas veces aparece un determinado animal y de acuerdo a ello tomar la decision de aumentar el contador de animales a ser expulsados o el contador de animales sin pareja.
    Para resolver el probleam se puede optar por usar un diccionario de palabras y numeros, o una table hash. Dados los limites del problema, cualquiera de los dos enfoques ser\'a aceptado.
* **Código en Python**
```python
num_casos = int(input())
for ith_caso in range(1, 1 + num_casos):
    n = int(input())
    names = dict()
    for i in range(n):
        name = input()
        if name in names:
            names[name] += 1
        else:
            names[name] = 1

    kick = 0
    miss = 0
    for count in names.values():
        if count == 1:
            miss += 1
        elif count > 2:
            kick += count - 2

    print ('Caso #%d: %d %d' % (ith_caso, kick, miss))
```

### Problema B. La travesía de Jarencio

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/569pwk1mln6h2skpx9g5ml2hflakmwe9?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
    Pueda que al inicio el problema parezca uno de simulaci\'on donde se deba inferir la energ\'ia inicial para recorrer todo el trayecto. Sin embargo, dado que para bajadas Jarencio gana puntos de energ\'ia, s\'olo debemos de preocuparnos de las subidas.

    Despu\'es de subir a un punto alto se habr\'a gastado $$K$$ de energ\'ia, y de alli se pueden tomar dos decisiones: a) Subir a un punto m\'as alto, o b) Descender a un punto bajo donde se gane energ\'ia. Si el caso a) llega a pasar, el valor inicial de energ\'ia que Jarencio debe de tener necesita ser aumentado, si el caso b) ocurre, simplemente el valor inicial de energ\'ia queda sin modificaci\'on. Similarmente, se puede tomar la misma decisi\'on para cada punto de tal forma que, para generalizar, la respuesta ser\'a la diferencia entre el punto m\'as elevado y el punto inicial de Jarencio.
* **Código en Python**
```python
num_casos = int(input())
for ith_caso in range(1, 1 + num_casos):
    input()
    numbers = [int(x) for x in input().split()]
    print ('Caso #%d: %d' % (ith_caso, max(0, max(numbers) - numbers[0])))
```

### Problema C. El último rey

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/58fxy8xmlx0l80v2g3lgoeotfr8inqo4?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
    El problema se puede resolver determinando si los alfiles atacan al rey blanco o no. Sin embargo, el hecho de tener la presencia del rey negro dificulta un poco el problema porque tambien debe de ser considerado el caso en donde un alfil est\'e atacando al rey blanco pero el rey negro se interponga y de cierta forma lo proteja.

    Un punto a considerar para resolver el problema es interpretar el input y tambi\'en convertir la notaci\'on de posiciones hacia coordenadas en el espacio.

* **Código en Python**
```python
def convertPosition(position):
    row = ord(position[0]) - ord('A') + 1
    col = int(position[1])
    return (row, col)
num_casos = int(input())
for ith_caso in range(1, 1 + num_casos):
    n = int(input())
    white_king = None
    black_king = None
    bishops = []
    for _ in range(n):
        piece, color, position = input().split()
        if piece == 'Alfil':
            bishops.append(convertPosition(position))
        elif color == 'blanco':
            white_king = convertPosition(position)
        else:
            black_king = convertPosition(position)
    num_checks = max(abs(white_king[0] - black_king[0]),
                     abs(white_king[1] - black_king[1])) == 1
    for bishop in bishops:
        if abs(bishop[0] - white_king[0]) == abs(bishop[1] - white_king[1]):
            if (bishop[0] - black_king[0]) == (black_king[0] - white_king[0]) and \
                    (bishop[1] - black_king[1]) == (black_king[1] - white_king[1]):
                continue
            else:
                num_checks += 1
    print ('Caso #%d: %s' % (ith_caso, 'Si' if num_checks > 0 else 'No'))
```

### Problema D. Tarkin (Fácil)

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/tdzg6y7vs1d3tx78u8n7805mvrlmxhdl?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
	Dados los límites del problema, es suficiente implementar el algoritmo *naive*. Complejidad: $$O(n^2)$$.
* **Código en Python**
```python
# Importar la librería math que contiene la
# función máximo común divisor (gcd)
import math
# Leer el número de casos de prueba
t = int(input())
# Procesar cada caso
for _ in range(t):
	# Leer 'n'
	n = int(input())
	# Iniciar la variable 'suma' en 0
	suma = 0
	# Iterar sobre 'i' y 'j'
	for i in range(1, n+1):
		for j in range(1, n+1):
			# Acumular la suma
			suma += math.gcd(i, j)
	# Mostrar el resultado
	print(suma)
```

### Problema E. Tarkin (Difícil)

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/22culy87vu6wlklryaa0vwfagmk2s52o?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
	El algoritmo utilizado en la versión fácil es muy lento para la versión difícil. En este caso, es útil visualizar el doble ciclo mediante una matriz (supongamos que $$n = 5$$):

	| | 1 | 2 | 3 | 4 | 5 |
	| :---: | :---: | :---: | :---: | :---: | :---: |
	| **1** | $$\text{mcd}(1, 1)$$ | $$\text{mcd}(1, 2)$$ | $$\text{mcd}(1, 3)$$ | $$\text{mcd}(1, 4)$$ | $$\text{mcd}(1, 5)$$ |
	| **2** | $$\text{mcd}(2, 1)$$ | $$\text{mcd}(2, 2)$$ | $$\text{mcd}(2, 3)$$ | $$\text{mcd}(2, 4)$$ | $$\text{mcd}(2, 5)$$ |
	| **3** | $$\text{mcd}(3, 1)$$ | $$\text{mcd}(3, 2)$$ | $$\text{mcd}(3, 3)$$ | $$\text{mcd}(3, 4)$$ | $$\text{mcd}(3, 5)$$ |
	| **4** | $$\text{mcd}(4, 1)$$ | $$\text{mcd}(4, 2)$$ | $$\text{mcd}(4, 3)$$ | $$\text{mcd}(4, 4)$$ | $$\text{mcd}(4, 5)$$ |
	| **5** | $$\text{mcd}(5, 1)$$ | $$\text{mcd}(5, 2)$$ | $$\text{mcd}(5, 3)$$ | $$\text{mcd}(5, 4)$$ | $$\text{mcd}(5, 5)$$ |

	El objetivo es obtener la suma $$\displaystyle \sum_{i=1}^n \sum_{j=1}^n \text{mcd}(i, j)$$. Dado que esta es una matriz simétrica, podemos deshacernos de la parte inferior. Los elementos de la diagonal tienen la forma de $$\text{mcd}(i, i)$$, siendo su valor $$i$$. Esto nos deja con la parte superior a la diagonal. A partir de ahora se considerará únicamente esta. Si tomamos la suma sobre una columna $$m > 1$$, esta es $$\displaystyle \sum_{i=1}^{m-1} \text{mcd}(i, m)$$. Nótese que esta suma está compuesta por divisores de $$m$$ que se irán repitiendo. Por lo tanto, esta se puede reescribir como $$\displaystyle \sum_{d \mid m} d\times f(m, d)$$ donde $$f(m, d)$$ indica la cantidad de valores desde $$1$$ hasta $$m-1$$ tal que su máximo común divisor con $$m$$ sea $$d$$. Esta función puede ser definida en términos de la [Función $$\varphi$$ de Euler](https://es.wikipedia.org/wiki/Funci%C3%B3n_%CF%86_de_Euler), que cuenta para un  entero $$n$$, la cantidad de valores desde $$1$$ hasta $$n$$ que son coprimos con $$n$$ (su máximo común divisor es $$1$$).

	**Ejercicio:** Demostrar que $$f(n, k) = \varphi(\frac{n}{k})$$ para enteros positivos $$k, n$$ con $$k\mid n$$.

	Con esto, la suma queda como $$\displaystyle \sum_{d \mid m} d \varphi(\frac{m}{d})$$. Es necesario calcular esta cantidad para cada columna. La función $$\varphi$$ puede ser precalculada para todos los valores $$\leq n$$ con una versión extendida de la [Criba de Eratóstenes](https://es.wikipedia.org/wiki/Criba_de_Erat%C3%B3stenes). Complejidad: Preprocesamiento: $$O(n\log \log n)$$, Consulta: $$O(1)$$.
* **Código en C++**
```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;
const int MAX = (int)1e6+5;
// Declarar los arreglos necesarios
int phi[MAX];
ll sum[MAX];
// Pre-calcular todas las respuestas ;v
void PreProcess(){
	// Iniciar los valores de phi y suma
	for(int i=1; i<MAX; i++){
		phi[i] = i;
		sum[i] = 0ll;
	}
	// Criba extendida para la función phi
	for(int i=2; i<MAX; i++)
		if(phi[i] == i){
			phi[i]--;
			// Iterar sobre los múltiplos de i
			for(int j=i+i; j<MAX; j+=i)
				phi[j] -= phi[j] / i;
		}
	// Calcular la suma de cada columna
	for(int i=1; i<MAX; i++)
		for(int j=i+i; j<MAX; j+=i)
			sum[j] += i * phi[j / i];
	// Acumular la suma total de columnas previas
	for(int i=3; i<MAX; i++)
		sum[i] += sum[i - 1];
	// Duplicar cada valor y sumar la diagonal
	ll diagonal = 0ll;
	for(int i=1; i<MAX; i++){
		diagonal += i;
		sum[i] = 2ll * sum[i] + diagonal;
	}
}
int main(){
	// Pre-procesar
	PreProcess();
	int te; scanf("%d", &te);
	while(te--){
		// Leer cada caso de prueba
		int n; scanf("%d", &n);
		// Dar la respuesta
		printf("%lld\n", sum[n]);
	}
	return 0;
}
```

### Problema F. Traducción de nokia a humano

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/y00g4m3opda744uolp0bfqfpompsqtz2?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
	Dependiendo del mensaje se debe hacer un tipo de traducción.
	Si el mensaje esta en caracteres alfabeticos simplemente es coger cada caracter y convertirlo a su correspondiente traducción en numeros y concantenarlos usando  el separador "|".
	Si el mensaje esta en caracteres numericos entonces se depe primero separar el mensaje usando como marca el caracter "|" y luego transformar cada sub cadena de numeros en su correspondiente letra.
* **Código en Python**
```python
# Creando un arreglo que contenga todos los
# caracteres escrtos con teclado numerico  
A = [str(i)*j for i in range(2, 10) for j in range(1, 4)]  
A.insert(18, '7777')
A.insert(25, '9999')
A.append('0')
# Creando un arreglo con letras de a-z mas el espacio  
B = [chr(i) for i in range(ord('a'), ord('z')+1)]
B.append(' ')
# Convirtiendo en dos diccionarios para hacer la traduccion
D1, D2 = dict(zip(A, B)), dict(zip(B, A))
n= int(input()) # Leer datos de entrada
for _ in range(n):
	t = input() # Tamaño del mensaje
	# Determinar de que tipo es el mensaje
	if t[0].isnumeric():
		t = t.split('|')
        r = "".join(D1[i] for i in t)
    else:
    	r = "|".join(D2[i] for i in t)
    print(r)
```

### Problema G. Shaggy Overpowered y las Scooby Galletas

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/u9rvpxj7bynu4caj4nkfwtnuf0e923mk?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>


	</details>
* **Solución:**

    Duplicar el número de Scooby Galletas $$S$$ en cada hora y solo aplicar la resta modular cuando la cantidad actual de $$S$$  sea mayor o igual a la cantidad máxima de galletas que Shaggy pueda requerir ($$2^{60}$$). Esto debido a que, además de evitar el overflow, si antes de duplicar el valor de $$S$$ en la $$i$$-ésima hora, $$S$$ es $$\geq 2^{60}$$, al duplicarlo, $$S$$ sería $$> 2^{60}$$ y de esta forma sin importar el valor de los siguientes $$c_i$$, $$S$$ nunca llegaría a ser un número negativo, porque en las siguientes horas su valor continuaría duplicándose. De esta forma Shaggy no tendrá que exclamar *zoinks!*.
 
    Si el caso anterior no se da, continuar duplicando el valor de $$S$$ y realizar la resta estándar entre $$S$$ y $$c_i$$ y verificar si el resultado es negativo.
    
    Finalmente la complejidad del algoritmo para cada $$n$$ es $$O(n)$$.

* **Código en C++**
```c++
#include <bits/stdc++.h>
using namespace std;
const int mod = (int)1e9 + 7;
inline long long sub(long long &a, long long b){
  a = (a - b) % mod;
  if(a < 0) a += mod;
}
void solve(){
	int n;
	cin >> n;
	vector<long long> v(n);
	for(int i = 0; i < n; i++){
		cin >> v[i];
	}
	bool available_forever = false;
	long long now = 1;
	for(int i = 0; i < n; i++){
		if(available_forever || now >= (1ll<<60)){
			now <<= 1;
			sub(now, v[i]);
			available_forever = true;
		} else {
			now <<= 1;
			now -= v[i];
			if(now < 0){
				cout << "zoinks!\n";
				return;
			}
		}
	}
	cout << now % mod << "\n";
}
int main(){
	ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int testcases;
	cin >> testcases;
	for(int t = 0; t < testcases; t++){
		solve();
	}
	return 0;
}
```

### Problema H. Detección de manos
* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/qt6gkw3a5od18091dwt18rhh984jbd0z?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
	Todos los caracteres que no nos sirvan para formar una mano los eliminamos y nos quedamos con las letras (''m', 'a', 'n', 'o') pero convertido a un nuermo que nosotros determinamos. Luego recorremos la matriz con un recuadro de tamaño 2x2 si los elementos dentro del recuadro suman lo mismo que la suma de los numeros de los caracteres para formar una mano entonces contamos. Esto se hace para no tener problemas con el orden de los caracteres.
* **Código en Python**
```python
from functools import reduce
t = int(input()) #lectura de datos  
M = {'m':2, 'a':4, 'n':8, 'o':16}  #Determinamos valores para los caracteres  
for _ in range(t):  
    n, m = map(int, input().split()) #lectura de datos  
  A = []  
    for i in range(n):  
        A.append(input())#lectura de datos  
  cont = 0  
  B = [[0 for _ in range(m)] for _ in range(n)] #creamos una matriz de 0's para recolocar los caracteres como numeros  
  for i in range(n):  
        for j in range(m):  
            if A[i][j] in M.keys(): B[i][j] = M[A[i][j]] #si los caracteres pueden formar una mano se almacenan como numero  
  
  for i in range(n-1):  
        for j in range(m-1):  
            cont += (30 == reduce(lambda x,y: x+y, B[i][j:j+2]+B[i+1][j:j+2])) #si el recuadro de 2x2 suma lo mismo que sumaria la imagen de una mano entonces contamos  
  print(cont)
```

### Problema I. Chusky El Aventurero (Medio)

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/lsfo1llq133ccejjjsng8293yzf1o50f?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>


	</details>
* **Solución 1:**
    El problema se puede resolver usando backtracking con memorización dados los limites pequeños. Sea $$solve(up, down, opt)$$ una función que reciba busque cuantas combinaciones se pueden lograr con $$up$$ movimientos hacia arriba, $$down$$ movimientos hacia abajo, y $$opt$$ nos indique si debemos ir hacia arriba o hacia abajo. Entonces; si, por ejemplo, $$up=5,~ opt=True$$ quiere decir que podemos subir $$k$$ niveles, donde $$k$$ varia entre $$1$$ y $$5$$ niveles. Luego, como hemos subido debemos de bajar un numero similar de niveles, entonces llamaremos a la funcion $$solve(up - k, down + k, False)$$. Similarmente, el mismo procedimiento funciona cuando descendemos. Finalmente, el caso base queda definido cuando $$up$$ y $$down$$ son iguales a $$0$$ (indicando que ya no hay energia suficiente ni para subir o bajar.

    Por lo tanto, nuestra funcion queda como:
    
    $$
    solve(up, down, opt) = \left\{\begin{matrix}
    up==0 \& down == 0&, &1 &//&~ Caso~ base\\
    opt  == True&, & \sum_{i=1}^{up}{solve(up - i, down + i, False)} &//&~ Caso~ recursivo\\ 
    opt ==  False&, & \sum_{i=1}^{down}{solve(up, down - i, True)} &//&~ Caso~ recursivo
    \end{matrix}\right.
    $$

	El unico punto a considerar ahora es ir guardando los resultados previamente calculados en un array tri-dimensional o un diccionario. Al usar memorizacion, nos evitamos de realizar calculos que ya hayamos hecho previamente.

* **Código en Python** *

```python
memo = dict()

def solve(up, down, opt):
    if up == down == 0:
        return 1

    if (up, down, opt) in memo:
        return memo[(up, down, opt)]

    ans = 0
    if opt:
        ans = sum(solve(up - i, down + i, not opt)
                  for i in range(1, up + 1))
    else:
        ans = sum(solve(up, down - i, not opt)
                  for i in range(1, down + 1))

    memo[(up, down, opt)] = ans
    return ans

t = int(input())
for _ in range(t):
    n = int(input())
    print (solve(n, 0, True))
```

* **Solución 2:**
	
	La solución al problema para cada $$n$$ es igual a su [Número de Catalan](https://es.wikipedia.org/wiki/N%C3%BAmeros_de_Catalan): $$Cat(n)$$. La definición original es:

	$$ Cat(n) = \frac{1}{n + 1}\binom{2n}{n} $$

	**Ejercicio:** Demostrar que esto es cierto.

	Para una implementación más simple podemos usar la relación entre el $$Cat(n)$$ y $$Cat(n + 1)$$:

	$$ Cat(n + 1) = \frac{(2n + 2)(2n + 1)}{(n + 2)(n + 1)} Cat(n) $$

	Así, podemos crear una funcion $$num(n)$$ que calcule $$(2n + 2)(2n + 1)$$, otra función $$den(n)$$ que calcula $$(n + 2)(n + 1)$$. Luego se pre-calcular todos los $$cat(n)$$ en un arreglo.

	Finalmente, la complejidad del algoritmo para cada $$n$$ es $$O(1)$$, como el número de casos $$t$$ y $$n$$ son pequeños, la complejidad final sigue siendo $$O(1)$$ ;)

	Una pequeño detalle al multiplicar $$num(n)Cat(n - 1)$$, éste valor general un overflow para enteros de 32 bits, por lo que es necesario considerar usar enteros de 64 bits para este processo.

* **Código en C++**
```c++
#include <bits/stdc++.h> 
using namespace std;
int cat[19];
int num(int x){
    return (2 * x + 2) * (2 * x + 1);
}
int den(int x){
    return (x + 2) * (x + 1);
}
void precompute(){
    cat[0] = 1;
    for(int i = 1; i < 19; i++){
        cat[i] = (1ll * cat[i - 1] * num(i)) / den(i);
    }
}
int main(){
    precompute();
    int test;
    scanf("%d", &test);
    while(test--){
        int x;
        scanf("%d", &x);
        printf("%d\n", cat[x - 1]);
    }
}
```

### Problema J. Chusky El Aventurero (Difícil)

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/1e8x989egmwzhodsaznowbha9aadixkj?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**

	Considerando la solución de la [versión mas simple](#problema-chusky-el-aventurero-medio) de este problema se puede ver que el problema pide calcular $$Cat(n)\text{ mod }(10^9 + 7)$$. Podria seguir usandose la solución anterior pero la función $$Cat(n)$$ crece muy rápido, así, es necesario aplicar la operación $$\text{ mod }(10^9 + 7)$$ a medida que se van calculando los valores.

	Antes de seguir es necesario recordar que la operación $$\text{ mod }$$ es [distributiva respecto a la suma y a la multiplicación](https://math.stackexchange.com/questions/147140/what-are-the-properties-of-the-modulus). Así, el producto de $$num(n)Cat(n - 1)$$ puede ser calculado evitando overflows aplicando $$mod$$ cada vez que sea necesario. La parte más complicada podria presentarse para el caso de $$den(n)$$, no es posible aplicar directamente $$den(n)~\text{ mod } (10^9 + 7)$$ porque esto genera resultados erroneos. Basandonos en la teoría de la aritmética modular se puede ver que es necesario calcular el **inverso modular** $$inv(den(n))$$.

	Así se reformula la equación:

	$$ 	Cat(n + 1) = (num(n) inv(den(n)) Cat(n))~mod~(10^9 + 7) $$

	Existen [varias formas](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/) para calcular el inverso modular, en este caso como $$10^9 + 7$$ es un primo, sabemos que el inverso existe y podemos hacer uso del [Pequeño Teorema de Fermat](https://es.wikipedia.org/wiki/Peque%C3%B1o_teorema_de_Fermat):

	$$ 	inv(den(n)) = den(n)^{(10^9 + 7) - 2}~\text{ mod }~(10^9 + 7) $$

	Para calcular esta potencia es necesario usar una implementación rapida de exponeciacion que use las propiedades del $$\text{ mod }$$ para evitar overflows. En la solución presentada la exponeciación tiene complejidad de $$O(\log (10^9 + 7)) = O(31) = O(1)$$.

	Finalmente, podemos usar la misma idea de pre-calcular $$Cat(n)$$ en un arreglo, así la complejidad para cada $$n$$ sigue siendo $$O(1)$$, en este problema el caso de pruebas $$t$$ es significativo por lo que la complejidad final es $$O(t)$$.
	
* **Código en C++**
```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long int i64;
const i64 MOD = 1000000007;
const int limit = 1000001;
int cat[limit];
i64 num(i64 x){
    return (((2ll*x)%MOD + 2ll)*((2ll*x)%MOD + 1ll))%MOD;
}
i64 den(i64 x){
    return ((x + 2ll)*(x + 1ll))%MOD;
}
i64 fast_pow(i64 x, i64 pow){
    if (pow == 0) return 1;
    if (pow == 1) return x;
    if (pow % 2ll == 0ll){
        i64 prod = fast_pow(x, pow / 2ll);
        return (prod * prod) % MOD;
    } 
    else{
        i64 prod = fast_pow(x, pow / 2ll);
        return (((prod * prod) % MOD) * x) % MOD;
    }
}
i64 inverse(i64 x){
    //because MOD is prime, we can use Fermat's little theorem
    return fast_pow(x, MOD - 2);
}
void precompute(){
    cat[0] = 1;
    for(int i = 1; i < limit; i++){
        i64 ans = (1ll*cat[i-1] * num(i)) % MOD;
        ans = (ans * inverse(den(i))) % MOD;
        cat[i] = (int)(ans);
    }
}
int main(){
    precompute();
    int test;
    scanf("%d", &test);
    while(test--){
        int x;
        scanf("%d", &x);
        printf("%d\n", cat[x - 1]);
    }
}
```

### Problema K. Kyber

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/nhtlmp8no0bwyzzii1jfvu7pqei5ll0k?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
	Cuando la gravedad es redireccionada, la distribución final de las cajas genera una representación que corresponde con la representación inicial ordenada.
	
	**Ejercicio:** Demostrar que esto es cierto.

	Complejidad: $$O(n\log n)$$.
* **Código en Python**
```python
# Leer cada caso de prueba
for _ in range(int(input())):
	n = int(input())
	# Leer el arreglo
	A = [int(x) for x in input().split(" ")]
	# Ordenarlo
	A.sort()
	# Imprimirlo con espacios entre elementos
	print(*A)
```

### Problema L. Berthincio y su quinua

* <details>
	<summary>Descripción del Problema (clic para ver)</summary>

	<iframe src="https://app.box.com/embed/s/ka7ecj6axcplpa24ilvxeyk4vexd4xgl?sortColumn=date&view=list" width="730" height="470" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>

	</details>
* **Solución:**
	Este es un problema bastante conocido llamado [Maximum subarray sum](https://en.wikipedia.org/wiki/Maximum_subarray_problem). Existen muchos algoritmos para resolverlo. El más obvio y trivial es iterar sobre cada subarreglo y calcular su suma. Luego devolver la máxima suma sobre todos los posibles sub arreglos La complejidad de esta solución es $$O(n^3)$$, puede ser implementada en $$O(n^2)$$ si se guardan las sumas acumuladas. Existe [otro algoritmo](https://www.geeksforgeeks.org/maximum-subarray-sum-using-divide-and-conquer-algorithm/) de divide and conquer muy interesante que logra una complejidad de $$O(n\log n)$$. Sin embargo, la forma más eficiente de resolverlo, es un [algoritmo](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/) de programación dinámica. Este algoritmo se explica a continuación:


	Para cada posición del arreglo, se deben conocer dos valores. Primero, el valor $$\text{max_aqui}(i)$$, que representa la máxima suma del mejor subarreglo que termina en la posición $$i$$. Segundo, $$\text{max_total}(i)$$, la solución óptima del arreglo contando hasta la posición $$i$$. Para calcular el primer valor, en cada posición lo actualizamos de la siguiente manera: dado que $$\text{max_aqui}(i)$$ requiere de $$A[i]$$, tomamos el máximo entre $$A[i]$$ y $$\text{max_aqui}(i-1) + A[i]$$. Finalmente, para calcular $$\text{max_total}(i)$$, tomamos el máximo entre $$\text{max_aqui}(1), \text{max_aqui}(2), \dots, \text{max_aqui}(i-1), \text{max_aqui}(i)$$. La solución al problema es $$\text{max_total}(n)$$.
	Complejidad: $$O(n)$$.
* **Código en Python**
```python
# Leer cada caso de prueba
for _ in range(int(input())):
	n = int(input());
	# Leer el arreglo
	A = [int(x) for x in input().split(' ')];
	# Iniciar las variables máximo hasta aquí y máximo total
	max_aqui, max_total = 0, 0;
	for i in range(n):
		# Con cada posición del arreglo, actualizar las variables
		max_aqui = max(A[i], A[i] + max_aqui);
		max_total = max(max_total, max_aqui);
	# Imprimir el máximo total
	print(max_total);
```
