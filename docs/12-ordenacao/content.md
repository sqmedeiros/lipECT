## Algoritmos de Ordenação 
### Parte I
---
### Motivação

Considere os seguintes problemas de vetores:
 - Buscar um elemento.
 - Determinar se existem elementos repetidos.
 - Determinar qual é o elemento com maior número de repetições (moda).

> Como solucionar eficientemente esses problemas  ?

---
### Motivação
Alguns problemas de vetores _são mais simples_ se considerarmos um vetor _ordenado_.

Muitas vezes precisamos ordenar os elementos de um vetor:
- Lista de frequência.
- Palavras no dicionário.
- Maiores notas em um concurso.

> Como ordenar eficientemente um vetor ?
---

### Objetivo da aula

Aprenderemos alguns _algoritmos de ordenação_.
- Bolha (Bubble sort)
- Ordenação por seleção (Selection sort)
- Ordenação por inserção (Insertion sort)
- Quick Sort (depois de ver funções _recursivas_).

> Utilizaremos algoritmos de ordenação para _resolver problemas_.
---

### Definições

__Ordenação__: Dado um vetor $v$ de dados, colocar os elementos de $v$ em uma
certa ordem (crescente / decrescente).

$ [4,1,8,3] \to [1,3,4,8] $

---
### Bubble Sort (Bolha)
Em cada iteração o maior elemento _flutua_ até a última posição.

---
### Bubble Sort (Bolha)

<img src=bbsort.png height=550/>

---

<iframe width="1186" height="667" src="https://www.youtube.com/embed/lyZQPjUT5B4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---
### Implementação de Bubble Sort

```cpp
// Trocar 2 posições no vetor
void swap(int v[], int p1, int p2){
  int temp;
  temp = v[p1];
  v[p1] = v[p2];
  v[p2] = temp;
}
```
---
### Implementação de Bubble Sort

```cpp
void bubble(int v[], int n){
  int i, j;
  for(i=n-1;i >= 1;i--){
    for(j=0 ; j < i ; j++){
      if(v[j] > v[j+1])
        swap(v,j,j+1);
    }
    print(v,TAM);
  }
}
```

---
### Implementação de Bubble Sort

```
[96 92 0 24 32 52 33 72 35 67 ]
[92 0 24 32 52 33 72 35 67 96 ]
[0 24 32 52 33 72 35 67 92 96 ]
[0 24 32 33 52 35 67 72 92 96 ]
[0 24 32 33 35 52 67 72 92 96 ]
[0 24 32 33 35 52 67 72 92 96 ]
[0 24 32 33 35 52 67 72 92 96 ]
[0 24 32 33 35 52 67 72 92 96 ]
[0 24 32 33 35 52 67 72 92 96 ]
[0 24 32 33 35 52 67 72 92 96 ]
```

---
### Selection Sort
Em cada iteração movemos  o menor elemento para a primeira posição.
---
### Selection Sort
<img src=selsort.jpg height=550/>

---
<iframe width="1186" height="667" src="https://www.youtube.com/embed/Ns4TPTC8whw" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---
### Implementação de Selection Sort

```cpp
void selection(int v[], int n){
  int i, j, min;
  for(i=0 ; i< n-1 ; i++){
    min = i;
    for(j=i+1 ; j < n ; j++){
      if(v[j] < v[min]) min = j;
    }
    swap(v,i,min);
    print(v,TAM);
  }
}

```
---
### Implementação de Selection Sort
```
[6 72 90 43 78 60 78 39 5 72 ]
[5 72 90 43 78 60 78 39 6 72 ]
[5 6 90 43 78 60 78 39 72 72 ]
[5 6 39 43 78 60 78 90 72 72 ]
[5 6 39 43 78 60 78 90 72 72 ]
[5 6 39 43 60 78 78 90 72 72 ]
[5 6 39 43 60 72 78 90 78 72 ]
[5 6 39 43 60 72 72 90 78 78 ]
[5 6 39 43 60 72 72 78 90 78 ]
[5 6 39 43 60 72 72 78 78 90 ]
```

---
### Insertion Sort
En cada iteração, o algoritmo vai deixando os elementos mais à esquerda ordenados 
---
### Insertion Sort
<img src=inssort.jpg width=600/>

---
<iframe width="1186" height="667" src="https://www.youtube.com/embed/ROalU379l3U" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---
### Implementação de Insertion Sort

```cpp
void insertion(int v[], int n){
  int i, j, min;
  for(i=1; i < n ;i++){
    for(j=i ; j > 0 ; j--){
      if(v[j] < v[j-1])
        swap(v,j,j-1);
      else break;
    }
    print(v,TAM);
  }
}
```
---
### Implementação de Insertion Sort

```
[14 13 82 69 50 3 62 73 66 34 ]
[13 14 82 69 50 3 62 73 66 34 ]
[13 14 82 69 50 3 62 73 66 34 ]
[13 14 69 82 50 3 62 73 66 34 ]
[13 14 50 69 82 3 62 73 66 34 ]
[3 13 14 50 69 82 62 73 66 34 ]
[3 13 14 50 62 69 82 73 66 34 ]
[3 13 14 50 62 69 73 82 66 34 ]
[3 13 14 50 62 66 69 73 82 34 ]
[3 13 14 34 50 62 66 69 73 82 ]
```

---
### Examplo: Elementos repetidos

Faça uma função que determine se um vetor $v$ possui elementos repetidos ou não.

Se $v$ está ordenado... será mais fácil?
---
#### Elementos repetidos
Verificar se o _primeiro_ (`v[0]`) elemento está repetido:

```
1  4  6  8  5  6  9
^  ^
|..|
```
---
#### Elementos repetidos
Verificar se o _primeiro_ (`v[0]`) elemento está repetido:

```
1  4  6  8  5  6  9
^     ^
|.....|
```
---
#### Elementos repetidos
Verificar se o _primeiro_ (`v[0]`) elemento está repetido:

```
1  4  6  8  5  6  9
^        ^
|........|
```
---
#### Elementos repetidos
Verificar se o _primeiro_ (`v[0]`) elemento está repetido:

```
1  4  6  8  5  6  9
^                 ^
|.................|
```

__Conclusão:__
- O primeiro elemento não está repetido
- Note que comparamos `v[0]` contra todos os outros elementos (`v[1],...,v[6]`)

---
#### Elementos repetidos
Verificar se o _segundo_ (`v[1]`) elemento está repetido:

```
1  4  6  8  5  6  9
   ^  ^
   |..|
```
---
#### Elementos repetidos
Verificar se o _segundo_ (`v[1]`) elemento está repetido:

```
1  4  6  8  5  6  9
   ^     ^
   |.....|
```
---
#### Elementos repetidos
Verificar se o _segundo_ (`v[1]`) elemento está repetido:

```
1  4  6  8  5  6  9
   ^              ^
   |..............|
```
__Conclusão:__
- O _segundo_ elemento não está repetido
- Note que comparamos `v[1]` contra todos os outros elementos a direita  (`v[2],...,v[6]`)

---

#### Elementos repetidos
Verificar se o _terceiro_ (`v[2]`) elemento está repetido:

```
1  4  6  8  5  6  9
      ^  ^
      |..|
```
---
#### Elementos repetidos
Verificar se o _terceiro_ (`v[2]`) elemento está repetido:

```
1  4  6  8  5  6  9
      ^     ^
      |.....|
```
---
#### Elementos repetidos
Verificar se o _terceiro_ (`v[2]`) elemento está repetido:

```
1  4  6  8  5  6  9
      ^        ^
      |........|
```

- Encontramos 2 elementos iguais!
- Portanto, existem elementos repetidos
- Não precisamos continuar percorrendo o vetor

---
### Elementos repetidos
```cpp
bool repetido (int v[], int n){
  for (i=0 ; i < n ; i++){
      for(j=i+1 ; j < n ; j++){
          if(v[i] == v[j]){
              return true;
          }
      }
  }
  return false;
}
```
---
### Elementos repetidos
#### Vetor Ordenado
```
   1  4  6  8  5  6  9
```

```
=> 1  4  5  6  6  8  9
```

Agora só precisamos percorrer de esquerda a direita!

---
### Elementos repetidos
#### Vetor Ordenado

```
// V deve estar ordenado
bool repetido(int v[], int n){
  for (i=0 ; i < n - 1 ; i++){
      if (v[i] == v[i+1])
          return true;
  }
  return false;
}
```
- Só precisamos de um laço for!

---
### Teste
<https://multiprova.ufrn.br/>
