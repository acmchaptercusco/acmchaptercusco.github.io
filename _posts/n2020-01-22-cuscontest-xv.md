---
layout: post
title: CusContest XV
subtitle: XX DE FEBRERO
bigimg: /img/ml-seminar.png
tags: [cuscontest]
---

# Scoreboard
### General
### Principiantes
### Intermedios
### Avanzados

# Problemset

### Problem G. El viaje de Adam <a id="Problem-G"/>

* Dadas $$N+1$$ ciudades y sea $$A=\{a_1, a_2, \dots, a_N \}$$ un conjunto tal que $$a_i$$ indica el número de caminos de la $$i$$-ésima ciudad a la ciudad $$i+1$$. El problema nos piden contar el número de caminos posibles que hay desde la ciudad $$1$$ hasta la ciudad $$N+1$$, sin embargo dado que dicho número puede ser muy grande ($$10^{9000}$$ en el peor de los casos), sólo debemos de mostrar el primer y último dígito.
* Sea $$P$$ el número de caminos posibles entras las ciudades $$1$$ y $$N+1$$, y $$K$$ el número de dígitos que tiene $$P$$:

  El primer dígito de $$P$$ será igual a:
  \begin{equation}
    d_{\text{digito}}^{\text{1er}} = \frac{P}{10^{K-1}} \label{eqG:1}
  \end{equation}
  y el último dígito será 
  \begin{equation}
    d_{\text{digito}}^{\text{ult}} = P \mod 10 \label{eqG:2}
  \end{equation}
  donde:
  \begin{align}
    P &= \prod_{i=1}^{N}{a_i} \label{eqG:P}\cr
    K &= 1 + \lfloor{\log_{10}(P)}\rfloor \label{eqG:K}
  \end{align}
* Por lo consiguiente, el problema consta de 2 sub-problemas: 

  1. **Obtener el primer dígito de $$P$$**

      Expresando \eqref{eqG:1} en términos de logaritmos, tenemos:

      \begin{equation}
        \begin{split}
          d_{\text{digito}}^{\text{1er}} &= e^{\log\({\frac{P}{10^{K-1}}}\)}   \cr
                                         &= e^{\log(P) - \log(10^{K-1})} \cr
                                         &= e^{\log(P) - (K-1)\log(10)}
        \end{split}
        \label{eqG:1log}
      \end{equation}
      del mismo modo con $$P$$, sea $$S=\log(P)$$ entonces:
      \begin{equation}
        P = e^{\log(P)} = e^{S} \label{eqG:logP}
      \end{equation}
      Reemplazando \eqref{eqG:logP} en \eqref{eqG:1log}:
      \begin{equation}
        \begin{split}
          d_{\text{digito}}^{\text{1er}} &= e^{\log(P) - (K-1)\log(10)}    \cr
                                         &= e^{\log(e^{S}) - (K-1)\log(10)}\cr
                                         &= e^{S - (K-1)\log(10)}
        \end{split}
        \label{eqG:1f}
      \end{equation}
      $$K$$ también puede ser representado mediante:
      \begin{equation}
        K = 1 + \lfloor{\sum_{i=1}^{N}{\log_{10}{(a_i)}}}\rfloor \label{eqG:K2}
      \end{equation}
      y aplicando propiedades de logaritmos en \eqref{eqG:P}:
      \begin{equation}
        S = \log{\(\prod_{i=1}^{N}{a_i}\)} = \sum_{i=1}^{N}{(\log(a_i))} \label{eqG:S}
      \end{equation}

      Finalmente, dado que $$d_{\text{digito}}^{\text{1er}}$$ es un número flotante, pero a nosotros únicamente nos interesa saber la parte entera, el primer dígito de $$P$$ será:
      \begin{equation}
        d_{\text{digito}}^{\text{1er}} = d_{\text{digito}}^{\text{1er}} - (d_{\text{digito}}^{\text{1er}} \mod 1)
      \end{equation}

  2. **Obtener el último dígito de $$P$$**
  
      Dado que la operación módulo por derecha es distributida con respecto a la multiplicación, es decir $$(A\cdot B) \mod M = ((A \mod M) \cdot (B \mod M)) \mod M$$, para obtener $$d_{\text{digito}}^{\text{ult}}$$ usaremos los valores de $$a_i \mod 10$$. Es importante realizar la operación módulo en cada iteración para la obtención del último dígito dado que en algún instante podríamos estar en un caso de *overflow* dados los límites de un número entero de 32 bits (ver código para mejor aclaración).

* Código en Python:

```python
# Importar libreria math que contiene la funcion log, log10, floor, y el valor
# de e (neperiano)
import math

# Leer T (número de casos de prueba)
T = int(raw_input())
# Procesar cada caso
for iT in xrange(T):
  # Leer N (número de ciudades - 1)
  N = int(raw_input())
  # Leer A (el número de caminos entre ciudades) 
  A = map(int, raw_input().split(' '))

  # Primer subproblema: primer dígito de P
  # Calcular S
  S = sum(map(math.log, A))
  # Calcular K
  K = 1 + math.floor(sum(map(math.log10, A)))
  # Calcular el primer digito
  p_dig = math.e ** (S - (K - 1) * math.log(10))
  # Obtener la parte entera de p_dig
  p_dig = int(p_dig - (p_dig % 1))

  # Segundo subproblema: ultimo digito de P
  # Obtener el ultimo digito usando la propiedad distributiva por derecha del
  # modulo para la multiplicacion
  u_dig = 1
  for a_i in A:
    u_dig = (u_dig * (a_i % 10)) % 10

  # Mostrar los resultados
  print p_dig, u_dig
```

### Problem H. Un viaje de ensueño <a id="Problem-H"/>

* Se tiene un omnibus con una velocidad constante $$v_o$$ que parte de un punto de inicio $$P$$ y al cabo de un tiempo, un taxi con una velocidad constante $$v_t$$ parte desde el mismo punto de inicio $$P$$ para intentar alcanzar al omnibus que ya se encuentra a una distancia $$d$$ de $$P$$.
* El problema nos pide averguar si el taxi podrá alcanzar al omnibus, si es así mostrar el tiempo que demorará y caso contrario mostrar $$-1$$.
* Suponiendo que existe un punto $$D$$ en el que el taxi logra a alcanzar al omnibus en un tiempo $$T$$, entonces las siguientes relaciones (considerando el movimiento rectilíneo uniforme) tanto para el omnibus como para el taxi tenemos:
\begin{align}
  D &= d + v_o T \label{eqH:Domn} \cr
  D &= v_t T \label{eqH:Dtaxi}
\end{align}

  Reemplazando \eqref{eqH:Dtaxi} en \eqref{eqH:Domn}:
\begin{equation}
\begin{split}
  v_t T &= d + v_o T \cr
  (v_t - v_o) T &= d \cr
  T &= \frac{d}{v_t - v_o}
\end{split}
\label{eqH:sol}
\end{equation}

  Por lo tanto, si ambos vehículos llegan a encontrarse, estos lo harán después de un tiempo $$T$$.
* Dado que se ha partido de la supocisión que existe un punto de encuentro, se debe de cumplir:
\begin{equation}
  0 < v_t - v_o
\end{equation}
  Caso contrario, si dicha condición no se cumple, podemos deducir que el punto de encuentro no existe.

* Código Python:

```python
# Leer T (número de casos de prueba)
T = int(raw_input())
# Procesar cada caso
for iT in xrange(T):
  # Leer v_t, v_o, y d (velocidad del taxi, velocidad el omnibus, y la distancia
  # entre el punto inicial y el punto donde se encuentra actualmente el omnibus)
  v_t, v_o, d = map(int, raw_input().split(' '))
  # Determinar si existe punto de encuentro, y si es el caso, mostrar el tiempo
  # que demorará el taxi en alcanzar al omnibus
  if v_t - v_o <= 0:
    print "-1"
  else:
    print "%.10f" % (d * 1.0 / (vt - vo))
```