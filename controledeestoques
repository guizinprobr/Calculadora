#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 1000

int main() {
    FILE *ponteiro;
    int op, i = 0, qtd[MAX], qtdr, encontrado;
    char item[MAX][50], resposta, itemremover[50];

    // Carrega o estoque do arquivo
    ponteiro = fopen("estoque.txt", "r");
    if (ponteiro != NULL) {
        while (fscanf(ponteiro, " %49[^\n]\n%d\n", item[i], &qtd[i]) == 2) {
            i++;
        }
        fclose(ponteiro);
    }

    do {
        system("cls");
        printf("=====================\n");
        printf("CONTROLE DE ESTOQUE\n");
        printf("=====================\n\n");
        printf("1. Adicionar item\n");
        printf("2. Remover item\n");
        printf("3. Listar estoque\n");
        printf("4. Sair\n\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &op);

        if (op < 1 || op > 4) {
            printf("Opcao invalida! Tente novamente.\n");
            system("pause");
            continue;
        }

        switch (op) {
            case 1:
                printf("Digite o nome do item: ");
                scanf(" %49[^\n]", item[i]);
                printf("Digite a quantidade: ");
                scanf("%d", &qtd[i]);

                // Adiciona item no vetor e salva no final do arquivo
                ponteiro = fopen("estoque.txt", "a");
                if (ponteiro == NULL) {
                    printf("Erro ao abrir arquivo para escrita.\n");
                    break;
                }
                fprintf(ponteiro, "%s\n%d\n", item[i], qtd[i]);
                fclose(ponteiro);

                i++; // próximo índice
                printf("Item adicionado com sucesso!\n");
                break;

            case 2:
                printf("Digite o nome do item a ser removido: ");
                scanf(" %49[^\n]", itemremover);
                encontrado = 0;

                for (int j = 0; j < i; j++) {
                    if (strcmp(item[j], itemremover) == 0) {
                        printf("Digite a quantidade a ser removida: ");
                        scanf("%d", &qtdr);

                        if (qtdr > qtd[j]) {
                            printf("Quantidade maior que o estoque! (%d disponivel)\n", qtd[j]);
                        } else {
                            qtd[j] -= qtdr;
                            printf("Quantidade atualizada: %d\n", qtd[j]);
                            if (qtd[j] == 0) {
                                for (int k = j; k < i - 1; k++) {
                                    strcpy(item[k], item[k + 1]);
                                    qtd[k] = qtd[k + 1];
                                }
                                i--;
                                printf("Item removido do estoque.\n");
                            }
                        }
                        encontrado = 1;
                        break;
                    }
                }

                if (!encontrado) {
                    printf("Item nao encontrado.\n");
                }

                // Regrava todo o arquivo
                ponteiro = fopen("estoque.txt", "w");
                for (int j = 0; j < i; j++) {
                    fprintf(ponteiro, "%s\n%d\n", item[j], qtd[j]);
                }
                fclose(ponteiro);
                break;

            case 3:
                if (i == 0) {
                    printf("Estoque vazio.\n");
                } else {
                    printf("===== ESTOQUE ATUAL =====\n");
                    printf("Nome\t\tQuantidade\n");
                    printf("-------------------------\n");
                    for (int j = 0; j < i; j++) {
                        printf("%-15s %d\n", item[j], qtd[j]);
                    }
                }
                break;

            case 4:
                printf("Saindo...\n");
                break;
        }

        if (op != 4) {
            printf("\nDeseja realizar outra operacao? (s/n): ");
            scanf(" %c", &resposta);
        } else {
            resposta = 'n';
        }

    } while (resposta == 's' || resposta == 'S');

    printf("Obrigado por usar o estoque!\n");
    return 0;
}
