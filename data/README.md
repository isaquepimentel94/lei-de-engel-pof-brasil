# Lei de Engel no Brasil com microdados da POF 2017–2018

Projeto de análise de dados e Machine Learning utilizando microdados da Pesquisa de Orçamentos Familiares (POF) 2017–2018, com o objetivo de investigar empiricamente a Lei de Engel no Brasil.

## Objetivo

A Lei de Engel descreve uma regularidade segundo a qual, à medida que a renda das famílias aumenta, a proporção do orçamento destinada à alimentação tende a diminuir.

A principal pergunta do projeto é:

**A participação da alimentação na renda diminui conforme aumenta a renda das unidades de consumo brasileiras?**

Além da análise econômica e econométrica, o projeto também utiliza `LinearSVC` para identificar unidades de consumo com alta pressão alimentar no orçamento.

## Estrutura do projeto

```text
POF/
├── data/
│   ├── raw/
│   └── processed/
├── figures/
├── Notebooks/
│   ├── 01_exploracao_pof.ipynb
│   ├── 02_lei_de_engel.ipynb
│   └── 03_linear_svc.ipynb
├── SRC/
│   └── tratamento.py
├── README.md
└── .gitignore
```

## Etapas da análise

### 1. Exploração e preparação dos dados

- leitura dos microdados da POF;
- estruturação de arquivos de largura fixa;
- investigação das variáveis;
- identificação e revisão dos códigos de produtos alimentares;
- construção da despesa alimentar mensal;
- agregação dos registros por unidade de consumo;
- validação de renda e tratamento de inconsistências;
- construção da base analítica final.

### 2. Análise da Lei de Engel

- cálculo da participação da alimentação na renda;
- análise por decis de renda;
- comparação entre média e mediana;
- correlações de Pearson e Spearman;
- regressão com renda em escala logarítmica;
- análise de robustez com erros-padrão HC3;
- regressão múltipla com características familiares.

Os resultados mostram uma relação inversa entre renda e participação alimentar. Na análise por decis, a mediana da participação da alimentação cai de aproximadamente 27% entre os 10% de menor renda para cerca de 4% entre os 10% de maior renda.

### 3. Classificação com LinearSVC

A participação alimentar foi transformada em um problema de classificação, considerando como alta pressão alimentar as unidades de consumo pertencentes aos 25% maiores valores da distribuição.

Foram comparadas duas versões do modelo:

- `LinearSVC` padrão;
- `LinearSVC` com `class_weight="balanced"`.

O modelo balanceado reduziu a acurácia geral, mas aumentou significativamente a capacidade de identificar a classe de interesse. O recall da classe de alta pressão alimentar passou de aproximadamente 18% para 69%.

Entre as variáveis analisadas, a renda apresentou o coeficiente de maior magnitude e sinal negativo, enquanto o número de moradores apresentou a principal contribuição positiva para a classificação em alta pressão alimentar.

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- SciPy
- Statsmodels
- Scikit-learn
- Jupyter Notebook

## Dados

Os dados utilizados são provenientes da Pesquisa de Orçamentos Familiares (POF) 2017–2018.

Os arquivos brutos não são versionados neste repositório. A pasta `data/raw/` é ignorada pelo Git.

As bases processadas utilizadas nas etapas de análise e modelagem são armazenadas em `data/processed/`.

## Observações metodológicas

A análise de alimentação neste projeto é baseada nos registros utilizados para construção da despesa alimentar domiciliar a partir da Caderneta Coletiva.

Os modelos apresentados identificam associações e padrões nos dados e não devem ser interpretados como evidência causal.

## Autor

Isaque Pimentel de Souza Ferreira