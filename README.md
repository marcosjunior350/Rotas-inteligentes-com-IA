# Rota Inteligente: Otimização de Entregas com Algoritmos de IA

## 1. Descrição do Problema, Desafio Proposto e Objetivos

### O Problema

A empresa de delivery de alimentos "Sabor Express" enfrenta grandes desafios logísticos, especialmente durante os horários de pico. Atualmente, os percursos de entrega são definidos manualmente, com base na experiência dos entregadores, o que resulta em rotas ineficientes. Essa ineficiência gera atrasos nas entregas, aumento nos custos de combustível e, consequentemente, a insatisfação dos clientes.

### O Desafio

O desafio consiste em desenvolver uma solução inteligente, baseada em algoritmos de Inteligência Artificial, para sugerir as melhores e mais eficientes rotas para os entregadores. O projeto deve tratar a cidade como um grafo, onde locais são nós e ruas são arestas com pesos, e encontrar o menor caminho entre múltiplos pontos de entrega. Adicionalmente, em cenários de alta demanda, a solução deve ser capaz de agrupar entregas próximas para otimizar o trabalho de múltiplos entregadores.

### Objetivos

**Aumentar a Eficiência** - Reduzir o tempo total e a distância percorrida nas entregas. </br>
**Reduzir Custos Operacionais** - Diminuir os gastos com combustível através de rotas otimizadas.</br>
**Melhorar a Satisfação do Cliente** - Garantir entregas mais rápidas e pontuais.</br>
**Automatizar o Planejamento** - Substituir o planejamento manual de rotas por um sistema automatizado e inteligente.</br>

## 2. Explicação Detalhada da Abordagem Adotada

Para solucionar o desafio da "Sabor Express", eu dividi a abordagem em duas fases estratégicas principais:

1 - **Agrupamento de Entregas (Clustering):** Em momentos de alta demanda com múltiplos pedidos simultâneos, é ineficiente tratar cada pedido como um problema isolado. Por isso, utilizei um algoritmo de clustering para agrupar geograficamente os pontos de entrega. Cada cluster gerado representa uma "zona de entrega" que será atribuída a um único entregador. Essa estratégia otimiza a alocação de recursos, garantindo que cada entregador lide com pedidos que estão próximos entre si.</br>

2 - **Otimização de Rota (Pathfinding):** Após a definição dos clusters, o próximo passo é encontrar a rota mais eficiente dentro de cada um deles. Para isso, modelei a cidade como um grafo e apliquei um algoritmo de busca para encontrar o menor caminho que conecta o restaurante (ponto de partida) a todos os pontos de entrega do cluster e, por fim, retorna ao restaurante. Essa abordagem garante que, para cada entregador, a sequência de entregas seja a mais rápida e econômica possível.</br>

Essa solução combinada ataca o problema de forma sistêmica, primeiro organizando a demanda (clustering) e depois otimizando a execução (roteirização).

## 3. Algoritmos Utilizados

Para a implementação prática da solução, foram escolhidos os seguintes algoritmos clássicos de IA:

🔵 **K-Means (Agrupamento Não Supervisionado):**</br>

> **O que faz?** O K-Means foi utilizado para dividir o conjunto total de pontos de entrega em 'K' clusters distintos, onde 'K' pode representar o número de entregadores disponíveis. </br></br>
> **Como funciona?** O algoritmo agrupa os pontos de dados minimizando a distância entre os pontos e o centroide (o centro do cluster) de seu respectivo grupo. O resultado é um conjunto de clusters de entrega geograficamente coesos. </br>

🔵 **Algoritmo A\* (Busca com Heurística):**

> **O que faz?** O A* foi escolhido para encontrar o menor caminho entre dois pontos no nosso grafo (mapa da cidade). </br></br>
> **Como funciona?** É um algoritmo de busca de grafos que combina a eficiência da busca em largura (como no BFS) com uma heurística para guiar a busca na direção certa. Ele encontra o caminho de menor custo (distância ou tempo) de um nó inicial para um nó final, sendo ideal para o nosso problema de roteirização. Para resolver o problema de visitar *múltiplos* pontos dentro de um cluster, apliquei o A* sucessivamente, utilizando uma heurística simples (como "ir para o ponto mais próximo") para definir a sequência de visitas. </br>

## 4. Diagrama do Grafo - Modelo Usado na Solução

O diagrama criado está na pasta "img". Os nós (círculos) simbolizam o restaurante e os pontos de entrega, enquanto as arestas (linhas) representam as ruas. Cada aresta possui um peso, que pode ser a distância ou o tempo estimado de percurso.

## 5. Análise dos Resultados e Melhorias

### Eficiência da Solução

A solução implementada demonstrou ser eficaz na otimização das entregas para a "Sabor Express". Para um cenário com 8 pedidos e 2 entregadores, o algoritmo K-Means dividiu os pedidos em dois clusters geográficos coesos (Cluster 0 na região Sudoeste e Cluster 1 na Nordeste), conforme visualizado no gráfico de dispersão.

Para tornar a análise mais realista, defini uma escala onde cada ponto de peso no grafo equivale a 100 metros. Com base nisso, a otimização de rota com A* calculou os percursos mais eficientes para cada cluster, resultando em:

> **Rota do Entregador 1:** Distância total de 16.00 km.</br>
> **Rota do Entregador 2:** Distância total de 17.00 km.</br>

Essa abordagem automatizada elimina a ineficiência do planejamento manual e fornece rotas claras e otimizadas, reduzindo a distância total percorrida.

### Limitações Encontradas

A solução atual, embora funcional, possui algumas limitações:

> **Dados Estáticos:** O grafo não considera condições dinâmicas do trânsito, como congestionamentos ou acidentes.</br>
> **Capacidade do Entregador:** O modelo não leva em conta a capacidade da mochila de entrega (quantos pedidos cabem por vez).</br>
> **Janelas de Entrega:** Não considera horários específicos prometidos aos clientes.</br>

### Minhas Sugestões de Melhoria

Para evoluir o projeto, acredito que as seguintes melhorias poderiam ser implementadas:

> **Integração com APIs de Tráfego:** Utilizar APIs como Google Maps ou Waze para obter pesos dinâmicos para as arestas do grafo, ajustando as rotas em tempo real.</br>
> **Algoritmos Genéticos:** Explorar algoritmos heurísticos mais avançados, como os genéticos, para resolver o Problema do Caixeiro Viajante (TSP) de forma mais robusta dentro de cada cluster.</br>
> **Aprendizado por Reforço (RL):** Desenvolver um agente de RL que aprenda as melhores políticas de roteirização com base em dados históricos de entregas, considerando variáveis como horário e clima.</br>

Como o projeto tem apenas uma finalidade acadêmica, o desenvolvimento feito até o momento é suficiente para a resolução do desafio.


