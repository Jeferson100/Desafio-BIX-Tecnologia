# Desafio-BIX-Tecnologia
Este repositório faz parte do processo seletivo para a vaga na empresa Bix Tecnologia. O detalhes do desáfio estão em [descricao_desafio.md](descricao_desafio.md) e as respostas para o desafio estão detalhadas em [respostas.md](respostas.md). 

Os dados estao na pasta [dados](dados) e são dois arquivos CSV:

-[air_system_previous_years.csv](air_system_previous_years.csv) arquivo contendo todas as informações do setor de manutenção para os anos anteriores a 2022, com 178 colunas e 60000 linhas.

-[air_system_present_year.csv](air_system_present_year.csv) arquivo contendo todas as informações do setor de manutenção neste ano contendo 178 colunas e 16000 linhas.

O repositório contém quatro notebooks, cada um abordando uma etapa específica do projeto:

1. [Análise Exploratória](analise_exploratoria_air_system.ipynb)
2. [Tratamento de Dados](tratamento_dados_air_system.ipynb)
3. [Treinamento de Modelos](treinamento_modelos.ipynb)
4. [Avaliação de Modelos](avaliacao_modelos.ipynb)

## Analise Exploratória

No notebook [Análise Exploratória](analise_exploratoria_air_system.ipynb), importei e examinei os dados. Durante a análise, identifiquei:

- Muitos valores nulos e colunas com zeros.
- Desbalanceamento de classes, com a classe negativa representando 98% dos dados e a classe positiva menos de 2%.
- Padrões e anomalias nos dados.
- Colunas redundantes ou irrelevantes.
- Necessidade de tratamento dos valores ausentes e padronização das variáveis.

Utilizando a biblioteca [Shapley Additive exPlanations(SHAP)](https://shap.readthedocs.io/en/latest/), identifiquei as variáveis mais importantes para o modelo com as variáveis `ck_000`, `bb_000`, `az_000` e `ee_005`sendo as mais importantes.

![Analise Exploratória](imagens/shap_principais_variaveis.png)

Esta etapa inicial foi crucial para orientar as próximas etapas, garantindo a preparação adequada dos dados.

## Tratamento de Dados

No notebook [Tratamento de Dados](tratamento_dados_air_system.ipynb), realizei o seguinte:

- Removi colunas com alta proporção de valores nulos e zeros (acima de 40%).
- Imputei valores ausentes utilizando a mediana.
- Utilizei o algoritmo `RandomOverSampler(sampling_strategy=1)` para lidar com o desbalanceamento de classes.
- Normalizei os dados com `StandardScaler()`.
- Reduzi a dimensionalidade utilizando `VarianceThreshold(threshold=0.3)`, `SmartCorrelatedSelection()` e `RFE()`, resultando em 20 colunas selecionadas.

## Treinamento de Modelos

No notebook [Treinamento de Modelos](treinamento_modelos.ipynb), selecionei e treinei os seguintes modelos:

- **Regressao Logisticas**
- **Gradiente Boost**
- **Redes Neurais Sequenciais**

Para otimização dos modelos:

- Utilizei `BayesSearchCV` para Gradiente Boost e Regressao Logisticas.
- Utilizei `keras_tuner.RandomSearch` para otimizar os hiperparâmetros das Redes Neurais Sequenciais.

## Avaliação de Modelos

No notebook [Avaliação de Modelos](avaliacao_modelos.ipynb), avaliei o desempenho dos modelos utilizando a métrica de recall:

- **Redes Neurais Sequenciais**: Recall de 58%
- **Gradiente Boost**: Recall de 75%
- **Regressão Logística**: Recall de 91%

### Análise de Custo Monetário

O desafio nos indicou os custos a seguir:
- Se um caminhão for enviado para manutenção, mas não apresentar defeito nesse sistema, cerca de $10 serão cobrados pelo tempo gasto durante a inspeção pela equipe especializada.
- Se um caminhão for enviado para manutenção e apresentar defeito nesse sistema, $25 serão cobrados para realizar o serviço de reparo preventivo.
- Se um caminhão com defeito no sistema de ar não for enviado diretamente para manutenção, a empresa paga $500 para realizar a manutenção corretiva, considerando a mão de obra, substituição de peças e outros possíveis inconvenientes (por exemplo, o caminhão quebrar no meio do trajeto).


Avaliei o desempenho dos modelos com base nos custos monetários de manutenção para diferentes thresholds:

![Custo Threshold](imagens/custo_threshold.png)


- **Regressão Logística**: Menor custo monetário de 13.700  para um threshold de 21%.
- **Redes Neurais Sequenciais**: Custo de 30.215 para o mesmo threshold.
- **Gradiente Boost**: Custo de 18.810.

### Matriz de Confusão (Threshold de 21%)

- **Regressão Logística**: Acertos de 180 de 187.
- **Redes Neurais Sequenciais**: Acertos de 121 de 187.
- **Gradiente Boost**: Acertos de 150 de 187.

## Análise de Calibração

**Ao analisar o gráfico de calibração, observei que nenhum modelo conseguiu ter um bom nivel de calibração. Para tentar corigir esses modelos, utilizei o metodo de Calibração VennABERS. Um preditor Venn-ABERS produz duas previsões de probabilidade para cada objeto de teste. Em poucas palavras, o preditor Venn-ABERS pode ser visto como uma função de calibração livre de distribuição que mapeia as pontuações produzidas por um classificador de pontuação para probabilidades bem calibradas.  Após utilizar o metodo de Calibração VennABERS nenhum modelo conseguiu ter um bom nivel de calibração também.**

![Plot de Calibração Ven](imagens/calibracao_plot_ven.png)








