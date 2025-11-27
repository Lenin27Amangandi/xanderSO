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
