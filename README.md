# xanderSO
Para codigos de SO
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

#define NUM_PROC 3

void hijoHasAlgo(int numero);

int main() {
    int i, pid;
    int hijosEjecutados = 0;

    for (i = 1; i <= NUM_PROC; i++) {
        pid = fork();

        if (pid == -1) {
            fprintf(stderr, "Error al crear el proceso\n");
        } else if (pid == 0) {
            // Código del hijo
            hijoHasAlgo(i);
            exit(0); // Muy importante: el hijo termina aquí
        } else {
            // Código del padre
            hijosEjecutados++;
        }
    }

    // El padre espera a que terminen todos los hijos
    for (i = 0; i < hijosEjecutados; i++) {
        wait(NULL);
    }

    printf("Se ejecutaron %d procesos hijos.\n", hijosEjecutados);
    return 0;
}

void hijoHasAlgo(int numero) {
    int i, MAX = 10;
    printf("Ejecutando el hijo %d:\n", numero);
    for (i = 1; i <= MAX; i++)
        printf("%d\t", i);
    printf("\n");
}
