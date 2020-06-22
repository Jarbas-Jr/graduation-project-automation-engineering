<p align="center">
  <img src="jarbasjr.jpeg" >
</p>

# Jarbas Carriconde
<sub>*Projeto de Graduação em Engenharia de Automação pela Univerisdade Federal do Rio Grande - FURG*</sub>

**[LinkedIn](https://www.linkedin.com/in/jarbas-carriconde-4877b9151/)**

# 1. Contextualização

O presente trabalho procura abordar o desenvolvimento de algoritmos que se apropriam de inteligência artificial para identificar tendências de mercado em ações e  auxiliar o investidor que mira retornos no longo prazo, finalidade esta pouco abordada em trabalhos acadêmicos que envolvam tecnologia para predições no mercado financeiro.

O trabalho visava  buscar ações que retornem 10% ou mais em um período de no mínimo um ano. Ainda que investidores não fossem capazes de predizer a porcentagem do crescimento do preço de uma determinada ação ao longo do tempo, tal informação é vital para investidores que buscam rendimentos no longo prazo. Relação esta que foge dos tradicionais HFT's que são negociações que acontecem em alta velocidade, em questão de segundos onde investidores buscam pequenos retornos encontrando pequenas disparidades de preços. Ou até mesmo dos chamados day trade e swing trade, onde o primeiro são negociações realizadas concretizadas em um mesmo dia e o segundo são negociações que levam entre um e alguns dias entre as realizações de compra e venda.

Há uma série de vantagens para investidores que optam por buscar retornos no longo 
prazo, logo se torna uma nuance com muito espaço para ser explorado. Como principais beneficio tem-se a redução com custos transacionais como corretagens(valor pago para emitir ordem de compra/venda de uma ação), os impostos sobre os ganhos são proporcionalmente menores, há uma melhor capacidade de adaptar o portfólio de ativos de acordo com as mudanças econômicas sem sofrer com questões tributárias, é capaz de tolerar as volatilidades de curto prazo obtendo maiores lucros no longo prazo além de capitalizar a volatilidade inerente que se relaciona com o risco, ou seja, quanto maior o risco maior os possíveis retornos.

A lógica se dará por criar uma atributo que compara o preço atual da ação em relação ao preço de exatamente um ano antes, assim obtendo uma classificação da ação como ‘Boa’ ou ‘Ruim’, e é essa variável classificatória que deverá ser predita por algoritmos de aprendizado de máquina para averiguar se uma ação é classificada como ‘Boa’, que segundo o algoritmo significaria que é tida como uma ação recomendada para se investir e com potencial de valorização no próximo ano corrente. 

A outra parte da metodologia teve seu embasamento que mostra a aplicação de redes neurais recorrentes do tipo LSTM na previsão de tendências de preços de ações com base em preços históricos.

Portanto, o presente trabalho busca pegar uma parte da metodologia que constrói um dataset com dados de preço e dados contábeis das empresas, e aplica algoritmos de classificação para inferir um target como ‘Bom’ caso a ação se valorize em 10% ou mais no período de um ano, e ‘Ruim’ caso o contrário. Com isso, juntamente incorporar aplicação de algoritmos mais sofisticados, bem como utilizar  técnicas de ajustes de hiperparâmetros e métodos para avaliar a capacidade de generalização dos modelos, além de um robusto pré-processamento dos dados. A outra parte da metodologia trazida em parte de nelson2017uso busca a aplicação de uma LSTM sobre séries temporais de ações com base em dados de preços anteriores no intuito de buscar a visualização gráfica de tendências do preço. 

Ao final, une-se os algoritmos de aprendizado de máquina que buscam a classificação binária que indica se uma ação irá se valorizar em 10% ou não no próximo ano, e aliado a isso busca-se uma inferência por parte da LSTM para através de aplicação sobre séries temporais visualizar a tendência, e assim utilizando os dois segmentos busca-se o auxílio para tomada de decisão em investimentos de longo prazo mirando uma convergência entre os algoritmos de classificação e a tendência apontada pelo gráfico oritundo da LSTM. Sendo feitos, ao final, análises e considerações no que tange o desempenho auferido com base nos recursos e metodologias utilizados no presente trabalho.


# 2. Sequência de Etapas

- Escolher ações dentre as que compõe o índice Ibovespa.

- Fazer download dos dados contábeis das ações.

- Descartar ações com muitos dados contábeis faltantes.

- Pré-processar dados contábeis de cada ação.

- Extrair dados de preço das ações.

- Concatenar dados de preço e contábil de cada ação. Criar \textit{target} que diz se a ação se valorizorá 10\% ou não no próximo 1 ano.

- Concatenar todos os dados das ações em dataset único.

- Tratar dados e normalizar os dados.

- Aplicação de 6 algoritmos de aprendizado de máquina classificatórios.

- Escolher 5 ações dentre as selecionadas.

- Extrair séries temporais de preço de cada uma das 5 ações.

- Aplicar RNN do tipo LSTM em cada uma das 5 ações.

- Validar todos os algoritmos aplicados no trabalho com dados de teste.

- Executar processo de inferência, através  da tendência do gráfico apontado pelos dados preditos pela LSTM em conjunto com o os \textit{targets} mostrados pelos modelos dos algoritmos de classificação. Utilizando dados futuros para uma tentativa real de predição, sem possibilidade de utilização de dados de teste.

- Concluir e avaliar o desempenho dos resultados obtidos na fase de teste e, principalmente, nas inferências,   considerando recursos possíveis e metodologia utilizados.


# 3. Fluxograma das Etapas

<p align="center">
  <img src="fluxograma.jpg" >
</p>

# 4. Etapas

Aqui irei descrever cada etapa e colocar os respectivos links para as pastas e notebooks correspondentes, que estarão com seus códigos devidamente explicados.

## 4.1 Escolha das Ações

Como critério de seleção de ações para compor o dados do dataset principal do presente trabalho, foi definido que seria de maior relevância a utilização de ações que compõem o principal índice de ações no mercado de capitais brasileiro, o índice Ibovespa. Com base na carteira téorica do dia 22/10/2019, as 69 ações que compunham o índice conforme o site da [BMF&Bovespa](http://www.bmfbovespa.com.br/pt_br/produtos/indices/indices-amplos/indice-ibovespa-ibovespa-composicao-da-carteira.htm).

Após a definição do critério para escolha das ações, necessitava-se averiguar a disponibilidade dos dados contábeis que iriam compor o dataset final, e como fonte aberta e gratuita de dados contábeis, foi utilizado o site da [Fundamentus](https://www.fundamentus.com.br/), onde basta realizar uma pesquisa na página inicial através do código da ação ou nome da empresa que estarão disponíveis umas série de dados contábeis a respeito da maioria das empresas de capital aberto na BMF\&Bovespa em formato excel.

Os dados contábeis estão dispostos em uma escala temporal trimestral que é o período em que os balanços das empresas são divulgados, e observou-se um padrão em que a maioria das empresas possui dados de até 10 anos antes do último balanço divulgado. No momento em que o presente trabalho estava sendo desenvolvido o padrão era de dados do segundo trimestre de 2019 até o segundo trimestre de 2009, portanto definiu-se como critérios para selecionar a ação para ter seus dados junto ao dataset, no mínimo dados com maior robustez e com um histórico disponível de no mínimo 5 anos antes, ou seja, no mínimo até o segundo trimestre de 2014. Além de que, dados contábeis de ações onde bancos eram as empresas emissoras foram descartadas por estarem dispostas em um padrão diferente em relação a todas as empresas restantes. 

Após análise do conjunto de dados de balanço de cada uma das 69 ações que compunham o índice Ibovespa, foram descartadas todas as ações de empresas bancárias e ações nas quais seu arquivo excel apresentava pouco histórico de trimestres ou muitos dados faltantes, assim restaram 39 ações onde cada um dos arquivos de balanço contábil deve passar por um pré-processamento para ser concatenado em formato CSV com dados de preço.

<p align="center">
  <img src="fundamentus.jpg" >
</p>

Os dados de preço são extraídos da API Yahoo Finance, onde através de código em python são definidas as delimitações das datas de início e fim dos dados a serem extraídos, além da escala temporal que os dados estarão colocados. No presente trabalho foi definida a extração dos dados na escala mensal de forma que a delimitação das datas estivessem criteriosamente de acordo com a delimitação temporal dos dados contábeis, procedimento este sendo feito individualmente para cada uma das 39 ações, uma vez que nem todos os dados contábeis atendiam ao padrão da maioria que dispunham de dados contábeis de até 10 anos antes do último balanço divulgado.

<p align="center">
  <img src="yahoo_finance.png" >
</p>

### 4.1.1 Pastas com notebooks das 39 Ações

Aqui temos uma pasta para cada uma das ações selecionadas, conforme critério estabelecido anteriormente. Onde em cada pasta temos todos os códigos em notebook devidamente comentado e explicado, bem como o csv de dados fundamentalistas de cada respectiva empresa. E além disso, o csv resultande.

Lembrando que cada código trata os dados fundamentalistas, de preço, bem como a criação do target. Tudo devidamente explicado.

SEGUEM OS LINKS, COM AS PASTAS REFERENTES A PRIMEIRA PARTE DO PROCESSAMENTO. FOI SUBDIVIDIDO EM 3 PASTAS POR QUESTÃO DE ESPAÇO. ORDENADAS POR ORDEM ALFABÉTICA. BASTA CLICAR NA PASTA, CLICAR NA AÇÃO E DEPOIS NO NOTEBOOK PARA VER TODO O CODE EXPLICADO.

 * **Parte 1. AÇÕES ÍNDICE BOVESPA(A-C):** https://bit.ly/30WTTDQ
 * **Parte 2. AÇÕES ÍNDICE BOVESPA(D-P):** https://bit.ly/30Yp6qd
 * **Parte 3. AÇÕES ÍNDICE BOVESPA(Q-Z):** https://bit.ly/2YXlylt

## 4.2 Concatenação das 39 ações em dataset único

Pegando o resultante de cada dataset das 39 ações, que uniram dados de preço, dados fundamentalistas e o target, chegou a hora de juntar tudo isso em um dataset no qual serão aplicados os algoritmos de classificação.

Primeiro temos o link da pasta que contém dois notebook, um para concatenar os 39 datasetes e outro que faz os processamentos, limpeza de dados e preenchimento de dados faltantes.

Seguem o link da pasta, e os netebooks que há dentro dela, devidamente comentados.

 * **Parte 4.  CONCATENANDO TODAS AS AÇÕES - DATASET FINAL:** https://bit.ly/2YjNwsr
    * **1. DATASET FINAL DOS FINAIS - VERSÃO FINAL.ipynb:** https://bit.ly/2YYpy50
    * **2. CLEANING COLUMNS - KNN - VERSÃO FINAL.ipynb:** https://bit.ly/3hNfbcX


## 4.3 Aplicação de 6 algoritmos de classificação.

Agora temos a modelagem de 6 algortimos de complexidades e metodologias distintas sobre o dataset constituído. Dedicamos um dataset para cada devidamente comentado. Aplicação de algortimo de Rede Neural está numa pasta a parte.

Em cada notebook temos:
* Aplicação do algortimo
* Normalização dos Dados
* Grid Search e Cross Validation
* Timer do tempo da modelagem
* Classification Report com as métricas de validação
* Armazenamento em arquivo picke para usar os modelos no processo de inferência junto com o LSTM ao final da metodologia

Na pasta referente as Redes Neurais naõ temos o grid search e o cross validation, mas temos a peculiaridade de ter uma pasta que traz as classificação dos rótulos para valores númericos.

Seguem os links:

* **PARTE 5. MODELOS DE CLASSIFICAÇÃO**: https://bit.ly/310oz71
  * **1. Árvore de Decisão**: https://bit.ly/2NftJ7l
  * **2. Floresta Aleatória**: https://bit.ly/37PwTry
  * **3. Regressão Logística**: https://bit.ly/318a0yB
  * **4. SVM**: https://bit.ly/3ekBtAT
  * **5. XGBoost**: https://bit.ly/3hKKYeB

* **6. Redes Neurais**: https://bit.ly/3fE6j7u
  * **1. Passando os target para número para aplicar na RNA**: https://bit.ly/3fJTVTM
  * **2. Redes Neurais Artificiais - Classificação Bínaria**: https://bit.ly/2YXcwVk

## 4.4 Inferênca dos Algortimos de Classificação e aplicação de Redes Neurais Recorrentes

Aqui temos a etapa final dos códigos.

Escolhi 5 ações para fazer um processo de inferência: CYRE3, GOAU4, LAME4, PETR4 e VALE3.

Logo dentro dessa pasta que representa a PARTE 6, que é a última, temos duas subpastas, uma que mostra as inferências feitas pelos modelos de classificação que foram treinados, e outra que mostra todo o processo de aplicação de LSTM para validação e predição.

* **PARTE 6. INFERÊNCIA DOS MODELOS DE CLASSIFICAÇÃO E APLICAÇÃO DE LSTM** : https://bit.ly/2NoeKrr

* **INFERIR 5 AÇÕES COM OS MODELOS DE CLASSIFICAÇÃO**: https://bit.ly/312Z4C9
  * Aqui temos 5 pastas, uma referente a cada uma das 5 ações escolhidas, e dentro temos dois notebooks. Um notebook que usa a mesma metodologia de processamento que une os dados de preço, dados fundamentalistas e o target para gerar uma única amostra que será usado no processo de inferência pelos classificadores. Então entra o segundo notebook, com a amostra gerada pelo processamento, imputo as entradas em todos os modelos classificadores que foram treinados e eles inferem o target: "Good" ou "Bad". Todos os notebooks estão comentados
  
* **INFERIR 5 AÇÕES COM LSTM - ALGORITMO SÉRIE TEMPORAL**: https://bit.ly/313i5Ep
  * Aqui também temos 5 pastas, tal qual a outra dessa parte, teremos dentro uma pasta referente a cada uma das 5 ações escohidas. Dentro de cada temos dois notebooks: um notebook comentado sobre o processo de aplicação de uma LSTM no qual a perspectiva é de "validação", onde temos os dados reais e comparamos com o que a série temporal da LSTM inferiu. A outra e sobre a perpestiva de predição mesmo, não temos os dados reais para avaliar, e queremos usar essa predição para unir com os targets inferidos pelos modelos de classificação e conseguir chegar em alguma conclusão sobre se a ação se valorizará em 10% ou não no próximo 1 ano.
  
  ## 5. RESULTADOS
  
Aqui coloquei a imagem da predição da LSTM e uma tabela com as classificações apontadas por cada um dos 6 modelos. Poderá ser conferido nos notebooks o processo e as imagens dos gráficos de validação da LSTM que mostra graficamente uma comparação entre o que foi predito e os dados reais.

* RESULTADOS DAS INFERÊNCIAS https://bit.ly/3hQyGRS


## 6. CONCLUSÕES E DISCUSSÕES

Este trabalho teve como objetivo, ainda que embrionário, desenvolver uma metodologia que utiliza duas bases técnicas principais para construção de um método envolvendo aprendizado de máquina para antever o movimento de preços futuros no mercado de ações visando o longo prazo. Além de utilizar dados de mercado de baixa frequência, que são pouco abordados na academia, outro aspecto também pouco abordado se dá no que tange a utilização de métodos classificatórios de aprendizado de máquina em conjunto com um método de LSTM aplicado em séries temporais, visando uma convergência entre as técnicas para uma tomada de decisão.

Considerando a relação custo benefício, o algoritmo de Florestas Aleatórias obteve a melhor performance com larga distância em relação aos demais, dentro da validação com dados de teste, umas vez que foi definida a melhor maneira de se avaliar a performance do algoritmo de forma generalista através de seu desempenho frente a 10 folds, com a métrica definida como accuracy. Através do best score com 10 folds obteve o melhor desempenho com 84,4% despendendo um tempo de processamento para encontro de melhores hiperparâmetros de 18min 25s, além de que as métricas de precision, recall e f1-score obtiveram um desempenho que não é discrepante, próximo ao desempenho generalista apontado por best score com diferença máxima de 3%. Vale ressaltar que o XGBoost obteve um bom desempenho de 83,06% apontado por best score para 10 folds, no entanto a um custo computacional de 1h 15min 46s para encontrar os melhores hiperparâmetros. Os algoritmos de Árvore Decisão, Regressão Logística e SVM obtiveram uma performance substancialmente menor que o de Florestas Aleatórias, não justificando qualquer economia de custo computacional para o ajuste de seus hiperparâmetros. Vale ressaltar, por fim, que o Perceptron Multicamadas obteve uma performance abaixo da crítica diante da complexidade do algoritmo, apresentando um desempenho apontado por best score de 70,25% com tempo de processamento  para encontrar os melhores hiperparâmetros de 26h 46min 23s demonstrando um grande custo computacional que não é justificada em performance, provavelmente pois o conjunto de dados utilizado têm uma baixa amostragem que não permite o treino efetivo da rede neural para um bom desempenho que se espera de um método mais avançado como este. 

Nas redes neurais recorrentes do tipo LSTM, no processo de validação, utilizou-se a diferença média entre os valores preditos e os preços reais, obtendo um erro médio que varia entre 0.5244 e 4.3876, com excessão de LAME4 que apontou uma discrepância de 23.2797, no entanto em todos os casos foi possível identificar uma tendência dos valores preditos em acordo com os preços reais, que era o real objetivo, e na maioria das vezes acompanhando as distorções e movimentos no decorrer da evolução do preço, mesmo que com algum delay.

Ao final, unindo os algoritmos classificatórias com as LSTM’s aplicadas em séries temporais, objetivava-se uma convergência dos métodos que possibilitasse uma tomada de decisão ao averiguar se era possível identificar uma tendência, e justamente por se caracterizar por um processo de inferência, foi escolhido um período que ainda não havia se concretizado, impossibilitando uma validação com dados de teste, assim o período exposto foi do final do segundo trimestre de 2019 até o segundo trimestre de 2020. Portanto, realizando um processo mais tangível a realidade para realçar a usabilidade da metodologia e analisar os resultados diante dos recursos disponíveis para desenvolvimento do presente trabalho, enquanto que MILOSEVIC(2016) e NELSON(2017), principais trabalhos influentes para construção da metodologia deste trabalho, realizaram apenas validação com base de dados de teste, sem processo de inferência, sendo que, o processo de inferência neste trabalho suscita o debate sobre o distanciamento do que é feito na academia e o real uso prático no mercado financeiro.  

Analisando o processo de inferência para cada uma das 5 ações escolhidas para tal, não foi possível identificar um padrão entre as 5 ações, ou na maioria delas, que permitisse a consistência de um auxílio para identificação se a ação se valorizaria 10% ou mais em 52 semanas(1 ano). Assim foi constituído o gráfico oriundo da LSTM e a resposta dos 6 algoritmos ao receber na entrada do modelo um registro com preços e dados fundamentalistas referentes ao segundo trimestre de 2019, assim esperava-se que a maioria dos algoritmos apontasse uma tendência que convergisse com a tendência apontada pelo gráfico dos preços preditos da LSTM. Nas ações GOAU4, LAME4 e VALE3 foi possível observar uma convergência dos algoritmos classificatórios com o gráfico apontado pela LSTM, no entanto, essas ações apontam tendência de queda, enquanto que CYRE3 e PETR4 que o gráfico LSTM aponta tendência de alta, os algoritmos classificatórios não convergiram em sua maioria conforme representação do gráfico, assim apontando uma inconsistência no processo de inferência a ser debatido na seção a seguir.

### 6.1. PRINCIPAIS DISCUSSÕES


Talvez o principal aspecto a ser ressaltado, é que os dados utilizados foram oriundos de plataformas gratuitas:Fundamentus e API Yahoo Finance, portanto, além de serem dados que não são robustos e confiáveis, ajudam no erro amostral, onde quanto menor a quantidade de amostras, maior dificuldade de se tirar conclusões dos modelos algorítmicos, não importando a complexidade. Conforme já citado, quanto maior a base de dados, mais experiência pode ser computada, o que afeta frontalmente o desempenho. E lembrando também que em MILOSEVIC(2016) utilizou-se o terminal pago da Bloomberg, além de que na iniciativa privada grandes grupos de investimentos despendem alto capital em dados de qualidade por meio de acesso pago e também em estudiosos da área que permanecem anos desenvolvendo métodos para obterem estratégias rentáveis. 

Devido ao custo computacional, a limitação imposta pelas plataformas pouco robustas, e o viés de longo prazo do presente trabalho, não foi possível a utilização de dados em menor escala, e conforme RECHENTIN(2014) salienta, a maioria dos estudos justamente pretere, em grande parte, o desenvolvimento de estratégias de longo prazo em detrimento aos de curto, justamente pelo fato de que têm-se uma maior facilidade em obter mais dados em escalas temporais menores, e também pela natureza do processo de curto prazo que caracteriza-se por desenvolver um processo de tentativa e erro muito mais rápido, abastecendo os estudos sobre esse tipo de método em um fluxo muito mais veloz.

Além do conhecimento técnico a respeito de processamento e manipulação de dados, algoritmos de aprendizado de máquina e tantos outros conhecimentos necessários, também é essencial um conhecimento a respeito das especificidades do assunto em que as tecnologias são aplicadas, como no caso, o mercado de ações. Assim, é sabido que o mercado de ações trabalha muito com expectativas a cerca dos acontecimentos que estão por vir, ou seja, os agentes vão precificando o ativo de acordo com as expectativas futuras, o que nos permite levantar uma discussão sobre o impacto de parâmetros contábeis, uma vez que os agentes do mercado já criam uma expectativa e precificam o ativo em consequência do balanço que está por ser divulgado, colocando em questionamento o quanto esse tipo de dado seria válido para uma abordagem com técnicas de aprendizado de máquina, o que poderia gerar no futuro uma maior análise maior sobre o real poder preditivo dos parâmetros contábeis sobre o que se deseja predizer.

Por fim, os assuntos trazidos nessa seção levantam as discussões sobre os motivos que acarretaram no fato do processo de inferência não ter sido mais efetivo, diante da complexidade de cada uma das argumentações apresentadas: desde problemas com dados confiáveis, erro amostral, custo computacional, e até sobre as especificidades do mercado quanto às expectativas que os agentes colocam conforme os acontecimento inerentes a precificação de ativos. Logo, o trabalho torna-se enriquecedor, também, por suscitar estas discussões.

### 6.2. CONTRIBUIÇÕES REALIZADAS

O presente trabalho contribuiu com a criação de uma metodologia que até o presente momento, o autor não identificou igual, utilizando duas bases técnicas que envolvem algoritmos classificatórios e um algoritmo aplicado em séries temporais para identificar tendências de ações no longo prazo, que também é um assunto pouco abordado na academia. Assim deseja-se que tal metodologia contribua para insights futuros nos temas citados e que há uma grande margem para exploração, tendo em vista o grande aumento no acesso a dados de qualidade e nas tecnologias com capacidade cada vez maior de processamento. Além de que, o autor do presente trabalho compreende que a tecnologia deve também ter ênfase em auxiliar o investidor que mira longo prazo, sendo um vasto campo para análise e pesquisa.

A metodologia quanto ao processamento e manipulação dos dados se demonstrou complexa e dispendiosa justamente pelo má qualidade dos dados acessados, o que facilitaria a transmissão da ideia aventada para quem buscar acesso a dados melhores no desenvolvimento de abordagens semelhantes. 

Foi de grande contribuição também, a comparação dos algoritmos classificatórios de diferentes complexidades, que demonstraram que nem sempre o algoritmo mais complexo terá o melhor desempenho e que o custo computacional sempre deverá ser analisado relativo a métrica de desempenho. Quanto ao algoritmo LSTM, ressalta-se que, em sua validação, consegue replicar a tendência e movimento dos preços reais com desempenho interessante. 

### 6.3 SUGESTÕES SOBRE POSSIVEIS TRABALHOS FUTUROS

Para trabalhos futuros, sugere-se, primordialmente, acesso a uma base de dados privada com qualidade confiável e também, se possível, utilização do dispositivo com maior capacidade de processamento possível, para então, obter uma base de dados muito mais sólida na execução da metodologia, além de que, com recursos mais sofisticados pode-se especular mais valores para ajustes de algoritmos complexos.


Uma sugestão relevante para trabalho futuros pode ser a utilização de um ensemble learning onde pega-se os algoritmos classificatórios utilizados em que um conjunto de algoritmos, tal qual os 6 usados no presente trabalho, atua como um único algoritmo onde cada algoritmo que compõem o método de aprendizado em conjunto é ponderado pelo erro.

Outro método importante a ser incorporado, é uma engenharia de parâmetros (feature engineering) mais complexa, avaliando o real poder preditivo de cada parâmetro, principalmente os parâmetros relativos a dados contábeis e, eventualmente, gerando novos parâmetros sintéticos para avaliar o desempenho frente ao que se almeja encontrar, obtendo como finalidade a máxima extração de desempenho do conjunto de dados que será mais robusto e confiável sendo oriundo de uma base de dados privada.  No que tange aos dados de séries temporais, poderia ser utilizado algum método de suavização da série para minimizar ruídos, como um média móvel exponencialmente ponderada, ou outras técnicas mais sofisticadas.

Assim, para trabalhos futuros e uma melhoria essencial torna-se essencial utilização de recursos mais sofitisticados no que se refere ao acesso a dados de qualidade e também na melhoria dos conjuntos de dados com a finalidade de torná-lo mais eficiente possível, sem se distanciar de discussões e aplicações que mostrem conclusões sobre a real possibilidade de utilização real do que fora desenvolvido. 
