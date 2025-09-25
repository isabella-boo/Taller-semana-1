# Taller-semana-1
#include <stdio.h>
#include <string.h>

int main() {
    int id, stock, opcion, cantidad;
    float precio, ganancias = 0, descuento, precioFinal;
    char nombre[50];

    // Registro inicial del producto
    printf("=== REGISTRO DEL PRODUCTO ===\n");
    printf("Ingrese ID: ");
    scanf("%d", &id);
    getchar(); // limpiar buffer

    printf("Ingrese nombre: ");
    fgets(nombre, 50, stdin);
    nombre[strcspn(nombre, "\n")] = 0;

    printf("Ingrese cantidad en stock: ");
    scanf("%d", &stock);

    printf("Ingrese precio unitario: ");
    scanf("%f", &precio);

    // Menú principal
    do {
        printf("\n=== MENU PRINCIPAL ===\n");
        printf("1.\tVender producto\n");
        printf("2.\tReabastecer producto\n");
        printf("3.\tConsultar información\n");
        printf("4.\tMostrar ganancias\n");
        printf("5.\tSalir\n");
        printf("Seleccione una opción: ");
        scanf("%d", &opcion);

        if (opcion == 1) { 
            // Vender producto
            printf("\nIngrese cantidad a vender: ");
            scanf("%d", &cantidad);

            if (cantidad <= 0) {
                printf("Cantidad inválida.\n");
            } else if (cantidad <= stock) {
                printf("Ingrese descuento (0 a 100): ");
                scanf("%f", &descuento);
                if (descuento < 0 || descuento > 100) {
                    printf("Descuento inválido. Se aplicará 0%%.\n");
                    descuento = 0;
                }

                precioFinal = precio - (precio * (descuento / 100));
                stock -= cantidad;
                ganancias += cantidad * precioFinal;

                printf("\nVenta realizada:\n");
                printf("\tUnidades vendidas: %d\n", cantidad);
                printf("\tPrecio con descuento: %.2f\n", precioFinal);
                printf("\tStock restante: %d\n", stock);
            } else {
                printf("Stock insuficiente. Solo hay %d unidades.\n", stock);
            }

        } else if (opcion == 2) {
            // Reabastecer
            printf("\nIngrese cantidad a reabastecer: ");
            scanf("%d", &cantidad);
            if (cantidad > 0) {
                stock += cantidad;
                printf("Stock actualizado: %d\n", stock);
            } else {
                printf("Cantidad inválida.\n");
            }

        } else if (opcion == 3) {
            // Consultar
            printf("\n--- INFORMACION DEL PRODUCTO ---\n");
            printf("ID:\t%d\n", id);
            printf("Nombre:\t%s\n", nombre);
            printf("Stock:\t%d\n", stock);
            printf("Precio:\t%.2f\n", precio);

        } else if (opcion == 4) {
            // Ganancias
            printf("\nGanancias acumuladas: %.2f\n", ganancias);

        } else if (opcion == 5) {
            printf("\nSaliendo del programa...\n");

        } else {
            printf("\nOpción no válida. Intente nuevamente.\n");
        }

    } while(opcion != 5);

    return 0;
}
