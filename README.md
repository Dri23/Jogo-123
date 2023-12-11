class Tabuleiro:
    def __init__(self):
        self.tabuleiro = [[' ' for _ in range(3)] for _ in range(3)]  # Inicializa o tabuleiro vazio

    def imprimir_tabuleiro(self):
        for linha in self.tabuleiro:
            print('|'.join(linha))
            print('-' * 5)

    def verificar_vitoria(self, jogador):
        # Verifica vitória por linhas, colunas e diagonais
        for i in range(3):
            if all(self.tabuleiro[i][j] == jogador for j in range(3)) or \
               all(self.tabuleiro[j][i] == jogador for j in range(3)):
                return True

        if all(self.tabuleiro[i][i] == jogador for i in range(3)) or \
           all(self.tabuleiro[i][2 - i] == jogador for i in range(3)):
            return True

        return False

    def realizar_jogada(self, linha, coluna, jogador):
        if 0 <= linha < 3 and 0 <= coluna < 3 and self.tabuleiro[linha][coluna] == ' ':
            self.tabuleiro[linha][coluna] = jogador
            return True
        else:
            return False


class JogoDaVelha:
    def __init__(self):
        self.tabuleiro = Tabuleiro()
        self.jogador_atual = 'X'

    def alternar_jogador(self):
        self.jogador_atual = 'O' if self.jogador_atual == 'X' else 'X'

    def jogar(self):
        while True:
            self.tabuleiro.imprimir_tabuleiro()

            linha = int(input(f'Jogador {self.jogador_atual}, informe a linha (0, 1, 2): '))
            coluna = int(input(f'Jogador {self.jogador_atual}, informe a coluna (0, 1, 2): '))

            if self.tabuleiro.realizar_jogada(linha, coluna, self.jogador_atual):
                if self.tabuleiro.verificar_vitoria(self.jogador_atual):
                    self.tabuleiro.imprimir_tabuleiro()
                    print(f'Jogador {self.jogador_atual} venceu!')
                    break
                elif ' ' not in [item for linha in self.tabuleiro.tabuleiro for item in linha]:
                    self.tabuleiro.imprimir_tabuleiro()
                    print('Empate!')
                    break

                self.alternar_jogador()
            else:
                print('Jogada inválida. Tente novamente.')


# Executar o jogo
jogo = JogoDaVelha()
jogo.jogar()
