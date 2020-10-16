## Funções (Introdução)

---

### Objetivos

Apresentar as construções oferecidas em C++ para a implementação de programas com funções.

#### Do ponto de vista de problemas a resolver
 - Identificar entradas e saídas de um procedimento.
 - Quebrar um problema em problemas mais simples.
 - Reaproveitar soluções já implementadas.

---
### Funções

Variáveis guardam valores de diferentes tipos:

```cpp
char, int, float, bool
```

E se pudéssemos atribuir não um valor, mas sim, um _trecho de código_ a um _nome_, similar a uma variável?

>Isto é exatamente o que acontece com funções em linguagens de programação

---
### Funções

#### Introdução

Vídeo: O que é uma função? (6.44)

---

<iframe width="1134" height="638" src="https://www.youtube.com/embed/9S32uN23u5Q?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

### Definições Básicas
Uma função é um _conjunto de comandos_ agrupados em um bloco, destinado a realizar uma __tarefa particular__.

Considere a função _soma_:
 - A função recebe um _nome_ e através deste pode ser _ativada_. 
 - A função pode _retornar_ um valor (ex., a soma de 3 e 2 é 5). 
 - A função pode receber _parâmetros de entrada_. 

> Uma função  _associa um identificador_ a um determinado trecho de código.

---
### Criando uma Função

Vídeo: Como criar minha própria função (16:29)

---
<iframe width="1134" height="638" src="https://www.youtube.com/embed/XDPudzItdd8?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

### Implementando Funções

Implementar funções corretamente envolve identificar:
 
- As _entradas_ necessárias do subprograma (_parâmetros_ ou argumentos da função)
- O que o subprograma deve _computar_ (_código da função_)
- As possíveis _saídas_ do subprograma

---

### Um exemplo (Fatorial)

Faça um programa que, dado um número `n`, calcule `n!`

Faça um programa que, dado um número `n`, calcule $\sum\limits_{i=1}^{n}i!$

Faça um programa que, dado um número `n`, calcule `n!!`

> Será que devemos implementar várias vezes o algoritmo para calcular `n!`?

---

### Um exemplo (Fatorial)

1. Protótipo da função: entradas? saídas?

```cpp
int fatorial(int n);
```

- entrada: um número inteiro
- saída: um número inteiro
- nome da função: `fatorial`
---

### Um exemplo (Fatorial)

2. Definição da função

```cpp
int fatorial(int n){
    int prod=1; // Variável local

    for(int i=2;i<=n;i++)
        prod *= i;

    return prod; // Retornar o resultado
}
```

- Note que o valor calculado é __retornado__

---

### Um exemplo (Fatorial)

3. Utilizar a função (só para calcular `n!`)

```cpp
int main(){
    int n, res;
    cin>>n;

    res = fatorial(n);
    cout<<"Resultado: " << res << endl;

    return 0;
}
```

- Exemplo de uma __chamada__ à função `fatorial`
---
### Um exemplo (Fatorial)

3. Utilizar a função (só para calcular `n!`)

```cpp
int main(){

    cout << fatorial(5) << endl ;
    return 0;
}
```

- Aqui chamamos a função com a constante `5` 

---
### Um exemplo (Fatorial)

3. Utilizar a função (só para calcular `n!`)
``` cpp
int main(){

    for(int i=1; i <= 10; i++){
        cout << i << "! = " << fatorial(i) << endl;
    }

    return 0;
}
```

- Chamar várias vezes a mesma função

---

### Um exemplo (Fatorial)

4. Utilizar a função (para calular $\sum\limits_{i=1}^{n}i!$)

```cpp
int main(){
    int n, soma=0;
    cin>>n;

    for(int i=1;i<=n;i++)
        soma += fatorial(i);

    cout<<"Soma: "<< soma << endl;
}
```
---

### Um exemplo (Fatorial)

4. Utilizar a função (para calular `n!!`)
```cpp
int main(){
    int n, res;
    cin>>n;
    res = fatorial(fatorial(n));

    cout<<"Resultado: "<< res << endl;
}
```
---

### Por que devo utilizar funções
 - Para _dividir um problema_ maior em vários menores, simplificando e
   _organizando o código_;
 - Reduzir o tamanho do programa;
 - Para permitir _reaproveitamento_ de código;
 - Para que os blocos do programa não fiquem grandes demais e mais difíceis de
   entender;
 - Para separar o programa em partes (blocos) que possam ser logicamente
   compreendidos de forma isolada;

--- 
### Exemplo: Determinar se um número é Primo ou não 

- Entradas?
- Saídas? 

---
### Exemplo: Determinar se um número é Primo ou não

1. Protótipo / Cabeçalho da função

```cpp
bool ehPrimo(int n);
```
---
### Exemplo: Determinar se um número é Primo ou não

2. Definição da função 

```cpp
bool ehPrimo(int n){
    // Assumindo n positivo
    if (n<=1)
        return false;

    for(int i=2;i < n;i++){
        if(n%i ==0) return false;
    }
    return true;
}
```

---

### Exemplo: Determinar se um número é Primo ou não
```cpp
bool ehPrimo(int n){
    ...
}
``` 

- A função __determina__ se `n` é primo *retornando* verdadeiro ou falso
- A função *não imprime* o resultado

---

### Exemplo: Determinar se um número é Primo ou não

3. Utilizar a função

```cpp
int main(){
    int n;
    cin >> n;
    if (ehPrimo(n)) // ou ehPrimo(n) == true
        cout << "O número é primo" << endl;
    else
        cout << "O número não é primo" << endl;

    return 0;
}
```

---

### Exemplo: Sequência Fibonacci

A sequência: 1, 1, 2, 3, 5, 8 ....

Faça uma função que, dado um número `n`, retorne o termo `n` da sequência.

---

### Exemplo: Sequência Fibonacci

1. Protótipo / Cabeçalho 

```cpp
int fibonacci(int n);
```

---

### Exemplo: Sequência Fibonacci

2. Definição da Função

```cpp
int fibonacci(int n){
    int v1=1, v2=1;// Valores iniciais
    int novo;

    for(int i=3 ; i<=n;i++){ // Gerar n-2 termos
        novo = v1 + v2;
        v1 = v2;
        v2 = novo;
    }
    return v2;
}
```

---

### Exemplo: Sequência Fibonacci

3. Chamar / utilizar a função

```cpp
int main(){
    int x;
    cout << fibonacci(10) << endl ;
    cout << fibonacci(20) << endl ;

    cin >> x ;
    cout << fibonacci(x) << endl ;

    return 0;
}
```

---
### Resumo
```cpp
#include< iostream>
using namespace std;
// Protótipos das funções
bool ehPrimo(int n); // Cabezalho: entradas e saídas 
int fatorial(int n);
...
// Função main
int main(){
    ...
    // Ler valores
    // Chamar as funções
    // Imprimir resultados
    ...
}

// Definir as funções
bool ehPrimo(int n){
    ...
}
```
---

### Teste!
[LOP](https://lop.natalnet.br/)

---
## Aula 02 Funções e Procedimentos
---

### Chamando várias funções. 

Vídeo Calculando a probabilidade de acertar na Megasena (10.18)
---
<iframe width="1206" height="678" src="https://www.youtube.com/embed/I67p4RNXj58?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---
### Procedimentos

Vídeo O que é um procedimento? (5.23)

---
<iframe width="1206" height="678" src="https://www.youtube.com/embed/zoILKCpydJ4?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---
### O comando `return`

A instrução  `return expressão;`  tem os seguintes efeitos:

- _avaliação_ da expressão (`return n * 2;`)
- _conversão_ automática do resultado da expressão para _o tipo da função_
- _retorno_ do resultado
- _término da execução_ da função e retorno do controle para a instrução seguinte do código de chamada

---

### O comando `return`

>Se a função é do tipo _void_ não precisa utilizar o comando `return`:

```cpp
// Função que imprime um inteiro
void imprimir(int x){
 cout << x;
}
```
Também: 

```cpp
// Função que imprime um inteiro
void imprimir(int x){
 cout << x;
 return;
}
```
---

### Algumas observações
- O comando _return_ pode retornar _somente um único valor_.
- Se uma função não tem valor de retorno, deve-se indicar o tipo de retorno como `void`
- Não é possível definir uma função dentro de outra função.
- Quando chamamos uma função o fluxo de execução é desviado para a função.
- Quando uma função termina o fluxo de execução retorna para onde a função foi chamada.

---
### Exemplo: Procedimento

Procedimento que imprime os primeiros `n` elementos da sequência Fibonacci. 

1. Protótipo da função

```cpp
void termosFib(int n);
```

- Entrada: o número de termos
- Saída: Nenhuma! (`void`)


---
### Exemplo: Procedimento

2. Definir o procedimento

```cpp
void termosFib(int n)P
    int v1=1, v2=1;// Valores iniciais
    int novo;
    cout<< v1 << endl << v2 << endl ; // 2 primeiros termos
    for(int i=3 ; i<=n;i++){ // Gerar n-2 termos
        novo = v1 + v2;
        v1 = v2;
        v2 = novo;
        cout << novo << endl;
    }
}
```

---
### Exemplo: Procedimento

3. Utilizar a função

```cpp
int main(){
    int num;
    cin >> num;
    termosFib(num); // Chamar a função
    return 0;
}
```

---
### Exemplo: Procedimento

3. Utilizar a função

```cpp
int main(){
    termosFib(20); // Chamar a função
    return 0;
}
```

- Chamar a função com a constante `20`
- Note: __sem__ `cout`

---

### Teste!
[LOP](https://lop.natalnet.br/)

---

## Aula 03
### Parâmetros por Valor e Referência

---

### Objetivos

Nesta aula responderemos as seguintes perguntas:

- Entender o __escopo__ das variáveis.
- Como devemos definir uma função para _retornar mais de um valor_ ?
- Podemos _modificar_ os valores dos parâmetros ?

---

### Escopo de variáveis

> O escopo de uma variável é o bloco de código onde esta variável é válida.

As variáveis podem ser declaradas em três lugares:

- _Variáveis locais_: declaradas dentro de uma função
- _Parâmetros formais_: parâmetros de funções
-_Variáveis globais_: declarada fora de todas as funções.

```cpp
void f(int x, double y){// x e y são parâmetros formais
 int a;
 float b;// a e b são variáveis locais

 ...
}
```

---
### Escopo de variáveis

```cpp
void f1();

int main (){
  int x=3;
  f1();
  cout << x; // 3 ou 5 ??
  return 0;
}

void f1(){
 int x=5;
}
```

---
### Escopo de variáveis

```cpp
void f1();
void f2(int x);

int main (){
  cout << x; // ERRO! x não existe na main.
  return 0;
}

void f1(){
 int x=5;
 cout << x; // variável local
}
void f2(int x){
 cout << x; // parâmetro
}
```

---
### Escopo de variáveis

```cpp

void f1();

int main (){
  int x = 3;
  f1();
  return 0;
}

void f1(){
  cout << x; // ERRO! x não existe na função f1
}
```

---
### Parâmetros de uma função

São variáveis __locais__ que são *inicializadas* pelos valores passados na
chamada da função:
- São visíveis apenas _dentro da função_: são _criadas_ na entrada e
  _destruídas_ na saída da função
- No momento da chamada de uma função, o número e o tipo dos parâmetros devem
  _corresponder_ à declaração da função

--- 
### Passagem de parâmetros

Em geral, pode-se passar parâmetros para funções de duas maneiras:

- _Por valor_: o _valor_ do argumento _é copiado_ para o parâmetro e as
  alterações feitas no parâmetro __não tem efeito__ sobre a variável usada na
  chamada da função.
- _Por referência_: o _endereço de uma variável_ é copiado para o
  parâmetro, portanto,  as mudanças feitas no parâmetro _afetam a variável
  usada_ na chamada da função

---
### Parâmetros por Valor

```cpp
void inc(int x);

int main(void){
 int i = 5;
 cout << "i: " << i << endl; // 5.
 inc(i);
 cout << "i: " << i << endl; // 5 ou 6 ??
 return 0;
}

void inc(int x){
  x++;
}
```

---
### Parâmetros por Valor

```cpp

int quadrado(int x);
int main(){
 int n=10;
 cout << quadrado(n) ; // resultado ?
 cout << n; // resultado ?
 return 0;
}

int quadrado(int x){
 x = x * x;
 return x;
}
```

---
### Qual é o problema?

```cpp
void trocar (int x, int y);

int main (){
  int a=5,b=7;
  cout << "a=" << a << " b=" << b << endl;
  trocar(a,b);
  cout << "a=" << a << " b=" << b << endl;
  return 0;
}

void trocar (int x, int y){
  int temp = x;
  x = y;
  y = temp;
}
```
Solução: Parâmetros por __referência__!

---
### Parâmetros por Referência

Video Passagem de parâmetros por valor e por referência (15.15)

---
<iframe width="1085" height="610" src="https://www.youtube.com/embed/pp6iWfYM2mg?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

### Parâmetros por Referência

```cpp
void trocar (int &x, int &y);

int main (){
  int a=5,b=7;
  cout << "a=" << a << " b=" << b << endl;
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
As valores de `a` e `b` são modificados!


---

### Parâmetros por Referência

O _endereço de uma variável_ é copiado: __mudanças no parâmetro afetam a
variável usada__

- Se a função _NÃO deve modificar_ o valor do parâmetro, melhor utilizar parâmetros _por valor_.
- Se precisar de _retornar mais de um valor_, deve utilizar parâmetros por __referência__.

---

### Parâmetros por Referência
#### Retornando vários valores

Video Exercício Resolvido (parâmetros de entrada e saída) (12.16)

---
<iframe width="1085" height="610" src="https://www.youtube.com/embed/ymellvbj8Cc?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

### Exemplo

Faça uma função que, dado um número de segundos _S_,  calule a quantidade
correspondente em horas, minutos e segundos. 

#### Protótipo da função
- Entradas?
- Saídas?

---

### Exemplo

#### Protótipo da função

```cppp
void time(int S, int &seg, int&min, int &hora);
```
- `S`: parâmetro de __entrada__ (valor)
- 3 parâmetros de __saída__ (referência)
---

### Exemplo

#### Definição da Função

```cpp
void time(int S, int &seg, int&min, int &hora){
    seg = S % 60;
    hora = S/3600;
    min = (S - hora*3600)/60;
}

```
- Parâmetros por referência
- Atribuir dentro da função significa __modificar os valores dos parâmetros__
  utilizados na chamada da função. 

---

### Exemplo

#### Utilizando a função

```cpp
int main(){
    int s,m,h;
    time(10000,s,m,h);
    cout << h << ":" << m << ":" << s << endl;
    return 0;
}
```
- O primeiro parâmetro é a entrada
- O resultado será armazenado nas variáveis `s`, `m` e `h` da `main`.

---
### Exemplo

Agora vamos implementar uma função para imprimir em formato hh:mm:ss

#### Protótipo
```cpp
void printTime(int S);
```

---
### Exemplo

#### Definição
```cpp
void printTime(int S){
    int s,m,h;
    time(S,s,m,h);
    cout << (h <= 9 ? "0" : "") << h << ":" <<
            (m <= 9 ? "0" : "") << m << ":" <<
            (s <= 9 ? "0" : "") << s << endl;
}
```
- O resultado será armazenado nas __variáveis locais__ da função `printTime`
--- 
### Exemplo
Utilizar a função

```cpp
int main(){
 // 02:46:40
 printTime(10000); 
 // 00:00:00
 printTime(0);  
 // 00:20:01
 printTime(1201);  
 return 0;
}

```
---

### Teste!
<https://multiprova.ufrn.br/>

---

## Aula 04
### Revisão

---

### Problema: Dígitos
Dado um número inteiro positivo `n`, implementar uma função que retorne as
seguintes informações: 

 - O número de dígitos pares de `n`
 - O número total de dígitos

---

### Problema: Dígitos

Entradas e saídas:
 - __Entrada__: O número `n` (tipo `int`)
 - __Saídas__: 2 números inteiros (dígitos pares e total de dígitos)

#### 3 possíveis protótipos (Opção No 1)
```cpp
void infoDigito1(int n, int &dpares, int &tdigitos);
```

- A função não retorna nada (`void`)
- Consideramos 3 parâmetros:
 - A entrada `n` (parâmetro por _valor_)
 - e as duas saídas (parâmetros por _referência_)

---
### Problema: Dígitos

#### 3 possíveis protótipos (Opção No 2)
```cpp
int infoDigito2(int n, int &tdigitos);
```

- A função retorna o número de dígitos pares (`int`)
- Consideramos 2 parâmetros:
 - A entrada `n` (parâmetro por _valor_)
 - o total de dígitos (parâmetro por _referência_)

---

### Problema: Dígitos
#### 3 possíveis protótipos (Opção No 3)
```cpp
int infoDigito3(int n, int &dpares);
```

- A função retorna o número total de dígitos (`int`)
- Consideramos 2 parâmetros:
 - A entrada `n` (parâmetro por _valor_)
 - o total de dígitos pares (parâmetro por _referência_)

---

### Problema: Dígitos
#### Definição da função (Opção No 1)

```cpp
void infoDigito1(int n, int &dpares, int &tdigitos){
    int d; // Variável local
    dpares=0;
    tdigitos=0;
    while(n>0){
        d = n % 10; // Próximo dígito
        tdigitos ++; // Dígitos totais
        if (d %2 ==0) dpares++; // Dígitos pares

        n /= 10 ; // próximo valor de n
    }
}
```
- A função __não__ retorna um valor
- Zeramos os 2 parâmetros por referência 
---

### Problema: Dígitos
#### Definição da função (Opção No 2)

```cpp
int infoDigito2(int n,  int & tdigitos){
    int d; // Variável local
    int dpares=0; // Variável local!
    tdigitos=0;
    while(n>0){
        d = n % 10; // Próximo dígito
        tdigitos ++; // Dígitos totais
        if (d %2 ==0) dpares++; // Dígitos pares

        n /= 10 ; // próximo valor de n
    }
    return dpares;
}
```
- A função retorna o valor da __variável local__ `dpares`

--- 
### Problema: Dígitos
#### Definição da função (Opção No 3)

```cpp
int infoDigito3(int n, int & dpares){
 int d; // Variável local
 dpares=0; // Variável local!
 int tdigitos=0;
    
 ...

 return tdigitos;
}
```
- A função retorna o valor da __variável local__ `tdigitos`

--- 
### Problema: Dígitos

#### Chamando a função (Opção No 1)

```
int main (){
 int n, dp, td;
 n = 1023456;
 infoDigito1(n, dp, td); // Sem retorno
 cout << n << ": " << dp << " , " << td << endl;
 return 0;
}
```

--- 
### Problema: Dígitos

#### Chamando a função (Opção No 2)

```
int main (){
 int n, dp, td;
 n = 1023456;
 dp = infoDigito2(n, td); // Retorna dígitos pares
 cout << n << ": " << dp << " , " << td << endl;
 return 0;
}
```


--- 
### Problema: Dígitos

#### Chamando a função (Opção No 3)

```
int main (){
 int n, dp, td;
 n = 1023456;
 td = infoDigito3(n, dp); // Retorna total de dígitos
 cout << n << ": " << dp << " , " << td << endl;
 return 0;
}
```

---

### Teste!
<https://multiprova.ufrn.br>

---

## Aula Revisão

---

### Exercício Inverte-X (Revisão)

Escreva uma função que recebe como parâmetro um número inteiro x. A função deve
utilizar um parâmetro por referência para informar o valor de x invertido (por
exemplo, 123 -> 321). A função também deve retornar:

 * -1 se o número x é menor que o número x invertido ;
 * 0 se x e o número invertido são iguais;
 * 1 caso contrario.

---
#### Alguns erros comuns 
O que está errado neste protótipo de função?

```cpp
void invertidin(int x);
```

---
#### Alguns erros comuns 
O que está errado neste protótipo de função?

```cpp
void invertidin(int x);
```
- Esta função __deve__ retornar um `int`
- O número invertido __deve__ ser armazenado em um parâmetro (_referência_). 

---
#### Alguns erros comuns 
O que está errado neste código?

```cpp
int main (){
    int num, resto,numInv;

    cout << "Informe um numero:" << endl;
    cin >> num;

    while(num>0){
        resto=num%10;
        ...
```

---
#### Alguns erros comuns 
O que está errado neste código?

```cpp
int main (){
    int num, resto,numInv;

    cout << "Informe um numero:" << endl;
    cin >> num;

    while(num>0){
        resto=num%10;
        ...
```

- A lógica para calcular o número invertido __não deve estar na `main`__
---
#### Alguns erros comuns 
O que está errado neste código?

```cpp
int invers (int x , int &y);
...

int invers(int x, int &y){

     int n_invert; // Armazenar o número invertido
     ...
     return n_invert;
}
```
---

#### Alguns erros comuns 
O que está errado neste código?

```cpp
int invers (int x , int &y);
...

int invers(int x, int &y){

     int n_invert; // Armazenar o número invertido
     ...
     return n_invert;
}
```
- O número invertido __não deve ser retornado__. 
- O parâmetro `y` deve ser utilizado para __armazenar o resultado__.
---

#### Solução

Entradas e saídas: 

```cpp
int inverteX(int x, int &xi);
```

- `x`: parâmetro (valor) de __entrada__
- `xi`: parâmetro (*referência*) de __saída__
- `int`: tipo de retorno (-1, 0 ou 1)

---

#### Solução

Como inverter um número?

```cpp
// xi = 0
// 123 % 10 --> 3 (último dígito)
// xi = xi * 10 + 3 = 3
// 123 / 10 --> 12 (próximo valor)
// 12 % 10 --> 2
// xi = xi * 10 + 2 = 30 + 2 = 32
// 12 / 10 --> 1
// 1 % 10 --> 1
// xi = xi * 10 + 1 = 320 + 1 = 321
// 1 / 10 --> 0  (termina)
```
---

#### Solução

Como inverter um número?

```cpp
int inverteX(int x, int &xi) {
    int xa = x, res;
    xi = 0; // Inicializar xi
    while(x > 0){ // calcular x invertido em xi
        res = x % 10;
        xi = xi*10 + res;
        x /= 10;
    }
    if(xa < xi) // retornar segundo o valor de xi
        return -1;
    else if(xa == xi)
        return 0;
    else
        return 1;
}

```
---

#### Solução

Utilizar a função na main

```cpp
int main()
{
    int num, inv, comp;
    cin >> num;
    comp = inverteX(num,inv); // Chamar a função
    cout << "X = " << x << endl << 
            "X invertido = " << inv << endl;
    if(comp == -1)
        cout << "X é menor que X invertido";
    else if(comp == 0)
        cout << "X é igual que X invertido";
    else if(comp == 1)
        cout << "X é maior que X invertido";
    return 0;
}
```
---

### Sequência S-primo (Revisão)

Dizemos que uma sequência de números naturais é "sprimo" se o somatório dos
números primos da sequência é também um número primo.  
Implemente uma função `ehSPrimo` que recebe dois números inteiros, x e y, e
retorna verdadeiro se a sequência de números no intervalo [x, y] é sprimo. 
```
Entrada: 1 10
Saída : sim (Note que 2+3+5+7 = 17, que é primo).
```
---
### Sequência S-primo
#### Erros comuns 

O que está errado neste código?
```cpp
int sprimo(int x, int y){
    int soma = 0;
    for(x; x <= y; x++){
        if(eprimo(x) == true){
            soma = soma + x;
        }
    }
}
```

---
### Sequência S-primo
#### Erros comuns 

O que está errado neste código?
```cpp
int sprimo(int x, int y){
    int soma = 0;
    for(int i= x; i <= y; i++){
        if(eprimo(i)){
            soma = soma + x;
        }
    }
}
```
- Falta um `return` para retornar o resultado. 
- Falta testar se `soma` é primo ou não
---
### Sequência S-primo
#### Erros comuns 

O que está errado neste código?
```cpp
bool ehsprimo(int x, int y)
{
    int result;
    for(int i=x; i<=y; i++)
    {
        if(primo(i)== true)
            result +=i;
    }
    return result;
}
```

---
### Sequência S-primo
#### Erros comuns 

O que está errado neste código?
```cpp
bool ehsprimo(int x, int y)
{
    int result;
    for(int i=x; i<=y; i++)
    {
        if(primo(i)== true)
            result +=i;
    }
    return result;
}
```
- `result` não foi __inicializado__.
- A função __não deve__ retornar o somatório. 
- A função é do tipo `bool` e o resultado `int`
---
### Sequência S-primo
#### Erros comuns 

O que está errado neste código?

```cpp
void ehSPrimo(int x, int y){
    ...
    cout << ..... 
}
    
```

---
### Sequência S-primo
#### Erros comuns 

O que está errado neste código?

```cpp
void ehSPrimo(int x, int y){
    ...
    cout << ..... 
}
    
```
- A função deve retornar `true/false` (tipo `bool`)
- A função __não deve__ imprimir o resultado. 
---

### Sequência S-primo
#### Erros comuns 

O que está errado neste código?
```cpp
bool ehPrimo(int n){
    if (n<=1)
        return false;

    for(int i=2;i < n;i++){
        if(n%i ==0) return false;
        else return true ;
    }
}
```

---

### Sequência S-primo
#### Erros comuns 

O que está errado neste código?
```cpp
bool ehPrimo(int n){
    if (n<=1)
        return false;

    for(int i=2;i < n;i++){
        if(n%i ==0) return false;
        else return true ;
    }
}
```

- `return true` __só depois__ de testar todos os valores!
---

### Sequência S-primo
#### Solução

Entradas / Saídas:

```cpp
bool ehPrimo(int n);
bool sprimo (int, int);
```

- `ehPrimo`: dado um `int`, __determina__ (retornando um `bool`) se esse número é primo. 
- `sprimo`: dados dois inteiros `x` e `y`, determina se a sequência `x, x+1, x+2,...,y` é sprimo. 

---

### Sequência S-primo
#### Solução

```cpp
// n um inteiro positivo
bool ehPrimo(int n)
{
  if (n<=1)
    return false;

  for(int i = 2; i < n; i++)
  {
    if(n % i == 0 )
      return false;
  }
  return true;
}
```
---

### Sequência S-primo
#### Solução
```cpp
bool sprimo (int a, int b) {
	int soma = 0;
	for (int i = a; i <= b; i++) {
		if (ehPrimo(i))
			soma += i;
	}

	return ehPrimo(soma);
    // if(ehPrimo(soma)==true) return true else return false;
}
```
---

### Sequência S-primo
#### Solução

```cpp
int main()
{
  int x, y;

	cin >> x >> y;

  if(sprimo(x,y)) // ou if(sprimo(x,y)==true)
      cout << "sim" << endl;
  else
      cout << "não" << endl;

  return 0;
}
```

---

### Teste!
<https://multiprova.ufrn.br/>
