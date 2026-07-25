# 🍷 Wine Quality Classification

Classificação da qualidade de vinhos tintos utilizando Machine Learning, a partir de suas características físico-químicas.

> Tech Challenge — Fase 2 | Pós-Tech (POSTECH)

## 📋 Sobre o Projeto

A avaliação da qualidade de um vinho é tradicionalmente feita por especialistas através de análise sensorial (aroma, sabor, acidez, equilíbrio), um processo subjetivo, demorado e dependente da experiência do avaliador.

Este projeto utiliza técnicas de ciência de dados e aprendizado de máquina para prever a qualidade de vinhos tintos com base em variáveis físico-químicas mensuráveis objetivamente em laboratório (acidez, teor alcoólico, densidade, dióxido de enxofre, entre outras), auxiliando produtores e enólogos na tomada de decisão durante o processo produtivo.

O problema foi tratado como uma **classificação binária**:

- **Alta Qualidade**: nota de qualidade ≥ 7
- **Baixa/Média Qualidade**: nota de qualidade < 7

## 📊 Dataset

- **Fonte**: [Wine Quality Dataset (Kaggle)](https://www.kaggle.com/datasets/yasserh/wine-quality-dataset/data)
- **Amostras**: ~1.143 vinhos tintos
- **Variáveis**: 11 features físico-químicas (acidez fixa, acidez volátil, ácido cítrico, açúcar residual, cloretos, dióxido de enxofre livre e total, densidade, pH, sulfatos, teor alcoólico) + variável alvo (`quality`)

## 🔎 Principais Insights da Análise Exploratória

- O dataset apresenta **forte desbalanceamento de classes**: 86,1% dos vinhos são de baixa/média qualidade e apenas 13,9% de alta qualidade.
- **Teor alcoólico** (`alcohol`) é a variável mais correlacionada positivamente com a qualidade (r = 0,40).
- **Acidez volátil** (`volatile acidity`) é a variável mais correlacionada negativamente (r = -0,30), refletindo o defeito sensorial de "gosto de vinagre".
- Foi identificada multicolinearidade relevante entre `fixed acidity`, `pH`, `citric acid` e `density`.
- Outliers mais expressivos foram encontrados em `residual sugar` (9,6%) e `chlorides` (6,7%), tratados via *capping* (winsorization) ao invés de remoção, para preservar amostras da classe minoritária.

## 🤖 Modelos Desenvolvidos

Foram treinados e comparados três modelos de classificação:

| Modelo | Acurácia | Precisão | Recall | F1-Score | AUC-ROC |
|---|---|---|---|---|---|
| **Random Forest** | 0.908 | 0.720 | 0.562 | **0.632** | **0.906** |
| Gradient Boosting | 0.878 | 0.553 | **0.656** | 0.600 | 0.877 |
| Regressão Logística | 0.777 | 0.349 | 0.688 | 0.463 | 0.841 |

**Random Forest** apresentou o melhor desempenho geral, com o maior F1-Score e AUC-ROC, sendo o modelo escolhido para a análise de importância de variáveis.

### Variáveis mais influentes na qualidade (Random Forest)

1. `alcohol` (teor alcoólico)
2. `citric acid` (ácido cítrico)
3. `sulphates` (sulfatos)
4. `volatile acidity` (acidez volátil)

## 🗂️ Estrutura do Repositório

```
wine-quality-classification/
│
├── data/               # Base de dados utilizada (WineQT.csv)
├── notebooks/          # Notebook com a análise exploratória e modelagem
├── results/             # Gráficos, métricas e comparações dos modelos
├── requirements.txt    # Bibliotecas utilizadas
└── README.md           # Este arquivo
```

## ⚙️ Pipeline do Projeto

1. **Compreensão do Problema** — definição do contexto e transformação da variável alvo em classificação binária.
2. **Análise Exploratória de Dados (EDA)** — distribuições, correlações, outliers e balanceamento de classes.
3. **Pré-processamento** — tratamento de outliers, split treino/teste estratificado, padronização (`StandardScaler`) e engenharia de features.
4. **Desenvolvimento de Modelos** — Regressão Logística, Random Forest e Gradient Boosting.
5. **Avaliação dos Modelos** — comparação via acurácia, precisão, recall, F1-score, AUC-ROC, matriz de confusão e curva ROC.
6. **Interpretação dos Resultados** — análise de importância das variáveis e implicações para o processo produtivo.



## 🛠️ Tecnologias Utilizadas

- Python 3.x
- pandas / numpy
- matplotlib / seaborn
- scikit-learn

## 📈 Apresentação Executiva

O storytelling completo da análise exploratória está disponível em [`Apresentação.pdf`](./Apresentação.pdf).


## 🎓 Contexto Acadêmico

Projeto desenvolvido como parte do **Tech Challenge — Fase 2** da Pós-Tech (POSTECH), integrando os conhecimentos de Data Analytics e Machine Learning da fase.

