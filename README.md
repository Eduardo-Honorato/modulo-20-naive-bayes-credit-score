# Módulo 20: Projeto de Credit Score com Naive Bayes

Exercício do curso Profissão: Cientista de Dados (EBAC). Aplica o algoritmo Naive Bayes às bases de crédito tratadas no Módulo 17 para prever o score de crédito de cada cliente em três classes: Low (baixo), Average (médio) e High (alto).

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Eduardo-Honorato/modulo-20-naive-bayes-credit-score/blob/main/Profissao_Cientista_de_Dados_M20_Pratique_resolvido.ipynb)

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `Profissao_Cientista_de_Dados_M20_Pratique_resolvido.ipynb` | Notebook com código, saídas e interpretações |
| `X_treino.csv`, `y_treino.csv` | Base de treino, balanceada com oversampling (270 linhas) |
| `X_teste.csv`, `y_teste.csv` | Base de teste, com a distribuição original das classes (33 linhas) |

As bases foram geradas no Módulo 17 (tratamento, codificação das variáveis categóricas, divisão em treino e teste e balanceamento apenas do treino). O score foi codificado como Low = 0, Average = 1 e High = 2.

## O que o notebook faz

1. Carrega as quatro bases e valida linhas, colunas, valores nulos e o balanceamento das classes.
2. Treina o `GaussianNB` na base de treino.
3. Avalia o treino com acurácia, recall macro e matriz de confusão.
4. Avalia o teste da mesma forma e compara com o treino.
5. Descreve o projeto e o objetivo de aplicar o Naive Bayes à base de crédito.
6. Bônus: painel interativo em React e Tailwind CSS com a matriz de confusão, a comparação treino x teste e uma demonstração de como o modelo decide.

## Resultados

| | Treino (270 clientes) | Teste (33 clientes) |
|---|---|---|
| Acurácia | 99,26% | 96,97% |
| Recall macro | 99,26% | 95,24% |

No treino houve 2 erros, e no teste houve 1: um cliente `Average` previsto como `High`. Os erros ocorreram sempre entre classes vizinhas, e o modelo não confundiu `Low` com `High`.

## Limitações

- **Teste pequeno:** são 33 clientes, com apenas 3 `Low` e 7 `Average`. Um único erro muda a acurácia em cerca de 3 pontos.
- **Teste não balanceado:** cerca de 70% dos clientes do teste são `High`. Um modelo que chutasse sempre `High` acertaria quase 70%, por isso o recall macro é a métrica mais informativa.
- **Cópias entre treino e teste:** 12 dos 33 clientes do teste (36%) têm uma cópia idêntica no treino, porque as linhas duplicadas foram mantidas no Módulo 17. Avaliando apenas os 21 clientes sem cópia, a acurácia foi de 95,24% e o recall macro de 91,67%. O desempenho continua alto, mas o resultado do teste completo é um pouco otimista.
- **Melhoria possível:** remover as duplicatas antes de separar treino e teste.

## Como executar

O caminho mais simples é abrir no Google Colab pelo botão acima e enviar os quatro CSVs para o painel de arquivos. Para rodar localmente:

```bash
pip install pandas numpy seaborn matplotlib scikit-learn jupyter
jupyter notebook Profissao_Cientista_de_Dados_M20_Pratique_resolvido.ipynb
```

Mantenha os quatro CSVs na mesma pasta do notebook e execute as células na ordem, começando pela de imports. O painel interativo da seção 6 precisa de conexão com a internet, porque carrega React e Tailwind CSS por CDN. O GitHub mostra o notebook, mas não executa esse painel.

## Tecnologias

Python, pandas, NumPy, seaborn, Matplotlib, scikit-learn, React e Tailwind CSS.
