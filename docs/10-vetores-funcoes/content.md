## Funções, vetores e matrizes
---
## Objetivo da aula

- Mostrar passagem de vetores como _parâmetros de funções_.
-  Resolver exercícios.

---

### Revisão

Em geral, pode-se passar parâmetros para funções de duas maneiras:
-  _Por valor_: o _valor_ do argumento _é copiado_ para o parâmetro e as
   alterações feitas no parâmetro _não tem efeito_ sobre a variável usada na
   chamada da função.
- _Por referência_: o _endereço de uma variável_ é copiado para o parâmetro,
  portanto, as mudanças feitas no parâmetro _afetam a variável usada_ na
  chamada da função

---

### Exemplo de parâmetros por referência

```cpp
#include < iostream>
using namespace std;
// x e y são parâmetros por referência.
void trocar (int &x, int &y); // &: referência
int main (){
  int a=5,b=7;
  cout<< "a=" << a << " b=" << b << endl;
  trocar(a,b);
  cout << "a=" << a << " b=" << b << endl;
  return 0;
}
void trocar (int &x, int &y){
  int temp = x;
  x = y;
  y = temp;
}
```
---
### Vetores como argumento de funções
O nome de um  vetor (_sem os colchetes_) representa o _endereço_ onde o vetor  está armazenado.

Ao passar o _nome de um vetor_ para uma função __não se cria uma cópia do vetor__, a passagem é feita por _referência_.

Deve-se fornecer o _tamanho do vetor_ _como parâmetro_ para que a função trabalhe corretamente.

---
### Exemplo: Imprimir um vetor de inteiros

```cpp[1-5|6-14|15-21]
#include < iostream>
using namespace std;
// n é o tamanho do vetor v
// Note que NÃO precisa do operador &
void imprimir(int v[], int n);
int main (){
   int vetor1[] = {5, 10, 15};
   int vetor2[] = {2, 4, 6, 8, 10};
   // O nome do vetor sem colchetes
   imprimir(vetor1, 3);
   // Segundo parâmetro é o tamanho
   imprimir(vetor2, 5);
   return 0;
}

void imprimir(int v[], int n) {
   for (int i=0; i < n; i++)
      cout << v[i] << " ";
   cout << endl ;
}
```
---

### Calcular a média

```cpp[1-4|5-12|14-17|19-24]
#include < iostream>
#define TAM 200
using namespace std;

float calcula_media(float notas[], int tamanho);

int main (){
   int tam; float media, notas[TAM];
   cout << "Qual o tamanho da turma? "; 
   cin >> tam;

   for(int i = 0; i < tam; i++)
      cin >> notas[i];

   media = calcula_media(notas, tam);
   cout << "A media é: " << media << endl;
   return 0;
}

float calcula_media(float notas[], int tamanho){
   float media = 0;
   for(int i = 0; i < tamanho; i++)
      media += notas[i];
   return  media/tamanho;
}
```
---
### Soma de dois vetores
A soma de dois vetores é  um vetor

Porém, não podemos retornar um vetor (sem utilizar memória dinâmica)

Portanto, utilizaremos um terceiro parâmetro para armazenar o resultado. 

---
### Soma de dois vetores
```cpp
void soma(int A[], int B[], int C[], int n){
   for(int i = 0; i < n; i++)
      C[i] = A[i] + B[i];
}

```
O espaço para guardar o resultado é alocado pela função chamadora (por exemplo
a main). Assim, a função soma recebe três vetores: dois com dados de
_entrada_ (A e B) e um _para armazenar o resultado_ (C)

---
### Soma de dois vetores
```cpp
int main(){
 int A[] = {1,2,3};
 int B[]= {4,5,6};
 int C[3];
 soma(A,B,C,3);
 imprimir(C,3);
 return 0;
}
```
---
### Imprimir uma matriz
O número de colunas __sempre__ deve ser fornecido

```cpp
void imprimir(int M[][TAM], int n, int m){
   for(int i=0; i < n; i++){
    for(int j=0; j < m; j++)
        cout << M[i][j] << " ";

    cout << endl ;
   }
}
```
---
### Ler os valores de uma matriz
O número de colunas __sempre__ deve ser fornecido
```cpp
void ler(int M[][TAM], int n, int m){
   for(int i=0; i < n; i++){

    for(int j=0; j < m; j++)
        cin >>  M[i][j];
   }
}
```
---
### Soma de duas matrizes

```cpp
void soma(int A[][TAM], int B[][TAM], int C[][TAM], 
          int n, int m){
   for(int i=0; i < n; i++){

    for(int j=0; j < m; j++){

      C[i][j] = A[i][j]+B[i][j];
    }
  }
}
```
---
### Soma de duas matrizes
Utilizando as três funções anteriores
```cpp
int main(){
    int M1[TAM][TAM], M2[TAM][TAM], M3[TAM][TAM];
    int n,m;
    cin >> n >> m ;// Dimensões da matriz

    ler(M1, n , m);
    ler(M2, n , m);
    soma(M1,M2,M3, n, m);
    imprimir(M3, n, m);
    return 0;
}
```


--- 
### Converter uma string para inteiro

Considere uma string cujos elementos  são todos dígitos, por exemplo, "1234". 
Como podemos converter essa string no número inteiro 1234?

--- 
### Converter String em Inteiro

- `'0'` é o número 48 na tabela ASCII
- `'1'` é o número 49 na tabela ASCII
- Portanto,`'1' - '0' --> 1`

A ideia:
- Percorrer a string.
- Por cada caractere `c` calcular `c - '0'
- Acumular o somatório

---
### Converter String em Inteiro

```cpp[1-6|8-17|18-28]
#include < iostream>
#define TAM 30

using namespace std;

int converterInt(char s[]);

int main(){
    char str[TAM];
    int i;

    cin >> str;
    i = converterInt(str);

    cout << i << endl;
    return 0;
}
int converterInt(char s[]){
    int soma=0;
    int l = strlen(s);
    int d;

    for (int i=0; i < l ; i++){
        d = s[i] - '0';
        soma = soma*10 + d;
    }
    return soma;
}
```
---

## Matriz de permutação

Uma matriz quadrada é chamada matriz de permutação se seus elementos são apenas
0's e 1's e se em cada linha e coluna da matriz existe apenas um único valor 1. Por exemplo, 

<img src=perm1.png width=300 />

<img src=perm2.png width=300 />

---
## Matriz de permutação

1. Uma função para determinar se uma coluna está OK
2. Uma função para determinar se uma linha está OK
3. Uma função que verifica todas as linhas e colunas 

---
## Matriz de permutação
Verificar uma coluna 

```cpp
bool colOK(int M[][MAX], int col, int n){
    int soma = 0;
    for(int i = 0 ; i< n;i++){
        if (M[i][col] != 0 && M[i][col] != 1)
            return false;

        soma+= M[i][col];
    }
    return soma == 1 ;
}
```
---
## Matriz de permutação
Verificar uma linha

Note que o parâmetro __é um vetor e não uma matriz__

```cpp
bool linhaOK(int v[], int n){
    int soma = 0;
    for(int i = 0 ; i < n ; i++){
        if (v[i] != 0 && v[i] != 1)
            return false;

        soma+= v[i];
    }
    return soma == 1;
}
```
---
## Matriz de permutação

A função que verifica todas as linhas e colunas

```cpp
bool permute(int M[][MAX], int n){
    for(int i = 0 ; i < n ; i++){
        // M[i] é um vetor!
        if (!linhaOK(M[i],n))
            return false;
    }

    for(int i = 0; i < n;i++){
        if (!colOK(M,i, n))
            return false;
    }

    return true;
}
```

---
## Matriz de permutação

O bloco main: 

```cpp
int main()
{
    int n,M[MAX][MAX];
    cin >> n;
    ler(M, n, n);

    if(permute(M, n))
        cout << "É matriz de permutação" << endl;
    else
        cout << "Não é matriz de permutação" << endl;
    return 0;
}
```

---
### Teste!
<https://multiprova.ufrn.br/>

---
### Elementos repetidos

Determinar se uma matriz $M$ de dimensão $n \times m$ possui elementos repetidos.

--- 

### Elementos repetidos

- Vamos implementar uma função que, dado um número $x$, retorne o número de vezes que
$x$ ocorre na matriz. 
- Se um valor ocorrer mais de uma vez, então a matriz possui elementos repetidos. 

---
### Elementos repetidos

Função para contar o número de vezes que $v$ ocorre na matriz:

```
int ocorre(int M[][TAM], int v, int n, int m){
    int cont =0;
   for(int i=0; i < n; i++){
    for(int j=0; j < m; j++){
        if (M[i][j]==v)
            cont ++;
    }
   }
   return cont;
}
```
---
### Elementos repetidos

Utilizando a função anterior, podemos determinar se a matriz possui ou não elementos
repetidos:

```
bool repetidos(int M[][TAM], int n, int m){
   for(int i=0; i < n; i++){
    for(int j=0; j < m; j++){
        if (ocorre(M, M[i][j], n ,m) >1)
            return true;
    }
   }
   return false;
}
```

---
### Elementos repetidos

Exemplo de uso:

```cpp
int main(){
    int M[TAM][TAM] = { {1,2,3},{4,2,6},{7,8,9}};
    if(repetidos(M,3,3))
        cout << "sim" << endl;
    else
        cout << "não" << endl;

}
```
---
### Elementos repetidos

Exemplo de uso:

```cpp
int main(){
    int M[TAM][TAM];
    int lin, col;
    cin >> lin >> col;
    ler(M, lin, col);

    if(repetidos(M,lin,col))
        cout << "sim" << endl;
    else
        cout << "não" << endl;
}
```
---
### Linhas Iguais

Escreva uma função que recebe uma matriz $M$, o seu número de linhas e colunas, e
retorna true se $M$ possui duas linhas iguais e false caso contrário.

---
### Linhas Iguais
- Vamos implementar uma função que, dadas duas linhas l1 e l2, determine se elas são iguais
- Depois, utilizaremos essa função para resolver o problema

---
### Linhas Iguais
Aqui temos uma função que compara se __2 vetores__ são iguais

```
bool linhasIguais(int v1[], int v2[], int n){
    for(int i=0 ; i < n ; i++){
        if(v1[i]!=v2[i])
            return false;
    }
    return true;
}
```
---
### Linhas Iguais
- Como podemos utilizar essa função com as _linhas de uma matriz?_
- Lembre que $M[i]$ representa um vetor (a linha $i$ da matriz)

---
### Linhas Iguais
```
bool matrizl(int M[][Max],int nl,int nc){
    for(int i=0 ; i < nl ;i++){
        for(int j=i+1 ; j < nl ; j++){
            if(linhasIguais(M[i], M[j], nc))
                return true;
        }
    }
    return false;
}
```

Note o uso de `M[i]` e `M[j]`

---
### Linhas Iguais
Uma alternativa:

```
bool linhasIguais(int M[][TAM], int l1, int l2,  int n){
    for(int i=0; i < n;i++){
        if(M[l1][i]!=M[l2][i])
            return false;
    }
    return true;
}
```
---
### Linhas Iguais
Uma alternativa:
```
bool matrizl(int M[][Max],int nl,int nc){
    for(int i=0; i < nl;i++){
        for(int j=i+1 ; j < nl;j++){
            if(linhasIguais(M, i, j , nc))
                return true;
        }
    }
    return false;
}
```
---
### Xadrez e torres
- No xadrez a torre se move em linha reta horizontalmente e verticalmente.
-  Considere uma matriz quadrada M de dimensão n x n (n <= 100) que representa um tabuleiro de xadrez no qual podemos colocar torres da _mesma cor_.
- Um número 1 na matriz representa uma posição com uma torre e um 0 representa um espaço livre. 
---
### Xadrez e torres
- Faça uma função que, dado um tabuleiro de dimensão n x n, determine (retornando true/false) se alguma das torres pode atacar outra torre. Por exemplo, no tabuleiro

Retorna: true
```cpp
0 1 0 1 <-- ataque
0 0 0 0
0 0 1 0
0 0 0 0
```
Retorna: false:
```cpp
0 1 0
1 0 0
0 0 1
```
---
### Xadrez e torres
- Vamos contar o número de 1's por cada linha e por cada coluna
- Se esse contador for maior que um, as torres podem atacar-se

---
### Xadrez e torres
Função para verificar uma linha:
```cpp
bool linhaOK(int v[], int n){
    int soma=0;
    for(int i=0; i < n;i++){
        if (v[i]!=0 && v[i]!=1)
            return false;
        soma+= v[i];
    }
    return soma <= 1;
}
```

---
### Xadrez e torres
Função para verificar uma coluna:
```cpp
bool colOK(int M[][MAX], int col, int n){
    int soma=0;
    for(int i=0; i < n;i++){
        if (M[i][col]!=0 && M[i][col]!=1)
            return false;
        soma+= M[i][col];
    }
    return soma <= 1 ;
}
```

---
### Xadrez e torres
Agora só precisamos utilizar as funções anteriores:

```cpp
// Retorna true se alguma torre pode atacarse
// Note que as funções OK retornam true se nenhuma torre pode atacar-se
bool torres(int M[][MAX], int n){
    // Linhas
    for(int i=0; i < n;i++){
        if (!linhaOK(M[i],n))
            return true;
    }
    // Colunas
    for(int i=0;i < n;i++){
        if (!colOK(M,i, n))
            return true;
    }
    return false;
}
```
---
### Multiplicação de matrizes

Faça uma função para multiplicar duas matrizes. 

Lembre: $M \times N$ faz sentido sim:
 - $M$ é de dimensão $a \times b$
 - $N$ é de dimensão $b \times c$
 - O resultado $M\times N$ é de dimensão $a \times c$

---
### Multiplicação de matrizes
O resultado $R = M \times N$:
- A posição $R[i][j]$ corresponde ao produto escalar da linha $i$ de $M$ e a coluna $j$ de $N$.

```
               - x - -
- - - - -      - x - -
x x x x x   *  - x - -
- - - - -      - x - -
               - x - -
```

---
### Multiplicação de matrizes

- Entradas: As matrizes M e N
- As dimensões: a,b,c
- Saídas: A matriz $M \times N$

---
### Multiplicação de matrizes
```cpp
void mult(int M1[][TAM], int M2[][TAM], int nlm1, ncm1, ncm2, int M3[][TAM]){
    for(int i=0 ; i < nlm1 ; i++){
        for(int j=0 ; j < ncm2 ; j++){
            // Produto escalar: 
            // linha i de M1 coluna j de M2
            int soma = 0;
            for (int k = 0 ; k < ncm1 ; k++){
                soma += M1[i][k] * M2[k][j];
            }
            M3[i][j] = soma;
        }
    }

}
```
---
### Multiplicação de matrizes
Note que o último parâmetro da função será utilizado como saída: 

```cpp
int main(){
    int A[TAM][TAM], B[TAM][TAM], C[TAM][TAM];
    int la,ca,cb;
    ler(A, la, ca);
    ler(B, ca, cb);
    mult(A,B,;a,ca,cb,C);
    imprimir(C, a, c);
    return 0;
}
```

---
### Teste!
<https://multiprova.ufrn.br/>
