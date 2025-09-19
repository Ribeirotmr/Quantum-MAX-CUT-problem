# Quantum Max-Cut e QAOA

## Introdução

O problema **Max-Cut** consiste em dividir os vértices de um grafo $G = (V, E)$ em dois conjuntos não vazios $S$ e $\overline{S}$ de forma a **maximizar a soma dos pesos das arestas que conectam vértices de conjuntos diferentes**.

Formalmente, queremos:

$$
\text{cut}(S, \overline{S}) = \sum_{(i,j) \in E} w_{ij} \cdot \delta(x_i \neq x_j)
$$

onde:
- $w_{ij}$ é o peso da aresta $(i,j)$,
- $x_i$ indica o conjunto ao qual o vértice $i$ pertence,
- $\delta(x_i \neq x_j)$ é 1 se os vértices estão em conjuntos diferentes e 0 caso contrário.

---

## Por que transformar para matriz de adjacência?

Para aplicar algoritmos clássicos e quânticos, como **QAOA**, precisamos **representar o grafo em uma forma matricial direta**, pois:
- Permite cálculos eficientes,
- É a base para construir a **função objetivo**,
- Serve como entrada para gerar o **Hamiltoniano quântico**.

No entanto, muitas vezes os dados vêm em **formato de lista de arestas**, por exemplo:

$$
M = \begin{bmatrix}
1 & 2 & 3 \\
2 & 3 & 4 \\
3 & 4 & 1
\end{bmatrix}
$$

Cada linha significa: **(vértice $i$, vértice $j$, peso)**.

---

## Como transformar matematicamente?

Se temos $n$ vértices, a matriz de adjacência $A$ é uma matriz $n \times n$ definida por:

$$
A[i][j] =
\begin{cases}
w_{ij}, & \text{se existe aresta } (i,j) \\
0, & \text{caso contrário}
\end{cases}
$$

Exemplo:  
Para \( n = 4 \) e arestas:
- (1, 2) com peso 3
- (2, 3) com peso 4
- (3, 4) com peso 1

A matriz resultante será:

$$
\begin{bmatrix}
0 & 3 & 0 & 0 \\
3 & 0 & 4 & 0 \\
0 & 4 & 0 & 1 \\
0 & 0 & 1 & 0
\end{bmatrix}
$$

**Por que isso é importante para o computador quântico?**

O computador quântico precisa "entender" a estrutura do problema. A matriz de adjacência é como um mapa de relacionamentos que mostramos para o algoritmo quântico, dizendo: "Olha, estas são as conexões que importam!"

**O que é o hamiltaniano na coputação quântica?** 
O Hamiltaniano é um operador $H$ que mede a energia total do sistema quântico 

No meu algoritimo eu usei dois hamiltaninano.

* 1- Hamiltaniano de custo
* 2- Hamiltaniano de mistura


## Hamiltaniano de custo: 
Na computação quântica, o Hamiltoniano de Custo $H_C$ é um operador construído matematicamente para codificar a essência de um problema de otimização na linguagem da mecânica quântica. Ele associa um valor de energia a cada solução possível, de forma que o estado de menor energia (o estado fundamental) represente a solução ótima que buscamos.

$H_C$ definido para o problema MAX-CUT:

$$
H_C = \frac{1}{2} \sum_{(i,j) \in E} (I - Z_i Z_j) 
$$

Onde: 
* $E$ conjunto de arestas do grafo.
* $I$ é a matriz identidade.
* $Z_i$ e $Z_j$ são operadores de Pauli-Z que agem nos qubits i e j, respectivamente. Esses operadores servem para codificar a partição dos vértices: se o qubit correspondente a um vértice está no estado ∣0⟩ ou ∣1⟩, isso determina o subconjunto ao qual o vértice pertence.


## Hamiltaniano de mistura: 
O hamiltaniano de mistura $H_C$ ele é o "empurrão quântico" que evita que a busca fique travada em soluções ruins e explora o espaço de forma inteligente, usando superposição e emaranhamento.

$H_M$ definido para o problema MAX-CUT:

$$
H_M = \sum_{i=1}^{N} X_i 
$$

* $N$ é o número de quibits
* $X_i$ é o operador de Pauli-X que age no qubit $i$. O operador de Pauli-X tem a propriedade de "virar" o estado de um qubit, transformando ∣0⟩ em ∣1⟩ e vice-versa. Quando $H_M$ é aplicado, ele cria uma superposição de todos os estados de base computacional. O sistema quântico não está mais em um único estado, mas sim em uma combinação linear de todos os estados possíveis, o que permite a exploração do espaço de soluções.


  


## Referências

1. Farhi, E., Goldstone, J., & Gutmann, S. (2014). A Quantum Approximate Optimization Algorithm. arXiv:1411.4028.
2. Qiskit Documentation: Quantum Approximate Optimization Algorithm
3. Lucas, A. (2014). Ising formulations of many NP problems. Frontiers in Physics, 2, 5.

---
