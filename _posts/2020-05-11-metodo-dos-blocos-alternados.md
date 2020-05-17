---
layout: post
title:  "Método dos Blocos Alternados usando Python"
date:   2020-05-11 00:00:00
description: Pensando na automatização do processo, usei programação para facilitar a geração de gráficos e tabelas do método.
img: blocosAlternados.JPG # Add image post (optional)
mathjax: true
---

Segundo Tomaz (2010), o método dos blocos alternados é de simples aplicação, se comparado a outros métodos de determinação da chuva de projeto. O primeiro passo do método é calcular, as intensidades da chuva para cada período de tempo e tempo de retorno, cada duração gera um bloco, que pode determinar a altura da lâmina precipitada e o limite da duração crítica do evento (que é normalmente o tempo de concentração da área contribuinte). O segundo passo, que dá o nome ao método, reordena o hietograma de forma a posicionar o pico de forma centralizada. Cada bloco de chuva do hietograma é alternado no entorno do bloco do pico, à direita e à esquerda. É aconselhado que o \\(\Delta\\)t adotado seja menor que o tempo de concentração da  bacia que está sendo estudada. 

Para a vazão de projeto utilizei a equação da chuva de Fortaleza que foi desenvolvida na Universidade Federal do Ceará (UFC), em 2011, com base nos últimos trinta anos de registros pluviográficos contínuos, ou seja, de 1970 a 1999 para obter a intensidade de chuva (SILVA; JÚNIOR; CAMPOS, 2013). Deve-se considerar uma precipitação uniformemente distribuída.

Equação da chuva de Fortaleza:
\begin{equation}\tag{1}
\label{eq:idf-fortaleza}
i = \frac{2345,29.Tr^{0,173}}{(t+28,31)^{0,904}}
\end{equation}

Onde: \\
Tr: é o período de retorno da precipitação em anos;\\
i: é a intensidade média de chuva mm/h para uma duração em minutos;\\
t: é o tempo de duração da chuva em minutos.

O período de retorno (Tr), a duração da chuva (t) e a intensidade de chuva (i) estabelecem uma relação conhecida como curva IDF, representada por uma curva exponencial ou hiperbólica. É recomendado que cada cidade possua a sua, pois elas ajudam na determinação da vazão de projeto em obras. Na figura [1](#curvaIDF) a curva IDF de Fortaleza para vários Trs.
<a name="curvaIDF"></a>

![foto1]({{site.baseurl}}/assets/img/curvaIDF.JPG)
*Figura 1: Curva IDF de Fortaleza para vários Trs*

O tempo a ser utilizado deve ser maior ou igual ao tempo de concentração, pois ao ultrapassar o tempo de concentração mantendo-se a precipitação, a vazão continua constante mesmo que a duração da chuva seja maior. Porém, pode-se observar que a intensidade média da chuva e a duração são grandezas inversamente proporcionais, desse modo, a vazão diminui a partir do tempo de concentração. Para a curva da precipitação é o contrário, aumenta com o tempo. Na figura [2](#precipitacaoFortaleza) a curva de precipitação de Fortaleza para vários Trs.
<a name="precipitacaoFortaleza"></a>

![foto1]({{site.baseurl}}/assets/img/precipitacaoFortaleza.JPG)
*Figura 2: Precipitação de Fortaleza para vários Trs*

 Tempo de retorno é o tempo médio entre dois eventos que cause falha na obra, ou seja, a ocorrência de uma chuva ou vazão superior aquela pré-estabelecida. Para escolhê-lo devem-se fazer estudos de base econômica e financeira considerando custos e benefícios da obra, porém esses aspectos são muito limitados pois existem eventos que não podem ser medidos. Devem-se considerar também os custos de operação e manutenção da obra. Outro problema é que quanto maior o tempo de retorno, maior o porte da obra, consequentemente o seu custo, e portanto, maior a interferência no ambiente urbano causando transtornos para a população. 

Vamos ao exemplo (tabela [1](#blocosAlternados)), foi adotado o passo de 6 minutos, tempo de duração de 60 minutos e tempo de retorno de 50 anos.
<a name="blocosAlternados"></a>

 índice	|	tempo(min)	|	i(mm/h)	|	p(mm)	|	\\(\Delta\\)p(mm)	|	\\(\Delta\\)p/t(mm/h)	|	índice ordenado	|	i (mm/h)	
 :-----:|:-------------:|:---------:|:---------:|:---------:|:-----------:|:-----------:|:---------------:
	0	|     6.00		|   188.84	|   18.88	|   18.88	| 	188.84	   	|	8.00			|		37.11
	1	|    12.00		|   163.24	|   32.65	|   13.76	| 	137.64	   	|   6.00			|  		48.98
	2	|    18.00		|   144.00	|   43.20	|   10.55	| 	105.51	   	|   4.00			|		68.68
	3	|    24.00		|   128.98	|   51.59	|    8.39	|  	83.93	   	|   2.00			|		105.51
	4	|    30.00		|   116.92	|   58.46	|    6.87	|  	68.68	   	|   0.00			|		188.84
	5	|    36.00		|   107.01	|   64.21	|    5.75	|  	57.48	   	|   1.00			|		137.64
	6	|    42.00		|    98.72	|   69.11	|    4.90	|  	48.98	   	|   3.00			|		83.93
	7	|    48.00		|    91.68	|   73.34	|    4.24	|  	42.37	   	|   5.00			|		57.48
	8	|    54.00		|    85.61	|   77.05	|    3.71	|  	37.11	   	|   7.00			|		42.37
	9	|    60.00		|    80.34	|   80.34	|    3.29	|  	32.85	   	|   9.00			|		32.85

*Tabela 1: Blocos alternados*

As figuras [3](#Hietograma) correspondem aos gráficos da tabela.
<a name="Hietograma"></a>

![foto1]({{site.baseurl}}/assets/img/post4-img1.png)
![foto1]({{site.baseurl}}/assets/img/post4-img2.png)
*Figura 3: Hietograma*

Fiz um vídeo (figura abaixo) explicando detalhadamente o código em python que está disponível no [`GitHub`](https://github.com/gustavosiebra/blocos-alternados/blob/master/blocosAlternados.py). 

[![](http://img.youtube.com/vi/hDPak1y4P_k/0.jpg)](http://www.youtube.com/watch?v=hDPak1y4P_k "código do método")

---

## **Fonte**

SILVA, F. O. E. da; JÚNIOR, F. F. R. P.; CAMPOS, J. N. B. **Equação de chuvas para Fortaleza-CE com dados do pluviógrafo da UFC**. [S.l.]: Revista DAE. N 192, 2013.

TOMAZ,   P. **Curso   de   Manejo   de   águas   pluviais**.   2010.   Acessadoem 19-Novembro-2019. Disponível em:  <https://www.passeidireto.com/arquivo/66227801/apostila-prof-plinio-metodo-dos-blocos-alternados>.

