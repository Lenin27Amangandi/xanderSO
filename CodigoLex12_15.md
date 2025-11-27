# Ejercicios Lex

## Ejercicio 1: Contar cuántos caracteres son letras mayúsculas, letras minúsculas, dígitos y espacios en blanco


%{
#include <stdio.h>
#include <stdlib.h>

int upper_case = 0;  // Contador de letras mayúsculas
int lower_case = 0;  // Contador de letras minúsculas
int digits = 0;      // Contador de dígitos
int spaces = 0;      // Contador de espacios
%}

UPPER [A-Z]
LOWER [a-z]
DIGIT [0-9]
SPACE [ \t]

%%

{UPPER}    { upper_case++; }
{LOWER}    { lower_case++; }
{DIGIT}    { digits++; }
{SPACE}    { spaces++; }

.          { /* Ignorar cualquier otro carácter */ }

%%

int main() {
    yylex();  // Ejecuta el análisis léxico

    // Mostrar los resultados
    printf("\nConteo de caracteres:\n");
    printf("Letras mayúsculas: %d\n", upper_case);
    printf("Letras minúsculas: %d\n", lower_case);
    printf("Dígitos: %d\n", digits);
    printf("Espacios: %d\n", spaces);

    return 0;
}


---

## Ejercicio 2:

%{
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

%}

ID      [a-zA-Z_][a-zA-Z0-9_]*
KEYWORD if|else|while|int
DIGIT   [0-9]+

%%

{KEYWORD} { printf("Palabra reservada: %s\n", yytext); }
{ID}      { printf("Identificador: %s\n", yytext); }
{DIGIT}   { printf("Número entero: %s\n", yytext); }

.         { printf("Error: Token no reconocido: %s\n", yytext); }

%%

int main() {
    yylex();  // Ejecuta el análisis léxico
    return 0;
}

%{
#include <stdio.h>
#include <stdlib.h>

%}

OP_ARITMETICOS [\+\-\*\/]
OP_RELACIONALES [<>!]=|==|<=|>=|!=

%%

{OP_ARITMETICOS}   { printf("Operador aritmético: %s\n", yytext); }
{OP_RELACIONALES}  { printf("Operador relacional: %s\n", yytext); }

.                   { printf("Error: Token no reconocido: %s\n", yytext); }

%%

int main() {
    yylex();  // Ejecuta el análisis léxico
    return 0;
}


## Ejercicio 3

%{
#include <stdio.h>
#include <stdlib.h>

%}

OP_ARITMETICOS [\+\-\*\/]
OP_RELACIONALES [<>!]=|==|<=|>=|!=

%%

{OP_ARITMETICOS}   { printf("Operador aritmético: %s\n", yytext); }
{OP_RELACIONALES}  { printf("Operador relacional: %s\n", yytext); }

.                   { printf("Error: Token no reconocido: %s\n", yytext); }

%%

int main() {
    yylex();  // Ejecuta el análisis léxico
    return 0;
}


-- Ejercicio 

%{
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

%}

UPPER [A-Z]
LOWER [a-z]

%%

{UPPER}    { printf("%c", tolower(yytext[0])); }
{LOWER}    { printf("%c", yytext[0]); }

.          { printf("%c", yytext[0]); }

%%

int main() {
    yylex();  // Ejecuta el análisis léxico
    return 0;
}

