# Ejercicios Lex

## Ejercicio 12 Completo


%{
#include <stdio.h>
#include <stdlib.h>

int upper_case = 0;  // Contador de letras mayúsculas
int lower_case = 0;  // Contador de letras minúsculas
int digits = 0;      // Contador de dígitos
int spaces = 0;      // Contador de espacios

int total_upper_case = 0;  // Total de letras mayúsculas
int total_lower_case = 0;  // Total de letras minúsculas
int total_digits = 0;      // Total de dígitos
int total_spaces = 0;      // Total de espacios
%}

UPPER [A-Z]
LOWER [a-z]
DIGIT [0-9]
SPACE [ \t]

%%

{UPPER}    { upper_case++; total_upper_case++; }
{LOWER}    { lower_case++; total_lower_case++; }
{DIGIT}    { digits++; total_digits++; }
{SPACE}    { spaces++; total_spaces++; }

\n  {
    // Al final de cada línea, imprimir el conteo de dígitos de esa línea
    printf("\nConteo de caracteres en la línea:\n");
    printf("Letras mayúsculas: %d\n", upper_case);
    printf("Letras minúsculas: %d\n", lower_case);
    printf("Dígitos: %d\n", digits);
    printf("Espacios: %d\n", spaces);

    // Restablecer el conteo de la línea actual
    upper_case = 0;
    lower_case = 0;
    digits = 0;
    spaces = 0;
}

.  { /* Ignorar cualquier otro carácter */ }

%%

int main() {
    yylex();  // Ejecuta el análisis léxico

    // Mostrar el conteo total después de procesar todo el archivo
    printf("\nConteo total de caracteres:\n");
    printf("Letras mayúsculas: %d\n", total_upper_case);
    printf("Letras minúsculas: %d\n", total_lower_case);
    printf("Dígitos: %d\n", total_digits);
    printf("Espacios: %d\n", total_spaces);

    return 0;
}


---

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

