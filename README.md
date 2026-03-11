     #include <stdio.h>
       #include <stdlib.h>
      int main() {
    int idade;
    int num_eixos;
    int opcao_seguro;
    char tipo_seguro[20];

    double valor_base = 1000.00;
    double adicional_categoria_perc = 20.0;
    double adicional_categoria_valor;

    double adicional_idade_perc;
    double adicional_idade_valor;

    double cobertura_perc_por_eixo;
    double cobertura_valor;

    double valor_total;
    do {
        printf("Idade do condutor principal: ");
        if (scanf("%d", &idade) != 1 || idade < 18) {
            printf("Idade invalida. Digite um numero inteiro >= 18.\n");
            while (getchar() != '\n'); // limpar buffer
        } else {
            break;
        }
    } while (1);

    do {
        printf("Numero de eixos do veiculo: ");
        if (scanf("%d", &num_eixos) != 1 || num_eixos < 2) {
            printf("Numero de eixos invalido. Minimo: 2.\n");
            while (getchar() != '\n');
        } else {
            break;
        }
    } while (1);

    // === Tipo de seguro ===
    printf("\nEscolha o tipo de cobertura:\n");
    printf("1 - Seguro Basico\n");
    printf("2 - Seguro Parcial\n");
    printf("3 - Seguro Completo\n");

    do {
        printf("Opcao (1-3): ");
        if (scanf("%d", &opcao_seguro) != 1 || opcao_seguro < 1 || opcao_seguro > 3) {
            printf("Opcao invalida. Escolha 1, 2 ou 3.\n");
            while (getchar() != '\n');
        } else {
            break;
        }
    } while (1);

    switch (opcao_seguro) {
        case 1:
            sprintf(tipo_seguro, "Basico");
            cobertura_perc_por_eixo = 3.0;
            break;
        case 2:
            sprintf(tipo_seguro, "Parcial");
            cobertura_perc_por_eixo = 5.0;
            break;
        case 3:
            sprintf(tipo_seguro, "Completo");
            cobertura_perc_por_eixo = 10.0;
            break;
    }


    adicional_categoria_valor = valor_base * (adicional_categoria_perc / 100.0);

    if (idade < 25) {
        adicional_idade_perc = 15.0;
    } else if (idade <= 29) {
        adicional_idade_perc = 10.0;
    } else {
        adicional_idade_perc = 5.0;
    }
    adicional_idade_valor = valor_base * (adicional_idade_perc / 100.0);

    cobertura_valor = (cobertura_perc_por_eixo * num_eixos / 100.0) * valor_base;

    valor_total = valor_base + adicional_categoria_valor + adicional_idade_valor + cobertura_valor;

    printf("\n==================================================\n");
    printf("           RELATORIO DO SEGURO - CARGA PESADA\n");
    printf("==================================================\n");
    printf("Valor Base:                       R$ %10.2f\n", valor_base);
    printf("Adicional Categoria (%4.0f%%):      R$ %10.2f\n", adicional_categoria_perc, adicional_categoria_valor);
    printf("Adicional Idade     (%4.0f%%):      R$ %10.2f\n", adicional_idade_perc, adicional_idade_valor);
    printf("Cobertura %s (%4.0f%% por eixo x %d): R$ %10.2f\n",
           tipo_seguro, cobertura_perc_por_eixo, num_eixos, cobertura_valor);
    printf("--------------------------------------------------\n");
    printf("VALOR TOTAL FINAL:                R$ %10.2f\n", valor_total);
    printf("==================================================\n\n");
    return 0;
}
