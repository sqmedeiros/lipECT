## Comandos de Seleção
### If-Else e Switch

---

### Objetivos

- Utilizar corretamente estruturas de *Seleção*
- Nesta aula veremos as seguintes estruturas
  - `if`
  - `if/else`
  - `switch`

#### Problemas a resolver
  Decisões simples e aninhadas.

---

### Estruturas de Seleção

São utilizadas para _escolher_ um fluxo de execução 

O fluxo é escolhido de acordo com o resultado de uma _expressão booleana_

#### Video O comando de seleção if (17.12)

---

<iframe width="1206" height="678" src="https://www.youtube.com/embed/Os0RC80O0ko?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

### Comando If-Else

Só um comando dentro do `if`

```cpp
if (n>=0)
  cout<<"Número positivo";
```

Vários comandos
```cpp
if (n>=0){ // Chaves {...} são necessárias
    soma += n;
    cont++;
}
```


---

### Comando If-Else
#### Seleção Homogênea
 ```cpp
 if(cond1){
     bloco1;
 }
 if(cond2){
     bloco2;
 }
 if (cond3){
     bloco3;
 }
 ...
 ```
A execução de `bloco2` não depende do valor de `cond1`

Os blocos são *independentes* 
---

### Comando If-Else
#### Seleção Homogênea
Exemplo: imprimir se um número é par/ímpar e se ele é positivo/negativo
```cpp
if(n%2==0)
    cout << "Par" << endl;
else
    cout << "Ímpar" << endl;
// A segunda estrutura é independente da primeira
if (n<0)
    cout << "Número negativo" << endl;
else
    cout << "Número positivo" << endl;
```
---

### Comando If-Else
#### Seleção Aninhada

```cpp
if(c1){
    B1;
}
else if(c2){
    B2;
}
else if(c3){
    B3;
}
```

A execução de B2 está condicionada a:
 - `c1` *deve ser falsa*
 - `c2` *deve ser verdadeira*


---

### Comando If-Else
#### Seleção Aninhada
Exemplo:  Classificar uma avaliação como Excelente (8-10), Bom (7-8), Regular (5-7) e Deficiente (<5)
```cpp
if(nota>=8)
    cout <<"Excelente" << endl;
else if(nota >=7)
    cout <<"Bom" << endl;
else if(nota >=5)
    cout <<"Regular" << endl;
else
    cout <<"Deficiente" << endl;
```

Note que só um dos ``cout``s será executado


---

### Comando If-Else
Lembre que qualquer valor diferente de zero é considerado como __verdadeiro__

O seria impresso pelo programa?
```cpp
int x=5;
if(x)
    cout << "Sim";
else
    cout << "Não";
```

---

### Comando If-Else
#### Curiosidade 

O que será impresso pelo programa ? 
```cpp
int x;
if (x = 0)
  cout << "Sim";
else
  cout<<"Não";
```
Para comparar valores, você deve utilizar __`==`__

---
### Mais um exemplo
Faça um programa que lê uma letra digitada pelo usuário e determina se essa
letra é uma vogal, consoante ou um símbolo. 

Como sabemos que um caractere é uma letra do alfabeto?
<!-- .element: class="fragment" -->

Se `c` é uma letra do alfabeto, como sabemos que ela é uma vogal?
<!-- .element: class="fragment" -->

---
### Mais um exemplo

```cpp
int main () {
    char c;
    cin>>c;
    if( (c>='a' && c<='z')|| (c>='A' && c<='Z')){
        // Nesses intervalos, c deve ser uma das letras do alfabeto
        if(c=='a' || c=='e' || c=='i' || c=='o' || c=='u' ||
           c=='A' || c=='E' || c=='I' || c=='O' || c=='U')
            cout << c << " é uma vogal" << endl;
        else
            cout << c << " é uma consoante" << endl;
    }
    else // c é um símbolo (e não uma letra)
        cout << c << " é um símbolo" << endl;
    return 0;
}
```

---
### Comando de Seleção `switch`

#### Comando de seleção switch (escolha) (17.15)

---

<iframe width="1206" height="679" src="https://www.youtube.com/embed/BKZIi9Ed0U4?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---

### Comando de Seleção `switch`
Exemplo: imprimir os dias da semana
```cpp
cin >> n;
switch (n) {
  case 0:
    cout << "Domingo" << endl;
    break;
  case 1:
   cout << "Segunda" << endl;
   break;
   ...
  default:
     cout << "Dia inválido" << endl;
}
```
Não esquecer o *`break`*

---
### Comando de Seleção `switch`

- É possível substituir uma estrutura  `switch`  por uma estrutura `if-else`.
- Os casos considerados dentro do switch devem ser *constantes* (e.x., 3 para um `int` ou `'a'`  para um `char`)
- Se  precisar de um intervalo (ex. 2.5 - 8.7) utilizar `if-else`

---
### Operador Ternário 

```cpp
bool ehPar;
if (n%2 ==0)
    ehPar = true;
else
    ehPar = false;
```

Esse programa pode ser escrito de forma mais simples:
```cpp
ehPar = n%2 == 0 ? true : false;
```

```cpp
// A expressão 
c ? v1 : v2 
// retorna v1 se c for verdadeiro e v2 caso contrário
```
De fato, como 0 e falso são a mesma coisa
```cpp
ehPar = !(n%2); // Mais simples, né? ;-)
```
---
### Operador Ternário 

Mais exemplos, ver vídeo: O Operador Ternário (Comandos de Seleção)


---
### Teste! 

<https://multiprova.ufrn.br/>
