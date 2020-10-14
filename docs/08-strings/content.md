## Cadeias de Caracteres
## Strings

---

## Objetivo da aula

Apresentar Strings em C++:
 - Leitura e escrita de Strings.
 - Exemplos de utilização de Strings.
 - Funções da biblioteca `cstring` de C++.

---

### Strings ou Cadeias de Caracteres

Vídeo  Cadeias de caracteres (strings) 17.12

---
<iframe width="1120" height="630" src="https://www.youtube.com/embed/GiDUeuyQqow?list=PLLjLO9s7KS4UBrOBelz0GyfiFn4CSqquH" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---
### Strings ou Cadeias de Caracteres

Strings são apenas _arranjos_ do tipo `char`

O __caractere de terminação__ é muito importante! (__`0`__ ou __`'\0'`__)

Para ler strings com espaços: 

```cpp
#include < iostream>
#define MAX_LENGTH 50
using namespace std;

int main(void){
    char str[MAX_LENGTH];
    cin.getline(str, MAX_LENGTH);
    cout << str << endl;  
    return 0;
}
```
---
### Outros tipos de vetores

Não esqueça que `cin` e `cout` não funcionam com vetores de outros tipos:

```cpp
int v[100];
cin >> v ; // ERRO!

for(int i=0; i < n ; i++)
    cin >> v[i] ; // Forma correta! 
```

Mas, com strings, funcionam:
```cpp
char s[100];
cin >> s ;
cin.getline(s, 100); // Com espaços

---
### Tamanho de uma string

- Podemos utilizar `strlen` (`#include <cstring>`):
```cpp
for (int i = 0 ; i < strlen(str) ; i++)
    ...
```

- ou podemos utilizar o caractere de terminação:

```cpp
i = 0;
while(str[i] != 0){ // ou != '\0'
    ...
    i++;
}
```

---
### Exemplo: Comparar 2 strings

Faça um programa que compara 2 strings digitadas pelo usuário. 

Depois veremos que existe uma função da biblioteca padrão que já faz isso!

A ideia: Percorrer as 2 strings e _comparar um por um_ os elementos

---
### Exemplo: Comparar 2 strings
Duas strings iguais:

```
'a' 'l' 'o' '\0' ....
 ^
 0

'a' 'l' 'o' '\0' ....
 ^
 0
```
---
### Exemplo: Comparar 2 strings

```
'a' 'l' 'o' '\0' ....
     ^
     1

'a' 'l' 'o' '\0' ....
     ^
     1
```
---
### Exemplo: Comparar 2 strings

```
'a' 'l' 'o' '\0' ....
         ^
         2

'a' 'l' 'o' '\0' ....
         ^
         2
```
---
### Exemplo: Comparar 2 strings

```
'a' 'l' 'o' '\0' ....
             ^
             3

'a' 'l' 'o' '\0' ....
             ^
             3
```
Os caracteres de terminação nas duas strings foram encontrados

As duas strings são, portanto, iguais

---
### Exemplo: Comparar 2 strings

Duas strings diferentes

```
'a' 'l' 'o' ' ' 'm' 'u' ....
 ^
 0

'a' 'l' 'a' '\0' ....
 ^
 0
```

---
### Exemplo: Comparar 2 strings

Duas strings diferentes

```
'a' 'l' 'o' ' ' 'm' 'u' ....
     ^
     1

'a' 'l' 'a' '\0' ....
     ^
     1
```
---
### Exemplo: Comparar 2 strings

Duas strings diferentes

```
'a' 'l' 'o' ' ' 'm' 'u' ....
         ^
         2

'a' 'l' 'a' '\0' ....
         ^
         2
```
2 caracteres diferentes

Não precisamos continuar: as strings são diferentes

---
### Exemplo: Comparar 2 strings
Cadeias de tamanhos diferentes:

```
'o' 'n' 'd' 'a' '\0'
 ^
 0

'o' 'n' 'd' 'a' 's' '\0'
 ^
 0
```
---
### Exemplo: Comparar 2 strings
Cadeias de tamanhos diferentes:

```
'o' 'n' 'd' 'a' '\0'
     ^
     1

'o' 'n' 'd' 'a' 's' '\0'
     ^
     1
```

---
### Exemplo: Comparar 2 strings
Cadeias de tamanhos diferentes:

```
'o' 'n' 'd' 'a' '\0'
         ^
         2

'o' 'n' 'd' 'a' 's' '\0'
         ^
         2
```

---
### Exemplo: Comparar 2 strings
Cadeias de tamanhos diferentes:

```
'o' 'n' 'd' 'a' '\0'
             ^
             3

'o' 'n' 'd' 'a' 's' '\0'
             ^
             3
```

---
### Exemplo: Comparar 2 strings
Cadeias de tamanhos diferentes:

```
'o' 'n' 'd' 'a' '\0'
                 ^
                 4

'o' 'n' 'd' 'a' 's' '\0'
                 ^
                 4
```

Encontramos um caracter diferente

Portanto, as strings são diferentes.

---
### Exemplo: Comparar 2 strings
- iniciar com `i=0`
- Quando parar? Quando o caractere de terminação é encontrado nas duas strings
```cpp
while(str1[i] !=0 || str2[i] != 0)
```
- O que fazer? Comparar `str1[i]` e `str2[i]`

---
### Exemplo: Comparar 2 strings

```cpp[1-10|11-15|16-17|18-24| 26-29]
#include < iostream>
#define TAM 50

using namespace std;

int main(){
    int i;
    char str1[TAM];
    char str2[TAM];
    bool iguais = true; // Determina se as strings são iguais ou não
    
    // Leer as duas strings
    cin.getline(str1,TAM);
    cin.getline(str2,TAM);
    i = 0;
    // Condição de parada: as 2 strings terminaram
    while(str1[i] !=0 || str2[i] != 0){
        // Se os caracteres são diferentes, as 2 strings são diferentes
        if(str1[i] != str2[i]){
            iguais = false;
            break;
        }
        i++;
    }

    if(iguais)
        cout << "as duas strings são iguais" << endl ;
    else
        cout << "as duas strings são diferentes" << endl ;

    return 0;
}
```

---
### Algumas Funções de Caracteres

Considere a biblioteca `cctype`

```cpp
#include < cctype>
// Converte para maiúsculo.
char x = toupper('a'); // x= 'A'

// Converte para minúsculo.
char x = tolower('A'); // x= 'a'

// Verificar que um caractere é um dígito decimal
b = isdigit('3') // b = true
b = isdigit('a') // b = false

```

---
### Exemplo: Converter uma string

Converter uma string de letras minúsculas em letras maiúsculas

1. percorrer cada um dos elementos da string
2. utilizar a função `toupper`

---
### Exemplo: Converter uma frase 
```cpp
int main(){
    char str[100];
    cin.getline(str, 100);

    for(int i=0; i< strlen(str);i++)
        str[i] = toupper(str[i]);

    cout << str << endl ;
    return 0;
}
```

---
###  Teste!
<https://multiprova.ufrn.br>
