---
layout: post
title:  "Método de Puls"
date:   2020-05-20 00:00:00
description: Neste post trago os passos para implementação do método com planilha e código no MatLab para interpolação.
img: hidrogramaAmortecidoArtigo.JPG # Add image post (optional)
mathjax: true
---

Quando se analisa o problema do abatimento de hidrogramas em reservatórios, depara-se com um problema de escoamento não permanente. O escoamento é caracterizado por uma grande profundidade e, consequentemente, baixa velocidade, de modo que os termos dinâmicos da equação dinâmica do escoamento são desprezíveis (TUCCI, 2007).

A forma amplamente difundida na bibliografia deve-se ao trabalho de Puls (1928) e Puls (1947), divulgado posteriormente de forma mais ampla como método de Puls modificado (BUTLER, 1957). 

A água que entra no reservatório ao longo do tempo se refere a vazão afluente e fica temporariamente armazenada para sair pela tubulação, para então ser chamada de vazão efluente. Esta deve ser menor que aquela como decorrência do armazenamento. Essa redução de vazão é chamada de atenuação ou laminação. E o procedimento para calcular seu valor é chamado de propagação.

O Modelo de Puls caracteriza-se por supor que existe uma relação entre o volume armazenado e a vazão efluente, sendo esta, portanto, independente da vazão afluente. Isso equivale a assumir que a superfície do reservatório se mantenha plana e horizontal, o que é em muitos casos apenas uma aproximação dada a existência do remanso.

Para determinar a propagação dos cursos d'água em reservatórios, ou seja, bacias de detenção, o Método de Puls é amplamente utilizado. Ele consiste na equação da continuidade, que é um balanco da água que entra e da aguá que sai. Ele consiste na discretização do tempo, ou seja, passa-se de uma equação infinita (derivada) para finita (intervalo de tempo $$\Delta$$t), podendo ocorrer erros nos resultados devido a esse fato. Quanto maior a discretização de tempo maior as chances de ocorrer um erro. Nos exemplos utilizados é necessário que a vazão de pico seja um ponto na tabela de propagação, para isso temos que discretizar o tempo de uma forma coerente.

\begin{equation}
\label{eq:eqcContinuidade1}\tag{1}
I - O = \frac{\Delta S}{\Delta t} 
\end{equation}


Onde:\\
I: vazão média afluente ao reservatório durante o tempo $$\Delta$$t ($$m^3$$/s);\\
O: vazão média efluente do reservatório durante o tempo $$\Delta$$t ($$m^3$$/s);\\
$$\Delta$$S: variação no volume do reservatório durante o tempo $$\Delta$$t ($$m^3$$);\\
$$\Delta$$t: período incremental (s).

Para resolver a equação \ref{eq:eqcContinuidade1}, primeiro reescreva para uma forma mais prática:

\begin{equation}
\label{eq:eqcContinuidade2}\tag{2}
\frac{I_{1}+I_{2}}{2}+\frac{O_{1}+O_{2}}{2}=\frac{S_{2}+S_{1}}{\Delta t} 
\end{equation}

Os subscritos 1 e 2 denotam o início e o fim, respectivamente, do período $\Delta$t escolhido. Os termos na equação \ref{eq:eqcContinuidade2} podem agora ser reorganizados como:

\begin{equation}
\label{eq:eqcContinuidade3}\tag{3}
\left (I_{1} + I_{2}  \right ) + \left [\frac{2S_{1}}{\Delta t} - O_{1}  \right ] = \frac{2S_{2}}{\Delta t} + O_{2}
\end{equation}

Na equação \ref{eq:eqcContinuidade3}, todos os termos a esquerda são conhecidos de cálculos anteriores de propagação, enquanto os termos a direita são desconhecidos e devem ser determinados pela propagação em reservatório. Supõe-se, que:

* A superfície da água nesse método é horizontal;
* A vazão efluente é uma função única do volume de armazenamento;
* A vazão efluente varia linearmente com o tempo, durante cada período $$\Delta$$t. 

Com base na duração do ramo ascendente do hidrograma de entrada, um período $$\Delta$$t será escolhido. Então, é feito uma combinação dos termos conhecidos para criar duas relações: gráficos de O versus 2S/$$\Delta$$t + O e versus de 2S/$$\Delta$$t – O (figura [1](#vazaoVersus2VolumeDeltat)) para achar a vazão de saída.
<a name="vazaoVersus2VolumeDeltat"></a>

![hidrogramaSCS]({{site.baseurl}}/assets/img/vazaoVersus2VolumeDeltat.JPG)
*Figura 1: Gráfico de O versus 2S/∆t+ O e de O versus 2S/∆t– O* 

No projeto de uma bacia de detenção, a equação \ref{eq:eqcContinuidade3} é usada no calculo do hidrograma de saída quando se conhece o hidrograma de entrada. Esse cálculo constitui uma propagação. Se a bacia de detenção não produzir os resultados pretendidos, os parâmetros devem ser revisados, procedendo-se então a uma outra propagação. Assim, o processo é de tentativa e erro até calibrar os melhores parâmetros.

## Aplicação do Modelo

Para aplicação do modelo foi dimensionado um reservatório para suportar o dobro da sua capacidade de volume que é aproximadamente 6.000 $$m^3$$, área total construída de 5.157,12 $$m^2$$, altura da arquibancada de 2,70m, com degraus de 80x45cm, cota da soleira do vertedouro de 1,50m, largura da soleira de 5m, para quatro orifícios de 30cm de diâmetro (figura [2 e 3](#plantaReservatorio6000m3)).
<a name="plantaReservatorio6000m3"></a>

![hidrogramaSCS]({{site.baseurl}}/assets/img/plantaReservatorio6000m3.JPG)
*Figura 2: Planta baixa do reservatório de 6.000 m³.*
![hidrogramaSCS]({{site.baseurl}}/assets/img/vistaReservatorio6000m3.JPG)
*Figura 3: Vista do reservatório de 6.000 m³.* 

O diâmetro do orifício é algo que deve ser levado em consideração. É necessária a colocação de grelha para cobrir o tubo, como vivemos numa sociedade em que o vandalismo predomina, tubos com diâmetros muito grande podem representar perigo para os transeuntes, pois se arrancadas as grelhas, ficam buracos enormes nos quais uma criança pode cair durante uma chuva com uma lâmina d’água. 

Segundo Gribbin (2009), o coeficiente de descarga, $$C_{d}$$, é uma constante de proporcionalidade adimensional, responsável pela redução do fluxo em razão da perda de carga na entrada. O valor experimental de $$C_{d}$$ para orifícios de borda reta varia de acordo com o tamanho, a forma e a quantidade de carga. No entanto, para a maioria das aplicações, resultados confiáveis podem ser obtidos com o uso de $$C_{d}$$ = 0,62.

Com os dados de dimensionamento do reservatório, foi criado a tabela \ref{tab:cotaxvolumexvazao} para relacionar a cota, área e volume, gerando o gráfico da figura \ref{fig:cotaxvolumexvazao} que mostra o aumento do volume até a cota de capacidade máxima do reservatório, o volume de água a mais que entrar será extravasado pelo vertedouro. 

A tabela \ref{tab:calculoPropagacao} traz informações dos parâmetros de propagação. O cálculo da vazão esta diretamente ligado a diferença de cota, sendo que, até a cota da soleira do vertedouro o orifício atua sozinho, quando a capacidade máxima do reservatório é atingida passa a atuar em conjunto o orifício e vertedouro (figuras \ref{fig:cotaxvazao} e \ref{fig:vazaoxvolume}). Os parâmetros (2S/$$\Delta$$t)+0 e (2S/$$\Delta$$t)-0 ajudam a encontrar a vazão de saída em relação ao tempo (Figura \ref{fig:parametrosBaciaDetencao}). 

Com a informação do hidrograma de projeto é possível fazer a tabela \ref{tab:propagacao} para achar a vazão amortecida devido o uso do reservatório, a figura \ref{fig:hidrogramaEntradaSaida} é utilizada pra analisar a diferença do pico da vazão em cada hidrograma, observe que a vazão efluente máxima ocorre no ponto onde o hidrograma de saída cruza o hidrograma de entrada. Essa é uma característica das propagações de reservatório. No hidrograma de saída o aumento da vazão aconteceu devido a utilização do vertedouro no instante de tempo aproximado de 33 minutos.

Note também que a vazão efluente máxima de 2,067$$m^3$$/s corresponde a uma elevação máxima de reservatório de aproximadamente 2 metros, que pode ser determinado interpolando a taxa de descarga em relação a cota. Essa elevação se tornaria então o nível de água de projeto na bacia de detenção.

Finalmente, observe que a propagação resultou em uma redução da vazão efluente máxima de 2,557$$m^3$$/s (entrada) para 2,067$$m^3$$/s (saída). Isso é uma atenuação de 19,16%, obtida pela equação \ref{eq:eqcContinuidade4}. O retardo no tempo é de aproximadamente 9 minutos.

\begin{equation}
\label{eq:eqcContinuidade4}\tag{4}
\frac{\Delta Q}{Q_{af}} = \left (\frac{Q_{p,af} - Q_{p,ef}}{Q_{p,af}}  \right )\times 100
\end{equation}

Onde: \\
$$\frac{\Delta Q}{Q_{af}}$$: diferença de laminação;\\
$$Q_{p,af}$$: Vazão de pico afluente $$m^{3}$$/s;\\
$$Q_{p,ef}$$: Vazão de pico efluente $$m^{3}$$/s.

---

## **Fontes:** <a name="Fontes"></a>

BUTLER, S. **Engineering Hydrology**. [S.l.]: Prentice-Hall, 1957.

GRIBBIN, J. **Introdução à hidráulica, hidrologia e gestão de águas pluviais**. [S.l.]: CengageLearning, 2009. ISBN 9788522106356.

PULS, L. **Flood Regulation of the Tennessee River**. [S.l.]:  70th Congress, !st Session, U.S.Government Printing Office, 1928.

PULS, L. **Bureau of Reclamation Manual**. [S.l.]:  U.S. Department of the Interior, Denver,1947.

TUCCI, C. **Hidrologia: Ciência e Aplicação**. [S.l.]: Editora da Universidade, UFRGS, 2007.(Coleção ABRH de Recursos Hídricos). ISBN 9788570259240.
