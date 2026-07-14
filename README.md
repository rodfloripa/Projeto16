
# Projeto16

# 1. Otimização Geométrica de Trajetórias utilizando Monte Carlo e Critério de Metropolis

<p align="justify">
Este projeto apresenta uma abordagem de otimização geométrica para planejamento de trajetórias utilizando busca estocástica baseada no critério de Metropolis. O objetivo é construir um caminho entre um ponto de origem e um ponto de destino passando por um conjunto de pontos intermediários, enquanto mantém uma distância mínima de segurança em relação a obstáculos distribuídos no ambiente. A solução combina conceitos de Álgebra Linear, Geometria Computacional, Métodos de Monte Carlo e otimização probabilística para explorar diferentes trajetórias e selecionar aquelas que melhor satisfazem as restrições do problema.
</p>

![thermo](https://github.com/rodfloripa/Projeto16/blob/master/dist.png)

<p align="center">
Fig. 1 – Trajetória encontrada pelo algoritmo e evolução da distância percorrida ao longo das iterações.
</p>

---

# 2. Objetivo

<p align="justify">
O problema consiste em encontrar uma trajetória entre um ponto de origem e um ponto de destino utilizando um conjunto de pontos intermediários disponíveis. Durante toda a construção da trajetória, cada segmento deve manter uma distância mínima em relação aos obstáculos representados pelos pontos vermelhos. Entre todas as trajetórias válidas encontradas, o algoritmo procura selecionar aquela com menor comprimento total.
</p>

---

# 3. Representação do Problema

<p align="justify">
O ambiente é composto por dois conjuntos distintos de pontos. Os pontos azuis representam os locais que podem ser utilizados para compor a trajetória, enquanto os pontos vermelhos representam obstáculos cuja proximidade deve ser limitada por uma distância mínima definida pelo usuário.
</p>

<p align="justify">
A entrada do algoritmo consiste apenas nas coordenadas cartesianas desses pontos e no valor mínimo permitido entre qualquer segmento da trajetória e cada obstáculo.
</p>

---

# 4. Cálculo da Projeção Ortogonal

<p align="justify">
O núcleo matemático do algoritmo está na função <code>point_on_line()</code>, responsável por calcular a projeção ortogonal de um obstáculo sobre cada segmento da trajetória.
</p>

<p align="justify">
A projeção é obtida utilizando Álgebra Linear por meio da projeção vetorial:
</p>

```text
proj = ((u · v) / ||v||²) · v + a
```


<p align="justify">
onde:
</p>

- <b>a</b> representa o ponto inicial do segmento;
- <b>b</b> representa o ponto final do segmento;
- <b>p</b> representa o obstáculo;
- <b>u · v</b> é o produto escalar entre os vetores;
- <b>||v||²</b> é o quadrado da norma do vetor do segmento.

<p align="justify">

<p align="justify">
Após calcular essa projeção, o algoritmo mede a distância entre o obstáculo e o ponto projetado. Caso a projeção esteja fora do segmento analisado, essa distância é desconsiderada. Dessa forma é possível determinar se o segmento respeita ou não a distância mínima de segurança.
</p>

---

# 5. Construção da Trajetória

<p align="justify">
O algoritmo inicia escolhendo aleatoriamente um ponto de origem e um ponto de destino entre os pontos disponíveis. Em seguida, novos pontos intermediários são selecionados de forma aleatória para construir uma trajetória candidata.
</p>

<p align="justify">
Sempre que um novo segmento é criado, são calculadas as distâncias entre esse segmento e todos os obstáculos presentes no ambiente. Dessa forma, o algoritmo acompanha continuamente o comprimento total da trajetória e verifica se todas as restrições geométricas continuam sendo satisfeitas.
</p>

---

# 6. Busca Baseada em Monte Carlo

<p align="justify">
Em vez de explorar todas as possibilidades existentes, o algoritmo utiliza uma estratégia probabilística inspirada nos Métodos de Monte Carlo. Diversas trajetórias são geradas aleatoriamente ao longo das iterações, permitindo explorar diferentes regiões do espaço de soluções sem necessidade de realizar busca exaustiva.
</p>

<p align="justify">
Essa abordagem reduz significativamente o custo computacional quando comparada à avaliação completa de todas as combinações possíveis de caminhos.
</p>

---

# 7. Critério de Metropolis

<p align="justify">
Após construir uma trajetória candidata, o algoritmo compara seu comprimento com a melhor solução encontrada até aquele momento.
</p>

<p align="justify">
Mesmo quando a nova trajetória apresenta comprimento maior, ela ainda pode ser aceita com determinada probabilidade calculada pelo critério de Metropolis. Esse mecanismo aumenta a diversidade das soluções exploradas e evita que o algoritmo permaneça preso em soluções locais durante a busca.
</p>

<p align="justify">
A decisão de aceitar ou rejeitar uma nova trajetória é realizada por meio de um experimento probabilístico utilizando distribuição binomial, permitindo que o processo de otimização explore continuamente diferentes alternativas.
</p>

---

# 8. Fluxo do Algoritmo

<p align="justify">
O funcionamento geral do algoritmo pode ser resumido nas seguintes etapas:
</p>

1. gerar aleatoriamente os pontos do ambiente;
2. selecionar origem e destino;
3. construir uma trajetória candidata;
4. calcular a distância de cada segmento até todos os obstáculos;
5. verificar se a restrição mínima é respeitada;
6. calcular o comprimento total da trajetória;
7. aplicar o critério de Metropolis para decidir se a solução será armazenada;
8. repetir o processo durante milhares de iterações;
9. apresentar a melhor trajetória encontrada.

---

# 9. Visualização dos Resultados

<p align="justify">
O projeto produz duas visualizações simultaneamente. A primeira mostra a trajetória final encontrada entre origem e destino, indicando também a distância de cada obstáculo em relação aos segmentos da rota. A segunda apresenta a evolução do comprimento das trajetórias aceitas ao longo das iterações, permitindo acompanhar visualmente o comportamento da busca probabilística durante a otimização.
</p>

---

# 10. Aplicações

<p align="justify">
Embora seja apresentado em um ambiente bidimensional simplificado, o método empregado pode ser adaptado para diversos problemas reais envolvendo planejamento de trajetórias e otimização geométrica. Entre suas aplicações destacam-se planejamento de rotas para robôs móveis, navegação autônoma de drones, definição de caminhos para veículos autônomos, planejamento de inspeções industriais, movimentação segura em ambientes com obstáculos e problemas gerais de otimização espacial.
</p>

---

# 11. Tecnologias Utilizadas

<p align="justify">
O projeto foi desenvolvido em Python utilizando bibliotecas científicas amplamente empregadas em computação científica e otimização.
</p>

- NumPy
- SciPy
- Matplotlib
- Random
- Math
- Collections

---

# 12. Conclusão

<p align="justify">
Este projeto demonstra como técnicas de Geometria Computacional, Álgebra Linear e Métodos de Monte Carlo podem ser integradas para resolver problemas de planejamento de trajetórias sujeitos a restrições espaciais. A utilização do critério de Metropolis permite explorar diferentes soluções durante a busca, favorecendo a descoberta de trajetórias de menor comprimento sem recorrer à exploração exaustiva de todas as possibilidades. Como resultado, obtém-se uma abordagem elegante e eficiente para problemas de otimização geométrica, ilustrando conceitos importantes de otimização estocástica aplicáveis em áreas como robótica, navegação autônoma, pesquisa operacional e inteligência computacional.
</p>
```
