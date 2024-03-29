# Projeto "Mundo de Wumpus"

<img src="https://cdna.artstation.com/p/assets/images/images/059/177/696/large/elijah-kuzmichov-wumpus.jpg?1675808223" alt="Wumpus" width="900">


<div style="text-align: justify;">
Este projeto tem como objetivo cumprir as etapas proposta na disciplina de Inteligência Computacional e Inteligência Artificial, onde artavés da idéia do Mundo de Wumpus é abordada algums métodos para a resolução do problema determinado pelo jogo. Abaixo temos a descrição de cada umas das etapas.<br><br>
This project aims to fulfill the steps proposed in the discipline of Computational Intelligence and Artificial Intelligence, where through the idea of the World of Wumpus some methods for solving the problem determined by the game are approached. Below is a description of each of the steps.
</div>

## Etapa 1 - Gerador aleatório de ambientes do "Mundo de Wumpus"
- [x] Tamanho (n) = Ordem (n) da matriz quadrada (n >= 3). Linha e coluna = (n - 1)
- [x] Objetos: poços (p), Wumpus (W) e ouro (o). Quantidade? 
- [x] A partir dos objetos , posicionar no ambiente, também, as percepções geradas por cada um deles.
- [x] A casa (0, 0) é a única que não pode ter nenhum objeto, pois é a posição inicial do agente.
- [x] Onde houver poço não pode ser posicionado o ouro e o Wumpus. No entanto, estes podem ser posicionados 
em quaisquer uma das outras casas.

<div style="text-align: justify;">
Nesta etapa, primeiramente foi criado uma estrutura (Classe) denominada Mapa(), onde servirá como base para a contrução de um mapa para o mundo de wumpus nas demais etapas, foram definidos os seguintes atributos para a geração de uma matriz em um mapa:
</div>

* altura 
* largura 
* número de poços 
* número de monstros 
* número de ouros

<div style="text-align: justify;">
A partir destas definições, foram criadas funções internas na classe onde foi possível definir que a cada vez que for chamado o método de criação (__init__) da classe, será criada uma matriz AxL aleatória com o número pré-definido de elementos referentes ao game. Ao executar o main desta etapa, teremos por exemplo o seguinte resultado:
<div>
<br>
<p align="center">
<img src="src/etapa_1/img/print_exemplo_2.jpg" alt="Exemplo para a etapa 1" width="160">
</p>

Ou seja, é gerada a matriz e é exibida as suas caractristicas e a representação da mesma ao usuário.

## Etapa 2 - Agente Reativo (versão 1)
- [x] O comportamento do agente é definido a partir de seu conjuntos de regras:
      Se <percepções> então <ação>
- [x] Este conjunto de regras (ou base de conhecimento) deve ser especificado por meio de uma tabela.
- [x] A partir da especificação, o próximo passo é codificar o agente e integrar o 'gerador aleatório de ambientes', de forma a possibilitar a realização de testes de validação para posterior avaliação de peformance.

<div style="text-align: justify;">
Nesta etapa, foi criado o agente reativo, onde o mesmo deveria percorrer o mapa definido na etapa 1 e conforme as percepções que o mesmo recebia, o seu comportamento é influênciado dentro do jogo. Foi criado então a estrutura denominada Agente(), onde é passado como argumento o Mapa() criado anteriormente, com isso, temos a vinculação dos objetos principais do game, tanto o mapa, onde estarão todos os elementos posicionados para a interação, e o agente, que será o sujeito do cenário proposto.<br><br>
Após isso, foi inserido ao Mapa uma função de retornar as percepçoes conforme solicitado pelo agente, ou seja, quando o agente estiver em qualquer casa, ele simplesmente pode fazer uma requisição informando o seu local (x, y) para o mapa, e então o mesmo retornará as percepções decorrentes de cada casa na matriz, sem informar o elemento (ouro, poço, etc.) nas casas vizinhas.<br><br>
Ao receber as percepções, o agente escolhe entre as ações possíveis (andar, pegar, atirar) e toma a decisão para cada casa do mapa, o algoritmo permanece até o mesmo cair em um poço ou ser capturado pelo Wumpus. As ações foram escritas em forma de ifs, onde primeiramente prioriza o ouro, se não houver ouro na casa (percepção de brilho) ele toma outras decisões.<br><br>
Ao executar o main da etapa é gerado os dados gerais conforme o número de individuos gerados. Por padrão foi adotado 10.000 agentes, onde é retornado como exemplo as seguintes informações:
<div>
<br>      
<p align="center">
<img src="src/etapa_2/img/etapa_2_print.jpg" alt="Exemplo para a etapa 2" width="310">
</p>
<div style="text-align: justify;">Ou seja, são geradas e exibidas as informações totais sobre os agentes, podendo então determinar e avaliar o comportamento na qual tende o algoritmo criado.
<div>

## Etapa 3 - Agente Reativo (versão 2)
- [x] Estrutura de memória, que pode ser: uma lista; uma matriz - réplica do ambiente, com anotações feitas pelo agente; ou, outra estrutura de dados definida como mais adequada pela equipe.
- [x] Mecanismo mais inteligente para escolha da regra a ser aplicada, em caso de duas ou mais possíveis de serem utilizadas em determinado instante. Na primeira versão foi utilizada a Estratégia Aleatória. Logo, há liberdade para definir a melhor estratégia para essa finalidade.
- [x] Além disso, uso do conhecimento registrado na memória para auxiliar o processo de escolha da regra a ser aplicada (Inferência? Planejamento?).

<div style="text-align: justify;">
Nesta etapa, foi feito um update em relação a etapa anterior, onde foi inserida uma lista como forma de memória, ou seja, todas as casas na qual o agente passar, ele irá armazenar a localização na memória, assim, ao precisar passar novamente por esta casa o agente saberá que esta é uma localização de segurança.<br><br>
Durante a sua jornada, o agente pode chegar em um local onde ele define se irá por um caminho desconhecido ou conhecido, para isso foi implementado o atributo medo, este atributo pode ir de 1 a 10, quanto maior for o medo, mais o agente será cauteloso para com as casa desconhecidas, ou seja, irá preferir uma casa conhecida. Por padrão, esatbelecemos o medo do agente em 7, com isso ele será cauteloso, porém não deixará de descobrir novos caminhos sempre que achar necessário.<br><br>
Quando o main da etapa 3 é executado, gera dados como no exemplo a seguir:
<div>
<br>
<p align="center">
<img src="src/etapa_3/img/print_etapa_3.jpg" alt="Exemplo para a etapa 3" width="310">
</p>
<div style="text-align: justify;">Ou seja, são geradas e exibidas as informações totais sobre os agentes, podendo então determinar e avaliar o comportamento na qual tende o algoritmo criado.
<div>

## Etapa 4 - Agente de Aprendizagem
- [x] O mecanismo utilizado para a aprendizagem do Agente do Mundo de Wumpus deve ser idealizado e projetado via Algoritmos Genéticos para, posteriormente, ser codificado;
- [x] Cada componente ou processo do Algoritmo Genético deverá ser projetado com o foco na resolução do problema de “sair da casa (0,0), pegar o ouro e voltar à casa (0,0)';
- [x] Além do caminhando, deverão ser considerados os poços, ouro e wumpus (até o momento, temos um gerador aleatório de ambientes com dimensão n > 3);

<div style="text-align: justify;">Nesta última etapa, o agente terá o comportamento formado a partir de algoritimos genéticos (AGs), para isso, foi planejado uma função que gerência toda a parte do AG utilizado nesta estapa. A função myAG() recebe como argumento os seguintes atributos:
<div>

* tamanho da geracao 
* tamanho da sequencia máxima de movimentos 
* número de geracao 
* Mapa - refente a etapa 1 
* ploting - opção para gerar gráficos 
* text - opção para gerar textos (relatórios do que está acontecendo)

Com isso a função seguirá o seguinte algoritmo:
<p align="center">
<img src="src/etapa_4/img/screen.jpg" alt="Algoritmo etapa 4" width="300" style="filter: invert(1);">
</p>

Foi utilizado o operador genético de um ponto de corte:

<p align="center">
<img src="https://sites.icmc.usp.br/andre/research/genetic/image/cross_an.gif" alt="Algoritmo etapa 4" width="300">
</p>

<div style="text-align: justify;">
Por fim foram criadas duas funções de avaliação.<br>
Na primeira foi implementado apenas o objetivo de andar dentro do mapa, onde toda vez que o agente saia era penalizado e quando encontrava o wumpus ou um poço ele era eliminado, com isso foi possível obter resultados conforme o exemplo abaixo:
<div>
<br>

<div style="display: flex;">
  <img src="src/etapa_4/img/Figure_1.png" alt="Imagem 1" width="400">
  <img src="src/etapa_4/img/Figure_2.png" alt="Imagem 2" width="400">
</div>

<div style="text-align: justify;">
Após, foi implementada as ações pegar o ouro de forma não automática e de volta para a casa (0, 0). Onde era dada penalidade a cada movimento invalido e pontuação acrescida para o movimento válido. O exemplo a seguir apresenta a saída de um desses exemplos:<div>
<br>
<div style="display: flex;">
  <img src="src/etapa_4/img/Figure_3.png" alt="Imagem 1" width="400">
  <img src="src/etapa_4/img/Figure_4.png" alt="Imagem 2" width="400">
</div>

Com isso foi possível chegar a um resultado satisfatório a princípio, contudo, para indices de acertividade mais elevados talvez seja melhor apropriado outros tipo de operadores genéticos em possíveis atualizações, tendo em vista que muitas (na maior parte das vezes) o algoritmo fica travado na execução.






