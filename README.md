# German Credit Risk Analysis Model

## Visão Geral do Projeto
Este projeto consiste no desenvolvimento de um modelo preditivo de análise de risco de crédito utilizando o *German Credit Dataset*. O foco principal está na tomada de decisão orientada a negócios, incorporando uma matriz de custos assimétrica para minimizar prejuízos financeiros reais decorrentes de decisões incorretas de crédito.

## Origem dos Dados
* **Fonte Oficial:** UCI Machine Learning Repository - Statlog (German Credit Data)
* **Link da Base de Dados:** https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data
* **Autor / Provedor:** Professor Dr. Hans Hofmann, Institut für Statistik und Ökonometrie, Universität Hamburg.
* **Descrição do Dataset:** O conjunto de dados possui 1000 instâncias e 20 atributos (sendo 7 numéricos e 13 categóricos), descrevendo perfis de clientes tomadores de crédito.

## Regras de Negócio e Matriz de Custos
O problema utiliza uma matriz de custos assimétrica para penalizar de forma diferente os erros de classificação, onde a aprovação de crédito para um mau pagador custa cinco vezes mais do que a recusa para um bom pagador.

Matriz de custos utilizada (Linhas: Real, Colunas: Predito; 1 = Bom, 2 = Mau/Risco):
* **Classificar um cliente mau como bom (False Negative):** Custo = 5
* **Classificar um cliente bom como mau (False Positive):** Custo = 1
* **Acertos (Bom/Bom ou Mau/Mau):** Custo = 0

## Metodologia e Fluxo de Trabalho
1. **Análise Exploratória de Dados (EDA):** Verificação do balanceamento da variável alvo (70% bons pagadores, 30% maus pagadores) e mapeamento de distribuições.
2. **Pré-processamento Blindado (Anti-Data Leakage):** 
   * Divisão estratificada dos dados em treino, validação e teste.
   * Padronização de variáveis numéricas utilizando `StandardScaler`.
   * Codificação de variáveis categóricas utilizando `OneHotEncoder`.
3. **Modelagem Preditiva:**
   * Implementação de modelos de classificação (Regressão Logística, Random Forest e Gradient Boosting).
   * Otimização do limiar de decisão (*threshold*) baseada na minimização do custo financeiro total da matriz de custos no conjunto de validação.
4. **Avaliação Final:** Generalização e validação dos modelos no conjunto de teste independente.

## Resultados Finais (Conjunto de Teste)
* **Regressão Logística (Melhor Modelo):**
  * Limiar otimizado: 0.11
  * Custo Total no Teste com Limiar Otimizado: 122
  * Desempenho financeiro superior frente ao limiar padrão (0.5), evitando perdas significativas por inadimplência.
