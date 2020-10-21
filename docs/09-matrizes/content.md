## Matrizes

---

## Objetivo da aula

Responder às seguintes perguntas:
- Como representar um conjunto de informação como uma matriz?
- Como representar uma tabela de dados em C++?
---

## Definições

Em C++, as matrizes podem ser:

_Unidimensionais_ (vetores)

_Multidimensionais_ (duas ou mais dimensões)

```cpp
// Declaração de uma matriz de duas dimensões 
// com 4 linhas e 3 colunas
int M[4][3];
```
---
## Armazenamento na memoria

<img src=mat3.png width=500 />
---
## Armazenamento na memoria

<img src=mat4.png width=300/>

---
### Acessar os elementos

Matrizes de duas dimensões são vetores em que os elementos são outros vetores.

Os elementos de uma matriz bidimensional são acessados com _indexação
dupla_: o primeiro índice acessa a _linha_ e o segundo acessa a
_coluna_.

Matrizes bidimensionais precisam de __duas estruturas de repetição__, uma para a
linha e outra para a coluna.

```cpp
// Examplo: armazenar valores na matriz M
int M[3][4];
for(i=0;i<3;i++){ // linhas
  for(j=0;j<4;j++){ // colunas
  cin  >> M[i][j];
 }
}
```
---
### Inicialização de matrizes

Temos várias alternativas: 

<img src=init.png width=700 />

__O número de colunas deve ser sempre fornecido__

---
### Exemplo1: Matriz Identidade

Escreva um programa que, dado um número $n<=30$, crie a matriz identidade
de dimensão $n$.

<img src=matid.png width=400/>

---
### Exemplo1: Matriz Identidade

Sempre utilizamos _constantes_ inteiras para declarar as matrizes
```cpp
#define TAM 30
```
Lógica do programa:

1. atribuir $1$ nas posições $i \equiv j$
2. atribuir $0$ nas posições $i\neq j$

---
### Exemplo1: Matriz Identidade

```cpp[1-10 | 11-19 | 21-27]
#include< iostream>
#define TAM 30

using namespace std;

int main(){
    int M[TAM][TAM];
    int i,j,n;
    cin >> n;

    // Matriz identidade
    for(i=0; i < n ; i++){
        for(j=0; j < n ; j++){
            if (i == j)
                M[i][j] = 1;
            else
                M[i][j] = 0;
        }
    }

    // Imprimir a Matriz
    for(i=0; i < n ; i++){
        for(j=0; j < n ; j++){
                cout << M[i][j] << " ";
        }
        cout << endl ;
    }

    return 0;
}
```
---
### Exemplo1: Matriz Identidade

Também podemos inicializar a matriz e só escrever os números 1s. 
```cpp[1-10 | 11-14 | 17-22 ]
#include< iostream>
#define TAM 30

using namespace std;

int main(){
    int M[TAM][TAM] = {}; // 0,0,0...0
    int i,j,n;
    cin >> n;

    // Matriz identidade
    for(i=0; i < n ; i++){
        M[i][i] = 1;
    }

    // Imprimir a Matriz
    for(i=0; i < n ; i++){
        for(j=0; j < n ; j++){
                cout << M[i][j] << " ";
        }
        cout << endl ;
    }

    return 0;
}
```

---
### Exemplo 2: Matriz Transposta

Dada uma matriz de dimensão $n\times m$, calcular e imprimir a 
_matriz transposta_. O usuário deve fornecer os tamanhos da matriz e, em seguida, os
elementos da matriz. Assuma que $m, n \leq 30$. 

<img src=mattr.png width=600 />

---
### Exemplo 2: Matriz Transposta

1. Criamos as duas matrizes $M$ e $MT$
2. Lemos as dimensões e os valores para $M$
3. Por cada posição $(i,j)$ de $M$, Atribuímos $MT[j][i] = M[i][j]$
4. Imprimimos $MT$

Note que se a dimensão de $M$ é  $n\times m$, então a dimensão de $MT$ é $m \times n$. 

---
### Exemplo 2: Matriz Transposta

```cpp[1-10|11-15|17-22|24-30]
#include < iostream>
#define TAM 30
using namespace std;

int main(){
    int M[TAM][TAM], MT[TAM][TAM];
    int i,j,n,m;

    cin >> n >> m;
    // Ler os valores da matriz
    for(i=0 ; i < n ; i ++){
        for(j=0 ; j < m ; j++){
            cin >> M[i][j];
        }
    }

    // Calcular a matriz transposta
    for(i=0 ; i < n ; i ++){
        for(j=0 ; j < m ; j++){
            MT[j][i] = M[i][j];
        }
    }

    // Imprimir MT
    for(i=0 ; i < m ; i ++){ // Número de linhas = m
        for(j=0 ; j < n ; j++){ // Número de colunas = n
            cout << MT[i][j] << " " ;
        }
        cout << endl;
    }
    return 0;
}
```

--- 
### Exemplo3: Procurar Elemento na Matriz 

Faça um programa que, dados $n,m <=30$, lê do usuário os valores de uma matriz $A$
de inteiros de dimensão $n \times m$. Depois, o programa deve ler um número x e
imprimir uma mensagem indicando se a matriz possui algum elemento cujo valor é
x.

---
### Exemplo3: Procurar Elemento na Matriz 

1. Ler as dimensões e os valores de $M$
2. Ler o número $x$
3. Percorrer a matriz:

 3.1: Se $M[i][j]==x$ então, sabemos que $x$ pertence à matriz

 3.2: Caso contrário, continuamos buscando

4. __Depois__ de percorrer _toda_ a matriz, imprimimos o resultado

Utilizaremos uma variável do tipo `bool` para saber se o elemento foi
encontrado ou não. 

---
### Exemplo3: Procurar Elemento na Matriz 

```cpp[1-10|11-17|19-25|26-29]
#include< iostream>
#define MAX 30

using namespace std;

int main()
{
    int n, m, x, A[MAX][MAX];
    bool achou = false;

    cin >> n >> m;

    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++)
            cin >> A[i][j];
    }
    cin >> x;

    // Buscar o elemento
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < m; j++) {
            if(x == A[i][j])
            	achou = true;
        }
    }
    if (achou)
    	cout << "Matriz tem elemento " << x << endl;
    else
    	cout << "Matriz não tem elemento " << x << endl;

    return 0;
}
```

---
### Exemplo3: Procurar Elemento na Matriz 

Se $x$ já foi encontrado, podemos terminar os laços

```cpp[1-10|11-17|19-29|30-34]
#include< iostream>
#define MAX 30

using namespace std;

int main()
{
    int n, m, x, A[MAX][MAX];
    bool achou = false;

    cin >> n >> m;

    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++)
            cin >> A[i][j];
    }
    cin >> x;

    // Buscar o elemento
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < m; j++) {
            if(x == A[i][j]){
            	achou = true;
                break;
            }
        }
        if(achou)
            break;
    }
    if (achou)
    	cout << "Matriz tem elemento " << x << endl;
    else
    	cout << "Matriz não tem elemento " << x << endl;

    return 0;
}
```
---
### Exemplo 4: Matriz com Borda

Determinar se todos os elementos internos da matriz são estritamente menores
que os elementos da borda da matriz. 

```
9 8 7 6
9 2 3 7
8 5 4 5
Sim!
```
```
1 1 1 1 1
1 0 0 0 1
1 0 1 0 1
1 0 0 0 1
1 1 1 1 1
Não!
```

---
### Exemplo 4: Matriz com Borda

1. Vamos calcular o menor elemento da borda
2. Note que os elementos da borda são:
-  $M[0][j]$: borda superior
-  $M[n-1][j]$: borda inferior
-  $M[i][0]$: borda esquedar
-  $M[i][m-1]$: borda direita

3. Depois, simplesmente comparamos os elementos internos com o menor elemento
da borda. 

---
### Exemplo 4: Matriz com Borda
```cpp[1-9|10-15|16-17|19-26|27-33|35-43|45-48]
#include< iostream>
#define TAM 30
using namespace std;

int main(){
    int M[TAM][TAM];
    int i,j,n,m;
    int min;

    cin >> n >> m ;

    for(i=0 ; i < n ; i++){
        for(j=0 ; j < m ; j++)
            cin >> M[i][j];
    }
    // Calcular o min da borda
    min=M[0][0];

    // Inferior e superior
    for(j=0 ; j < m ; j++){
        if (min > M[0][j])
            min = M[0][j];
        if (min > M[n-1][j])
            min = M[n-1][j];

    }
    // Direita e esquerda
    for(i=0 ; i < n ; i++){
        if (min > M[i][0])
            min = M[i][0];
        if (min > M[i][m-1])
            min = M[i][m-1];
    }

    // Determinar se os elementos internos são todos menores
    bool borda=true;
    for(i=1 ; i < n-1 && borda ; i++){
        for(j=1 ; j < m-1 ; j++)
            if(M[i][j] >= min){
                borda = false;
                break;
            }
    }

    if (borda)
        cout << "Todos os elementos da borda são maiores que os elementos internos";
    else
        cout << "Não todos os elementos da borda são maiores que os elementos internos";
}
```

---
## Teste!
<https://multiprova.ufrn.br/>
