# Jokenpô

*IMPORTANTE: Este repositório é parte integrante da disciplina de Porgramação de Jogos em Rede do Curso Integrado em Programação de Jogos Digitais do IFRN - Campus Ceará-Mirim.*

## 1 Descrição do Projeto de Jogo

A descrição do projeto de jogo deverá reunir o conjunto de informações necessárias para comprender os dados gerados pelo jogo, as regras e os fluxos da jogada.

### 1.1 Regras do Jogo

- O jogo será disputado em uma melhor de 05 (cinco) turnos;
- O primeiro jogador a conseguir 3 vitórias ganha;
- Um turno não pode acabar em empate (caso haja empate, os jogadores jogam novamente até que haja um vencedor);

### 1.2 Regras do Turno

- Em cada turno, cada jogador irá escolher sua jogada (Pedra papel ou Tesoura);
- Será verificado o resultado conforme diagrama abaixo.
  
```mermaid
graph LR;
    Pe[Pedra];
    T[Tesoura];
    Pa[Papel];
    Pe -- Vence --> T;
    T -- Vence --> Pa;
    Pa -- Vence --> Pe;
```

## 2 Especificação do Jogo

### 2.1 Descrição dos dados do jogo

A descrição dos dados do jogo permite identificar o conjunto e o tipo das variáveis que precisaremos criar para o seu funcionamento.

- `vitorias_j1`
  - Armazena a quantidade de vitórias do jogador 1;
  - Valores possíveis: [0 - 3]
- `vitorias_j2`
  - Armazena a quantidade de vitórias do jogador 2;
  - Valores possíveis: [0 - 3]
- `turno_atual`
  - Armazena qual o turno atual;
  - Valores possíveis: [0 - 5]
- `jogada_j1`
  - Armazena a jogada atual do jogador 1;
  - Valores possíveis: [Pedra, Papel, Tesoura]
- `jogada_j2`
  - Armazena a jogada atual do jogador 2;
  - Valores possíveis: [Pedra, Papel, Tesoura]
- `resultado_disputa`
  - Armazena o resultado da disputa
  - Valores possíveis: [vitoria_j1, empate, vitoria_j2]

### 2.2 Descrição do fluxo do jogo (local)

```mermaid
flowchart TD;
    ini((Início));
    fim((Fim));
    ini_var[Inícia Variáveis
            vitorias_j1 = 0
            vitorias_j2 = 0
            turno_atual = 0];
    novo_turno[Novo Turno
               turno_atual += 1];
    jogadas[Aguarda Jogadas
            dos Jogadores
            atualiza jogada_j1
            autaliza jogada_j2];
    disputa{Realiza 
            disputa};
    vitoria_j1[Vitória do
               Jogador 1
               vitorias_j1 += 1];
    vitoria_j2[Vitória do
               Jogador 1
               vitorias_j2 += 1];
    empate[Realizar nova
           disputa];
    acabou{Verifica se o
           jogo encerrou
           vitorias_j1 == 3 OU
           vitorias_j2 == 3?};
    exibe_vencedor[Exibe
                   Vencedor];

    ini --> ini_var;
    ini_var --> novo_turno;
    novo_turno --> jogadas;
    jogadas --> disputa;
    disputa -- vitoria_j1 --> vitoria_j1;
    disputa -- vitoria_j2 --> vitoria_j2;
    disputa -- empate --> empate;
    empate --> jogadas;
    vitoria_j1 --> acabou;
    vitoria_j2 --> acabou;
    acabou -- Sim --> exibe_vencedor;
    acabou -- Não --> novo_turno
    exibe_vencedor --> fim;
```
