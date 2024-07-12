# Respostas para o questionário

## 1. Quais passos você tomaria para resolver este problema? Descreva de forma completa e clara todos os passos que você considera essenciais para a resolução do problema.**

## 2. Qual métrica técnica de ciência de dados você utilizaria para resolver este desafio? Ex: erro absoluto, RMSE, etc.

**A métrica técnica que eu utilizaria para resolver esse desafio é o recall. Em um cenário onde os dados estão desbalanceados, o recall se destaca por capturar eficientemente a proporção de verdadeiros positivos que foram corretamente identificados pelo modelo. Isso é particularmente relevante quando o foco está na detecção correta dos caminhões com defeito, minimizando o risco de falsos negativos (defeitos não detectados).**


## 3. Qual métrica de negócio você utilizaria para resolver o desafio?

**Uma métrica de negócio relevante para resolver esse desafio seria o custo total de manutenção do sistema de ar de todos os caminhões. Essa métrica permite comparar diretamente o custo antes e depois da implementação do modelo de detecção de defeitos. A ideia é avaliar o impacto econômico real do modelo ao longo do tempo.**

## 4. Como as métricas técnicas se relacionam com as métricas de negócio?
**As métricas técnicas e as métricas de negócio são complementares e devem ser avaliadas em conjunto para garantir que um projeto de ciência de dados não apenas entregue modelos precisos, mas também gere valor tangível para a organização.**

## 5. Que tipos de análises você gostaria de realizar no banco de dados do cliente?
**O principal e mais importante problema é a alta incidência de valores nulos e muitos valores zeros nos dados. É crucial investigar as causas dessa abundância de dados descartáveis e identificar quais colunas não são necessárias.**

## 6. Quais técnicas você utilizaria para reduzir a dimensionalidade do problema?
**Primeiro usei o algoritimo VarianceThreshold para retirar colunas com nenhuma variação dos dados,
apos isso, usei o algoritimo SmartCorrelatedSelection() com limite de 0.70, eliminando as colunas com alta correlação, e apos isso, usei o algoritimo RFE()(Eliminação Recursiva de Recursos) para selecionar as colunas as 20 colunas mais importantes para o modelo.**


