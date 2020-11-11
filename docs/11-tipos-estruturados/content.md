## Tipos Estruturados
---
### Objetivo da aula

Responder à seguinte pergunta:

Eu sei como:
- armazenar _uma_ informação de um tipo (__variável__);
- armazenar _várias_ informações do mesmo tipo _sob um mesmo nome_ (__vetores/matrizes__)

>E se eu quiser armazenar informações de _tipos diferentes_ _sob um mesmo nome_?

---
### Motivação
Muitas vezes precisamos agrupar informações de _tipos diferentes_ sob um __mesmo nome__.

 - _Aluno_: CPF, RG, nome, sobrenome, endereço, etc. 
 - _Disciplina_: Código, nome, créditos, ementa, etc. 
 - _Livro_: ISBN, título, ano, número de páginas, etc. 

---
### Motivação

se eu quiser armazenar os dados dos estudantes da UFRN....

```cpp
char cpf[NUM_EST][TAM_MAX];
char nome[NUM_EST][TAM_MAX];
char email[NUM_EST][TAM_MAX];
int semestre[NUM_EXT];
```

será uma boa solução ?

---
### Tipos Estruturados ou Estruturas de Dados Heterogêneas

Uma estrutura (_struct_) ou registro em C++ é uma coleção de um ou mais valores
(possivelmente de _tipos diferentes_), agrupados sob um _único nome_.

As estruturas são um recurso importante para _organizar_ os dados de um
programa graças à possibilidade de tratar _um grupo de valores como uma única
variável_.

---
### Tipos Estruturados 

Uma estrutura é um _tipo_ de dado cujo formato é _definido_ pelo programador.

Vídeo Tipos estruturados: definição, declaração de variáveis e acesso aos campos (11.02)

---
<iframe width="1122" height="631" src="https://www.youtube.com/embed/kh3Z2ywZJmI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---

### Definição de tipos estruturados

Elementos individuais de uma estrutura são chamados _membros_;

Os membros podem ter _tipos diferentes_ (primitivo, matriz ou struct);

O nome de uma estrutura agrega vários membros, enquanto os membros, individualmente, devem possuir _identificadores únicos_

---
### Definição

```cpp
// Cada identificador define um membro.
struct Nome{
 tipo1 identificador1; 
 ...
 tipon identificadorn; 
 } ;
```

---
### Definição
Armazenar uma data
```cpp
struct Data {
  int dia;
  int mes;
  int ano;
} ;
```
---
### Definição

Os membros podem ser vetores ou outros tipos struct:
```cpp
struct contaBancaria{
 char Nome[15];
 char ContaNo[10];
 double saldo;
 Data abertura;
};
```

`Data` é um tipo _definido pelo usuário_ e podemos utilizar ele
para definir outros tipos estruturados. 

---
### Definição

```
struct Estudante{
 char Nome[15];
 int Id;
 char Curso[20];
 char sexo;
};
```
---
### Declaração de variáveis do tipo `struct`
```
Estrutura Identificador;
```

Exemplo:
```
Estudante E1, E2 ;
```

<img src=ED1.png width=600/>

---
### Acesso aos membros

Os membros de um tipo estruturado são acessados com a utilização do _operador
ponto_(.):

```
variavel.membro;
```

Exemplo:

```cpp
Estudante E;
cin >> E.nome ;
cin >> E.Id;
cin >> E.Curso;
cin >> E.sexo;

if (E.sexo == 'M')
 cout << "Sr. " << E.nome;
else
 cout << "Sra. " << E.nome;
```

---
### Estruturas aninhadas
```
struct Ponto{
   double x, y;
};
struct Linha{
   Ponto p1, p2;
};
struct Triangulo{
   Ponto p1, p2, p3;
};
```

---
### Estruturas aninhadas
<img src=figs.png />
---
### Estruturas aninhadas

Como representamos essas figuras?
```cpp
Ponto vp = {4,11}; // Inicializando 
Linha vl = { {2,7}, {10,9}} ;
Triangulo vt; // Declarar e depois atribuir
vt.p1.x = 2; vt.p1.y = 0;
vt.p2.x = 6; vt.p2.y = 5;
vt.p3.x = 8; vt.p3.y = 3;
```

---
### Vetor de estruturas
Um vetor de estruturas armazena em cada posição um tipo estruturado (com vários membros):
<img src=vetor.png />

---
### Vetor de estruturas

```
Estudante Turma[100];
strcpy(Turma[98].Nome, "Chan Tai Man");
Turma[98].Id = 12345;
strcpy(Turma[98].Curso, "COMP");
Turma[98].Sexo = 'M';
// Podemos utilizar o operador de atribuição!
Turma[0] = Turma[98];

```
<img src=est.png width=500/>

---
### Vetor como membro de estrutura
```
struct Quadrilatero{
  Ponto vertices[4];
};

int main(){
  Quadrilatero q;
	...
}
```
---
### Vetor como membro de estrutura
<img src=quad.png width=400/>

```cpp
Quadrilatero q1 = { { {4,1}, {4,3}, {10,3}, {10,1}} };
Quadrilatero q2;
q2.vertices[0].x = 4 ; q2.vertices[0].y = 1;
q2.vertices[1].x = 4 ; q2.vertices[1].y = 3;
q2.vertices[2].x = 10 ; q2.vertices[2].y = 3;
q2.vertices[3].x = 10 ; q2.vertices[3].y = 1;

```

---
### Estruturas como parâmetros de funções

Parâmetros por valor:
```
struct Ponto{
   double x, y;
};

struct Quadrilatero{
  Ponto vertices[4];
};

void print_ponto(Ponto p){
 cout << "(" << p.x << "," << p.y << ")";
}

void print_quadrilatero(Quadrilatero q){
  int i;
  for(i=0;i < 4;i++){
    print_ponto(q.vertices[i]) ;
    cout << endl ;
  }
}
```
---
### Estruturas como parâmetros de funções

Parâmetros por referência 
```
struct Ponto{
   double x, y;
};
struct Quadrilatero{
  Ponto vertices[4];
};

void ler_ponto(Ponto &p){
 cin >> p.x >> p.y;
}
void ler_quadrilatero(Quadrilatero &q){
    for(int i=0; i < 4 ; i++)
        ler_ponto(q[i]);
}
```

---
### Exemplo
Foi realizada uma pesquisa entre 100 habitantes de uma certa região. De cada
habitante foram coletados os dados: CPF, idade, sexo, salário e número de
filhos. Construa um programa C++ que armazene as informações da pesquisa e
calcule a média do salário dos habitantes e de filhos e liste os habitantes com
salário inferior a média e o número de filhos superior a média.

---
### Exemplo

Primeiro definimos a estrutura para armazenar os dados das pessoas:
```
struct Pessoa{
    char cpf[12];
    int idade;
    char sexo;
    float salario;
    int nfilhos;
};
```
---
### Exemplo

Podemos definir pelo menos 4 funções:
```cpp
void ler(Pessoa &P); // ler as informações de uma pessoa
void imprimir(Pessoa P); // imprimir as informações de uma pessoa
float mediaSalarios(Pessoa vp[], int n); // calcular a média dos salários
float mediaFilhos(Pessoa vp[], int n); // calcular a média do número de filhos
```
---
### Exemplo
Implementar as funções
```cpp
void ler(Pessoa &P){
    cin >> P.cpf >> P.idade >> 
    P.sexo >> P.salario >> P.nfilhos;
}
```

---
### Exemplo
Implementar as funções
```cpp
void imprimir(Pessoa P){
    cout<< "CPF: "<< P.cpf << " idade: " << P.idade
        << " sexo: " << P.sexo << " salário: " << P.salario
        << " número de filhos: " << P.nfilhos << endl ;
}
```

---
### Exemplo
Implementar as funções
```cpp
float mediaSalarios(Pessoa vp[], int n){
    float soma =0;
    for(int i=0 ; i < n ; i++){
        soma += vp[i].salario;
    }
    return soma / n ;
}
```

---
### Exemplo
Implementar as funções
```cpp
float mediaFilhos(Pessoa vp[], int n){
    int soma =0;
    for(int i=0 ; i < n ; i++){
        soma += vp[i].nfilhos;
    }
    return (float) soma / n ;
}
```

---
### Exemplo
Agora sim, podemos implementar a função `main`:
```cpp[1-5|7-9|11-15|17-23]
int main(){
    Pessoa dados[TAM];
    int n;
    float msalario, mfilhos;
    cin >> n;

    // Ler os dados das n pessoas
    for(int i=0 ; i < n ; i++)
        ler(dados[i]);

    // calcular as médias
    msalario = mediaSalarios(dados, n);
    mfilhos = mediaFilhos(dados, n);
    cout << "Média Salário: " << msalario
        << " Média Número de Filhos: " << mfilhos << endl;

    // Imprimir as pessoas
    for(int i=0 ; i < n ; i++){
        if(dados[i].salario < msalario &&
           dados[i].nfilhos > mfilhos)
            imprimir(dados[i]);

    }
    return 0;
}
```

---
### Teste

<https://multiprova.ufrn.br/>
