# Respostas para o questionário

## 1. Quais passos você tomaria para resolver este problema? Descreva de forma completa e clara todos os passos que você considera essenciais para a resolução do problema.

**Primeiro de tudo importei os dados. Apos isso, fiz uma analise exploratória dos dados, que esta em [analise_exploratoria_air_system.ipynb](analise_exploratoria_air_system.ipynb). Durante a análise, observei muitos valores nulos e diversas colunas com zeros. Identifiquei também um desbalanceamento de classes, com a classe negativa representando 98% dos dados e a classe positiva menos de 2%. Esse desbalanceamento poderia comprometer o desempenho dos modelos de machine learning. A análise exploratória ajudou a identificar padrões e anomalias nos dados. Verifiquei que várias colunas continham dados redundantes ou irrelevantes. Além disso, observei a necessidade de tratamento dos valores ausentes e padronização das variáveis. Esta etapa inicial foi fundamental para direcionar as próximas etapas do projeto, garantindo que os dados estivessem preparados para o processamento e análise subsequente.**

**Após essa etapa, procedi com o tratamento dos dados no notebook [tratamento_dados_air_system.ipynb](tratamento_dados_air_system.ipynb), removi as colunas que continham uma alta proporção de valores nulos e zeros simultaneamente, estabelecendo um limite de 40%. Em seguida, imputei os valores ausentes utilizando a mediana. Para lidar com o desbalanceamento de classes, utilizei o algoritmo RandomOverSampler(sampling_strategy=1). Posteriormente, normalizei os dados utilizando o método StandardScaler(). Utilizei os algoritmos VarianceThreshold(threshold=0.3), SmartCorrelatedSelection() e RFE() para reduzir a dimensionalidade dos dados, finalizando com 20 colunas selecionadas.**

**Na etapa de treinamento, no notebook [treinamento_modelos.ipynb](treinamento_modelos.ipynb), eu selecionei os seguintes modelos: Cat Boost, Random Forest e Redes Neurais Sequenciais. Para otimizar o desempenho dos modelos Cat Boost e Random Forest, eu utilizei o algoritimo BayesSearchCV, para a Redes Neurais Sequenciais eu utilizei o algoritimo keras_tuner.RandomSearch para otimizar os hiperparâmetros.**

**No notebook de [avaliacao_modelos.ipynb](avaliacao_modelos.ipynb), avaliei o desempenho dos modelos. Utilizando o recall como métrica de desempenho, constatei que o modelo de Redes Neurais Sequenciais obteve o melhor resultado nos dados de teste, alcançando um recall de 73%. O modelo Random Forest teve desempenho de 60%, enquanto o CatBoost alcançou 68%. Com base nos custos monetários de manutenção para cada possível resultado (TP com valor de 25, TN com valor de 0, FP com valor de 10 e FN com valor de 500), avaliei o desempenho dos modelos através do custo monetário de manutenção dos sistemas de ar condicionado para diferentes thresholds. O modelo que apresentou o menor custo monetário foi o Random Forest, com um custo de 21.805 unidades monetárias para um threshold de 5%. O modelo de Redes Neurais Sequenciais teve um custo de 26.735 unidades monetárias para o mesmo threshold, enquanto o CatBoost teve um custo de 46.010 unidades monetárias. Ao analisar a matriz de confusão com um threshold de 5%, o modelo Random Forest conseguiu acertar 357 de 373, o modelo Redes Neurais acertou 345 de 373, e o modelo CatBoost acertou 298 de 373.**

## 2. Qual métrica técnica de ciência de dados você utilizaria para resolver este desafio? Ex: erro absoluto, RMSE, etc.

**A métrica técnica que eu utilizaria para resolver esse desafio é o recall. Em um cenário onde os dados estão desbalanceados, o recall se destaca por capturar eficientemente a proporção de verdadeiros positivos que foram corretamente identificados pelo modelo. Isso é particularmente relevante quando o foco está na detecção correta dos caminhões com defeito, minimizando o risco de falsos negativos (defeitos não detectados).**


## 3. Qual métrica de negócio você utilizaria para resolver o desafio?

**Uma métrica de negócio relevante para resolver esse desafio seria o custo total de manutenção do sistema de ar de todos os caminhões. Essa métrica permite comparar diretamente o custo antes e depois da implementação do modelo de detecção de defeitos. A ideia é avaliar o impacto econômico real do modelo ao longo do tempo.**

## 4. Como as métricas técnicas se relacionam com as métricas de negócio?
**As métricas técnicas e as métricas de negócio são complementares e devem ser avaliadas em conjunto para garantir que um projeto de ciência de dados não apenas entregue modelos precisos, mas também gere valor tangível para a organização.**

## 5. Que tipos de análises você gostaria de realizar no banco de dados do cliente?
**O principal e mais importante problema é a alta incidência de valores nulos e muitos valores zeros nos dados. É crucial investigar as causas dessa abundância de dados descartáveis e identificar quais colunas não são necessárias.**

## 6. Quais técnicas você utilizaria para reduzir a dimensionalidade do problema?
**Primeiro usei o algoritimo VarianceThreshold para retirar colunas com nenhuma variação dos dados,apos isso, usei o algoritimo SmartCorrelatedSelection() com limite de 0.70, eliminando as colunas com alta correlação, e apos isso, usei o algoritimo RFE()(Eliminação Recursiva de Recursos) para selecionar as 20 colunas mais importantes para o modelo**

## 7. Quais técnicas você utilizaria para selecionar variáveis para seu modelo preditivo?
**Para identificar as variavieis mais importantes para o modelo([analise_exploratoria_air_system.ipynb](analise_exploratoria_air_system.ipynb) ), usei o algoritimo [SHAP](https://shap.readthedocs.io/en/latest/) (SHapley Additive exPlanations) que é uma abordagem de teoria de jogos para explicar a saída de qualquer modelo de aprendizado de máquina. Ela conecta alocação de crédito ótima com explicações locais usando os valores clássicos de Shapley da teoria dos jogos e suas extensões relacionadas. Segundo o algoritimo SHAP, as variáveis mais importantes são as colunas ck_000, bb_000, az_000 e ee_005**

## 8. Quais modelos preditivos você utilizaria ou testaria para este problema? Indique pelo menos 3.
**Primeiramente, utilizei seis algoritmos para o treinamento: LogisticRegression(), RandomForestClassifier(), GradientBoostingClassifier(), SVC(), CatBoostClassifier(), e keras.Sequential(). Após avaliar o desempenho de cada modelo com hiperparâmetros padrão, escolhi RandomForestClassifier() e CatBoostClassifier() devido ao seu melhor desempenho. Como ambos são baseados em árvores de decisão, também selecionei keras.Sequential() (Redes Neurais Sequenciais) para incluir um modelo com uma abordagem diferente. Esses três modelos serão passados para o algoritmo de otimização de hiperparâmetros.**

## 9. Como você avaliaria qual dos modelos treinados é o melhor?
**Para avaliar qual dos modelos treinados é o melhor, utilizarei a métrica de Recall, para considerar o desbalanceamento das classes. Além disso, analisarei a matriz de confusão para cada modelo, verificando a taxa de verdadeiros positivos. Também calcularei o custo total de manutenção, baseado nos falsos positivos e falsos negativos. O modelo com maior Recall e menor custo total será considerado o melhor. Compararei esses resultados nos dados de teste para assegurar a generalização.**

## 10. Como você explicaria o resultado do seu modelo? É possível saber quais variáveis são mais importantes?
**Primeiro, o algoritmo RFE é um método recursivo de eliminação de features, começando com todos os recursos disponíveis e iterativamente removendo os menos importantes até atingir o número desejado de recursos. Segundo o algoritmo RFE, as 20 variáveis mais importantes são: 'ag_006', 'ay_008', 'az_000', 'az_002', 'az_003', 'az_005', 'bb_000', 'be_000', 'bk_000', 'cb_000', 'ck_000', 'cn_007', 'cs_001', 'cs_004', 'cs_006', 'dd_000', 'ds_000', 'ee_005', 'ee_006', 'ee_007'. Após isso, utilizo o algoritmo SHAP para identificar a importância de cada variável, sendo as variáveis mais importantes: 'ck_000', 'bb_000', 'az_000' e 'ee_005'.**

## 11. Como você avaliaria o impacto financeiro do modelo proposto?
**Utilizei os valores de custo monetário para cada possível resposta: TP com valor de 25, TN com valor de 0, FP com valor de 10 e FN com valor de 500. Com esses valores, calculei o custo total de manutenção para cada algoritmo. O algoritmo de Redes Neurais, com um limite de 50%, apresentou o custo total de 61.295. Em contrapartida, o algoritmo de Random Forest, com um limite de 5%, teve o menor custo total, alcançando 21.805**

## 12. Quais técnicas você utilizaria para realizar a otimização de hiperparâmetros do modelo escolhido?
**Para otimizar os hiperparâmetros dos modelos Cat Boost e Random Forest, utilizei o algoritmo BayesSearchCV.Essa abordagem usa Otimização Bayesiana passo a passo para explorar os hiperparâmetros mais promissores no espaço do problema. Para a Redes Neurais Sequenciais, utilizei o algoritmo keras_tuner.RandomSearch,ele vem com algoritmos de Otimização Bayesiana, Hiperbanda e Pesquisa Aleatória integrados e também foi projetado para ser fácil para pesquisadores estenderem a fim de experimentar novos algoritmos de pesquisa.**

## 13. Quais riscos ou precauções você apresentaria ao cliente antes de colocar este modelo em produção?
**Antes de implementar o modelo em produção, é crucial garantir que os resultados sejam interpretados corretamente para evitar decisões equivocadas. Além disso, o modelo deve ser capaz de lidar eficientemente com novos dados em tempo real e requerer monitoramento contínuo para ajustes conforme necessário. Um desafio significativo é a manutenção da eficácia preditiva do modelo diante da evolução dos dados ao longo do tempo, o que pode afetar sua capacidade de generalização e precisão nas previsões**

## 14. Se seu modelo preditivo for aprovado, como você o colocaria em produção?
**Implementar um modelo preditivo de forma eficaz pode envolver o uso de práticas de MLOps. Inicialmente, é essencial utilizar ferramentas de versionamento como o GitHub para registrar e gerenciar as versões do modelo, garantindo um histórico claro e o controle de mudanças ao longo do tempo. Além disso, adotar CI/CD (Integração Contínua e Entrega Contínua) é fundamental para automatizar o processo de integração e implementação, permitindo que novas versões sejam testadas e implantadas de forma eficiente e confiável. Essas práticas garantem uma implementação robusta e escalável do modelo, mantendo-o atualizado e alinhado com as necessidades do ambiente de produção. Além disso, a implementação em lote ou delivery vai depender das necessidades específicas do cliente, os requisitos de atualização e a frequência de aplicação do modelo preditivo.**

## 15. Se o modelo estiver em produção, como você o monitoraria?

**Monitorar um modelo em produção apresenta desafios significativos, principalmente devido ao delay entre previsões e respostas reais. Além de métricas técnicas como precisão e recall, é essencial implementar validações independentes e análises de confiança para verificar a qualidade das previsões em tempo real. Implementar alertas para detectar mudanças abruptas nos padrões de entrada também é crucial para identificar desvios no desempenho do modelo.**

## 16. Se o modelo estiver em produção, como você saberia quando re-treiná-lo?

**Para monitorar um modelo em produção de forma eficaz, podemos adotar duas abordagens principais. Primeiro, o retreinamento periódico, pode ser realizado com base na disponibilidade de novos dados, seja diariamente, semanalmente, ou mensalmente, conforme a necessidade e a capacidade de processamento. Além disso, é crucial monitorar regularmente os parâmetros de treinamento, como média e desvio padrão, e compará-los com os novos dados de entrada. Quando esses parâmetros divergem significativamente, isso pode sinalizar a necessidade de retreinamento do modelo para manter sua precisão e relevância**




