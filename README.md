#include <stdio.h>
#include <string.h>

// Estrutura da carta
typedef struct {
    char nome[20];
    int estetica;
    int investimento;
    int riqueza;
} Carta;

// Função para mostrar uma carta
void mostrarCarta(Carta c) {
    printf("Carta: %s\n", c.nome);
    printf(" Estética: %d\n Investimento: %d\n Riqueza: %d\n",
           c.estetica, c.investimento, c.riqueza);
}

// Função para comparar um atributo
void compararAtributo(char *nomeAtributo, int val1, int val2, char *nome1, char *nome2) {
    printf("%s: ", nomeAtributo);
    if (val1 > val2)
        printf("%s venceu!\n", nome1);
    else if (val1 < val2)
        printf("%s venceu!\n", nome2);
    else
        printf("Empate!\n");
}

int main() {
    // Cartas disponíveis
    Carta cartas[3] = {
        {"São Gonçalo", 80, 70, 90},
        {"Niterói",     75, 85, 60},
        {"Maricá",      85, 60, 80}
    };

    int escolha1, escolha2;

    printf("=== Cartas Disponíveis ===\n");
    for (int i = 0; i < 3; i++) {
        printf("%d - %s\n", i + 1, cartas[i].nome);
    }

    // Escolha das cartas
    printf("\nEscolha a carta do Jogador 1 (1-3): ");
    scanf("%d", &escolha1);
    escolha1--;

    printf("Escolha a carta do Jogador 2 (1-3, diferente do Jogador 1): ");
    scanf("%d", &escolha2);
    escolha2--;

    if (escolha1 < 0 || escolha1 > 2 || escolha2 < 0 || escolha2 > 2 || escolha1 == escolha2) {
        printf("Escolha inválida de cartas!\n");
        return 1;
    }

    Carta c1 = cartas[escolha1];
    Carta c2 = cartas[escolha2];

    printf("\n--- Carta do Jogador 1 ---\n");
    mostrarCarta(c1);

    printf("\n--- Carta do Jogador 2 ---\n");
    mostrarCarta(c2);

    // Escolha do atributo para comparação direta
    int atributo;
    printf("\n--- Escolha o atributo para comparar ---\n");
    printf("1 - Estética\n2 - Investimento\n3 - Riqueza\n");
    printf("Digite sua escolha: ");
    scanf("%d", &atributo);

    printf("\n--- Resultado da Comparação ---\n");

    switch (atributo) {
        case 1:
            compararAtributo("Estética", c1.estetica, c2.estetica, c1.nome, c2.nome);
            break;
        case 2:
            compararAtributo("Investimento", c1.investimento, c2.investimento, c1.nome, c2.nome);
            break;
        case 3:
            compararAtributo("Riqueza", c1.riqueza, c2.riqueza, c1.nome, c2.nome);
            break;
        default:
            printf("Atributo inválido!\n");
            return 1;
    }

    // Comparação geral dos 3 atributos
    int pontos1 = 0, pontos2 = 0;

    if (c1.estetica > c2.estetica) pontos1++;
    else if (c1.estetica < c2.estetica) pontos2++;

    if (c1.investimento > c2.investimento) pontos1++;
    else if (c1.investimento < c2.investimento) pontos2++;

    if (c1.riqueza > c2.riqueza) pontos1++;
    else if (c1.riqueza < c2.riqueza) pontos2++;

    printf("\n--- Resultado Final (Melhor de 3) ---\n");
    if (pontos1 > pontos2)
        printf("%s venceu a rodada!\n", c1.nome);
    else if (pontos1 < pontos2)
        printf("%s venceu a rodada!\n", c2.nome);
    else
        printf("Rodada empatada!\n");

    return 0;
}
