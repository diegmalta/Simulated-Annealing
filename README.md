# Simulated Annealing e o Problema das N Rainhas

## Resumo
Trabalho de Inteligência Artificial, tentando resolver o Problema das N Rainhas utilizando o algoritmo Simulated Annealing.
## O Problema das N Rainhas
- O problema consiste em colocar um número n >= 2 de rainhas em um tabuleiro de xadrez, de forma que elas não se ataquem simultaneamente, e ao final possa se dizer quantas formas deste existam.

![Tabuleiros de xadrez representando o Problema das N Rainahs](https://gizmodo.uol.com.br/wp-content/blogs.dir/8/files/2017/09/n8riqfrjdnb5vndkpbf8.png)
Fonte: Wikimedia


## Algoritmo Hill Climbing
- Para facilitar a explicação do algoritmo Simulated Annealing, é interessante basear-se também na definição do algoritmo Hill Climbing.

- O algoritmo Hill Climbing é um algoritmo guloso cujo objetivo é encontrar uma configuração ótima ou que satisfaça as restrições de um determinado problema.

- Ele funciona realizando uma busca local que mantém um único estado corrente e tenta melhorá-lo analisando somente seus vizinhos e para quando nenhum vizinho for melhor que o estado corrente.

![Gráfico representação do Hill Climbing](https://miro.medium.com/v2/resize:fit:828/format:webp/0*yON268ZY1DQQd76S.png)
Fonte: https://www.researchgate.net/figure/Non-convex-registration-function-and-the-concept-of-local-and-global-optima_fig3_229022192

- O problema desse algoritmo é que, dependendo de qual for seu estado inicial, pode acabar ficando preso em um ponto de máximo (ou mínimo) local.

## Algoritmo Simulated Annealing
- Diferente do método Hill Climbing, que pode ficar preso num ponto crítico local, o Simulated Annealing permite que, eventualmente, estados piores possam ser explorados. Esse método remonta ao método de refino de um metal da forja, que se aproveita das altas temperaturas para moldar o metal da melhor forma possível conforme vai esfriando.

- O método funciona começando com uma temperatura elevada, permitindo que o algoritmo se mova livremente pelo espaço amostral. Quanto maior a temperatura, mais facilidade o algoritmo tem de se mover. Conforme a temperatura vai diminuindo, o algoritmo vai lentamente convergindo para o espaço de máximo (ou mínimo, dependendo de como for a implementação) que ele encontrou. 

- A temperatura deve diminuir lentamente, quanto mais rápido for a taxa de resfriamento, mais impreciso se torna o algoritmo, pois ele terá menos tempo para convergir pro ponto de maior (ou menor) valor local e trocar para outro.

- Esse algoritmo não garante obter uma solução ótima, se previamente não for informado qual o valor de máximo (ou mínimo) global. Se não há certeza de qual é o seu valor usando o algoritmo, uma alternativa é colocar um número alto de iterações e uma taxa mais lenta de resfriamento, aumentando em muito as chances do algoritmo de encontrar o máximo (ou mínimo) global (em troca de mais tempo de processamento), mas novamente, isso não garante 100% uma solução ótima como resultado.

- A cada iteração do algoritmo, um estado x’, vizinho do estado corrente x, é avaliado e aceito como próximo estado a ser considerado com a seguinte probabilidade:
```
100% se Δ <= 0
(e^(-Δ/T) * 100)% se Δ > 0
```
Onde  é a diferença de valores do estado vizinho analisado e o estado corrente e T a temperatura corrente.

## Implementação

- A modelagem do tabuleiro foi construída de forma simples: um tabuleiro NxN é representado por um vetor de inteiros de tamanho N, tal qual cada índice representa uma coluna do tabuleiro. Em cada índice há um inteiro, ele representa em qual linha do tabuleiro está a rainha.

- Esse modelo de tabuleiro foi escolhido pelos seguintes motivos:
    - Como se trata de posições de rainhas, um tabuleiro(bidimensional) pode ser representado por um vetor (unidimensional).
    - Além disso, como o problema das rainhas demanda que as rainhas não possam atacar umas as outras, duas rainhas não estarão na mesma coluna, então esse modelo elimina a necessidade de adicionar a restrição de estarem na mesma coluna.

- Após executar o algoritmo, além de retornar o resultado, ele imprime um pequeno relatório do que aconteceu durante sua execução;

- O algoritmo registra o número de vezes que o estado corrente:
    - foi para um estado melhor;
    - não mudou na iteração;
    - foi para um estado pior (aleatório);
- O programa imprime um gráfico com a trajetória do algoritmo até o resultado ótimo encontrado para melhor análise;

- Durante a execução, é notificado quando acontece uma troca aleatória, junto com os dados do nó corrente, próximo nó e probabilidade da troca.
