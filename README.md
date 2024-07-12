# Desafio-BIX-Tecnologia
Esse repositório faz parte de uma das etapas para a seleção da vaga na empresa Bix Tecnologia. As respostas para o desafio estão listadas nesse [README](respostas.md):

# Descrição do Desafio em Ciência de Dados Aplicada à Otimização de Planejamento de Manutenção

## Resumo

### Situação

Uma nova empresa de consultoria em ciência de dados foi contratada para resolver e melhorar o planejamento de manutenção de uma empresa terceirizada de transporte. A empresa mantém um número médio de caminhões em sua frota para entregas em todo o país, mas nos últimos 3 anos tem notado um grande aumento nas despesas relacionadas à manutenção do sistema de ar de seus veículos, mesmo mantendo o tamanho de sua frota relativamente constante. O custo de manutenção deste sistema específico é mostrado abaixo em dólares:

Seu objetivo como consultor é diminuir os custos de manutenção desse sistema em particular. Os custos de manutenção do sistema de ar podem variar dependendo da condição real do caminhão.

- Se um caminhão for enviado para manutenção, mas não apresentar defeito nesse sistema, cerca de $10 serão cobrados pelo tempo gasto durante a inspeção pela equipe especializada.
- Se um caminhão for enviado para manutenção e apresentar defeito nesse sistema, $25 serão cobrados para realizar o serviço de reparo preventivo.
- Se um caminhão com defeito no sistema de ar não for enviado diretamente para manutenção, a empresa paga $500 para realizar a manutenção corretiva, considerando a mão de obra, substituição de peças e outros possíveis inconvenientes (por exemplo, o caminhão quebrar no meio do trajeto).

Durante a reunião de alinhamento com os responsáveis pelo projeto e a equipe de TI da empresa, algumas informações foram fornecidas:

- A equipe técnica informou que todas as informações sobre o sistema de ar dos caminhões estarão disponíveis, mas, por razões burocráticas relacionadas aos contratos da empresa, todas as colunas tiveram que ser codificadas.
- A equipe técnica também informou que, devido à recente digitalização da empresa, algumas informações podem estar faltando no banco de dados enviado.
- Finalmente, a equipe técnica informou que a fonte de informação vem do setor de manutenção da empresa, onde foi criada uma coluna no banco de dados chamada "class": "pos" seriam os caminhões que apresentaram defeitos no sistema de ar e "neg" seriam os caminhões que apresentaram defeitos em qualquer sistema que não fosse o de ar.

Os responsáveis pelo projeto estão muito empolgados com a iniciativa e, ao solicitar uma prova de conceito técnica, colocaram como principais requisitos:
- Podemos reduzir nossos gastos com este tipo de manutenção usando técnicas de IA?
- Você pode apresentar os principais fatores que indicam uma possível falha neste sistema?
  
Esses pontos, segundo eles, são importantes para convencer o conselho executivo a abraçar a causa e aplicá-la a outros sistemas de manutenção durante o ano de 2022.

## Sobre o banco de dados

Dois arquivos serão enviados para você:
1. [air_system_previous_years.csv](air_system_previous_years.csv): Arquivo contendo todas as informações do setor de manutenção para os anos anteriores a 2022, com 178 colunas.
2. [air_system_present_year.csv](air_system_present_year.csv): Arquivo contendo todas as informações do setor de manutenção neste ano.
  
Qualquer valor ausente no banco de dados é denotado por `na`.

Os resultados finais que serão apresentados ao conselho executivo precisam ser avaliados em relação ao `air_system_present_year.csv`.

## Atividades do Desafio

Para resolver este problema, queremos que você responda às seguintes perguntas:

1. Quais passos você tomaria para resolver este problema? Descreva de forma completa e clara todos os passos que você considera essenciais para a resolução do problema.
2. Qual métrica técnica de ciência de dados você utilizaria para resolver este desafio? Ex: erro absoluto, RMSE, etc.
3. Qual métrica de negócio você utilizaria para resolver o desafio?
4. Como as métricas técnicas se relacionam com as métricas de negócio?
5. Que tipos de análises você gostaria de realizar no banco de dados do cliente?
6. Quais técnicas você utilizaria para reduzir a dimensionalidade do problema?
7. Quais técnicas você utilizaria para selecionar variáveis para seu modelo preditivo?
8. Quais modelos preditivos você utilizaria ou testaria para este problema? Indique pelo menos 3.
9. Como você avaliaria qual dos modelos treinados é o melhor?
10. Como você explicaria o resultado do seu modelo? É possível saber quais variáveis são mais importantes?
11. Como você avaliaria o impacto financeiro do modelo proposto?
12. Quais técnicas você utilizaria para realizar a otimização de hiperparâmetros do modelo escolhido?
13. Quais riscos ou precauções você apresentaria ao cliente antes de colocar este modelo em produção?
14. Se seu modelo preditivo for aprovado, como você o colocaria em produção?
15. Se o modelo estiver em produção, como você o monitoraria?
16. Se o modelo estiver em produção, como você saberia quando re-treiná-lo?

