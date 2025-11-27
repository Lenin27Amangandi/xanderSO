## Codigo Cataorse

%{
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<ctype.h>

int error_occurred = 0;  // Variable para controlar si ocurrió un error
%}

DIGITO    [0-9]
ID        [a-z][a-z0-9]*

%%

{DIGITO}+ {
    printf("Un Entero: %s (%d)\n", yytext, atoi(yytext));
}

{DIGITO}+"."{DIGITO}*  {
    char *endptr;
    double val = strtod(yytext, &endptr);
    if (*endptr == '\0') {  // Verificar si la conversión fue exitosa
        printf("Un Real: %s (%g)\n", yytext, val);
    } else {
        printf("Error: No se pudo convertir a un número real: %s\n", yytext);
        error_occurred = 1;  // Marcar que hubo un error
    }
}

"if"|"then"|"begin"|"end"|"procedure"|"function"  {
    printf("Palabra Clave: %s \n", yytext);
}

{ID}    {
    printf("Un identificador: %s \n", yytext);
}

"+"|"-"|"*"|"/" {
    printf("Un operador: %s\n", yytext);
}

"{"[^}\n]*"}"  // Se come una línea de comentarios
[\t\n]+   // Se come espacios en blanco

.        {
    printf("Caracter no reconocido: %s\n", yytext);
    error_occurred = 1;  // Marcar que hubo un error
}

%%

int main(int argc, char **argv)
{
    ++argv, --argc; // Se salta el nombre del programa
    if (argc > 0) {
        yyin = fopen(argv[0], "r");
        if (!yyin) {
            perror("Error al abrir el archivo");
            return 1;  // Terminar si el archivo no se puede abrir
        }
    } else {
        yyin = stdin;  // Usar entrada estándar si no se proporciona un archivo
    }

    yylex();

    if (error_occurred) {
        printf("\nSe encontraron errores durante el análisis.\n");
        return 1;
    }

    return 0;
}

---

## Codigo 13

%{
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<ctype.h>

// Definimos un error global
int error_occurred = 0;
%}

%%

^A.*    { printf("%s", yytext); }
.+      { printf(" "); }

%%

int main() {
    // Intentar ejecutar yylex() y verificar si ocurre un error
    if (setjmp(jmpbuf) != 0) {
        printf("\nError: Se ha producido un error de análisis.\n");
        return 1;  // Retornar código de error
    }
    
    // Llamada a yylex() para procesar el texto
    yylex();

    // Si no hubo error
    if (!error_occurred) {
        printf("\nAnálisis completado correctamente.\n");
    }
    
    return 0;
}

---

## Codigo 12

%{
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<ctype.h>

char c;  // Variable que no se está utilizando
%}

%%

[A-Z]    { printf("%c", tolower(yytext[0])); }   // Convierte mayúsculas a minúsculas
[a-z]    { printf("%c", toupper(yytext[0])); }   // Convierte minúsculas a mayúsculas
[^A-Za-z\t] { printf("%c", yytext[0]); }         // Si no es una letra, imprímelo tal cual

%%

int main() {
    // Manejo de errores al llamar a yylex()
    if (yylex() == 0) {
        printf("\nFin de archivo alcanzado sin errores.\n");
    } else {
        printf("\nSe produjo un error al procesar el texto.\n");
    }
    return 0;
}


---

## Codigo 11
%{
    int num_el = 0, num_ella = 0;
%}

%%

el      { num_el++; }
ella    { num_ella++; }
\n      { /* Saltamos las líneas nuevas */ }
[ \t]   { /* Ignoramos espacios y tabuladores */ }
[0-9]+  { printf("Error: Número no válido detectado: %s\n", yytext); } // Captura números
[A-Za-z]+ { printf("Error: Palabra no válida detectada: %s\n", yytext); } // Captura palabras no válidas
.       { printf("Error: Carácter no válido detectado: %s\n", yytext); } // Captura cualquier entrada no válida

%%

int main()
{
    yylex(); // Procesa la entrada
    printf("Número de 'el' independientes: %d\n", num_el);
    printf("Número de 'ella' en las frases: %d\n", num_ella);
    return 0;
}

---


## Codigo 10

%{
    int num_el = 0, num_ella = 0;
%}

%%

el      { num_el++; }
ella    { num_ella++; }
\n      { /* Saltamos las líneas nuevas */ }
[ \t]   { /* Ignoramos espacios y tabuladores */ }
.       { printf("Error: Palabra no válida detectada: %s\n", yytext); } // Captura cualquier entrada no válida

%%

int main()
{
    yylex(); // Procesa la entrada
    printf("Número de 'el' independientes: %d\n", num_el);
    printf("Número de 'ella' en las frases: %d\n", num_ella);
    return 0;
}

## Fin codido 10



%{
#include <stdio.h>
int total = 0;
int contador = 1;
%}
WS	[ \t]+
%%
I	{ total += 1; }
IV	{ total += 4; }
V	{ total += 5; }
IX	{ total += 9; }
X	{ total += 10; }
XL	{ total += 40; }
L	{ total += 50; }
XC	{ total += 90; }
C	{ total += 100; }
CD	{ total += 400; }
D	{ total += 500; }
CM	{ total += 900; }
M	{ total += 1000; }
{WS}	{ /* ignorar espacios */ }
\n	{ printf("Número romano %d: %d\n", contador++, total); total = 0; }
.	{ /* ignorar otros caracteres */ }
%%

int main()
{
    printf("CONVERSIÓN DE NÚMEROS ROMANOS A DECIMALES:\n");
    yylex();
    return 0;
}
