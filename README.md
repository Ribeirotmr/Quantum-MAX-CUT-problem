# Quantum Max-Cut e QAOA

## Introdução

O problema **Max-Cut** consiste em dividir os vértices de um grafo \( G = (V, E) \) em dois conjuntos não vazios \( S \) e \( \overline{S} \) de forma a **maximizar a soma dos pesos das arestas que conectam vértices de conjuntos diferentes**.

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



## Referências

1. Farhi, E., Goldstone, J., & Gutmann, S. (2014). A Quantum Approximate Optimization Algorithm. arXiv:1411.4028.
2. Qiskit Documentation: Quantum Approximate Optimization Algorithm
3. Lucas, A. (2014). Ising formulations of many NP problems. Frontiers in Physics, 2, 5.

---
