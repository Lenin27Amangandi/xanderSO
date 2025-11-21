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
