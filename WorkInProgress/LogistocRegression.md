Aqui está um **README.md** focado na utilização de **Regressão Logística (Logistic Regression)** para o projeto de detecção de fraudes em transações financeiras.

# 🚨 Detecção de Fraudes em Cartões de Crédito com Logistic Regression

## 📌 Visão Geral

Este projeto demonstra a utilização do algoritmo **Logistic Regression (Regressão Logística)** para identificar transações fraudulentas em operações de cartão de crédito.

Embora seja um dos algoritmos mais simples da área de Machine Learning, a Regressão Logística continua sendo amplamente utilizada no mercado financeiro devido à sua:

- Simplicidade
- Rapidez de treinamento
- Facilidade de interpretação
- Excelente desempenho em problemas de classificação binária

------

# 🎯 Objetivo

Construir um modelo capaz de prever se uma transação é:

| Classe | Significado           |
| ------ | --------------------- |
| 0      | Transação legítima    |
| 1      | Transação fraudulenta |

A partir das características presentes na base de dados.

------

# 📊 Base de Dados

Utilizamos o dataset:

**Credit Card Fraud Detection Dataset**

Características:

- 284.807 transações
- 31 colunas
- Dados anonimizados por PCA
- 492 fraudes registradas

------

# 🔍 Estrutura da Base

| Campo  | Descrição                        |
| ------ | -------------------------------- |
| Time   | Tempo desde a primeira transação |
| V1-V28 | Componentes gerados por PCA      |
| Amount | Valor da transação               |
| Class  | Variável alvo                    |

------

# ⚠️ Problema de Classes Desbalanceadas

A distribuição das classes é extremamente desigual:

| Classe | Quantidade |
| ------ | ---------- |
| 0      | 284.315    |
| 1      | 492        |

Percentualmente:

| Classe | Percentual |
| ------ | ---------- |
| Normal | 99,83%     |
| Fraude | 0,17%      |

Esse cenário representa um desafio comum em sistemas antifraude reais.

------

# 🧠 O Que é Logistic Regression?

Apesar do nome "regressão", trata-se de um algoritmo de:

## Classificação

Seu objetivo é calcular a probabilidade de uma observação pertencer a uma determinada classe.

Exemplo:

```text
Probabilidade de Fraude = 0.97
```

Resultado:

```text
Fraude
```

Ou:

```text
Probabilidade de Fraude = 0.04
```

Resultado:

```text
Transação Normal
```

------

# 📐 Função Sigmoide

A Logistic Regression utiliza a função logística (sigmoide):

P(y=1)=\frac{1}{1+e^{-z}}

Essa função converte qualquer valor em uma probabilidade entre:

```text
0 e 1
```

------

# 🔧 Bibliotecas Utilizadas

```python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

from sklearn.linear_model import LogisticRegression

from sklearn.metrics import (
    confusion_matrix,
    classification_report,
    roc_auc_score
)
```

------

# 📥 Carregamento dos Dados

```python
import pandas as pd

url = "https://storage.googleapis.com/download.tensorflow.org/data/creditcard.csv"

df = pd.read_csv(url)
```

------

# 🧹 Preparação dos Dados

Separação das variáveis:

```python
X = df.drop("Class", axis=1)

y = df["Class"]
```

------

# 🔄 Divisão Treino e Teste

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42,
    stratify=y
)
```

------

# 📏 Padronização

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)

X_test = scaler.transform(X_test)
```

------

# 🤖 Treinamento do Modelo

```python
from sklearn.linear_model import LogisticRegression

modelo = LogisticRegression(
    class_weight='balanced',
    max_iter=1000
)

modelo.fit(X_train, y_train)
```

A opção:

```python
class_weight='balanced'
```

ajuda a compensar o forte desbalanceamento da base.

------

# 🔍 Realizando Previsões

```python
y_pred = modelo.predict(X_test)

y_prob = modelo.predict_proba(X_test)[:,1]
```

------

# 📊 Avaliação do Modelo

## Matriz de Confusão

```python
from sklearn.metrics import confusion_matrix

cm = confusion_matrix(y_test, y_pred)

print(cm)
```

------

## Classification Report

```python
from sklearn.metrics import classification_report

print(
    classification_report(
        y_test,
        y_pred
    )
)
```

------

## ROC-AUC

```python
from sklearn.metrics import roc_auc_score

roc_auc = roc_auc_score(
    y_test,
    y_prob
)

print(roc_auc)
```

------

# 📈 Métricas Importantes

Para problemas de fraude devemos observar:

## Precision

Entre as transações classificadas como fraude:

> Quantas realmente eram fraude?

------

## Recall

Entre todas as fraudes existentes:

> Quantas conseguimos detectar?

------

## F1-Score

Equilíbrio entre Precision e Recall.

------

## ROC-AUC

Capacidade do modelo distinguir transações legítimas de fraudulentas.

------

# 💡 Vantagens da Logistic Regression

✅ Simples de implementar

✅ Treinamento rápido

✅ Fácil interpretação

✅ Baixo consumo de recursos

✅ Excelente baseline para comparação

------

# ⚠️ Limitações

❌ Pode perder padrões muito complexos

❌ Sensível ao desbalanceamento

❌ Menor poder preditivo que modelos mais sofisticados

Exemplos:

- Random Forest
- XGBoost
- LightGBM
- Neural Networks

------

# 🏦 Aplicação no Mercado Financeiro

Modelos baseados em Regressão Logística ainda são utilizados em:

- Score de crédito
- Aprovação de empréstimos
- Detecção de fraudes
- Análise de risco
- Prevenção à lavagem de dinheiro

Sua interpretabilidade facilita auditorias e conformidade regulatória.

------

# ☕ Curiosidade Mainframe

Muitos motores de decisão utilizados por bancos processam milhões de transações originadas em sistemas COBOL executando em IBM Z.

Fluxo típico:

```text
Terminal / App
      ↓
API Gateway
      ↓
CICS
      ↓
COBOL
      ↓
DB2
      ↓
Modelo de Machine Learning
      ↓
Decisão da Transação
```

A Logistic Regression foi um dos primeiros algoritmos amplamente utilizados em motores de risco bancário e continua presente em diversas soluções corporativas.

------

# 👨‍💻 Autor

**Vagner Bellacosa**

Especialista em:

- IBM Mainframe
- COBOL
- CICS
- DB2
- Python
- Data Science
- Machine Learning
- Inteligência Artificial

GitHub:
https://github.com/VagnerBellacosa

LinkedIn:
https://www.linkedin.com/in/vagnerbellacosa

------

# ⭐ Apoie o Projeto

Se este projeto ajudou seus estudos:

⭐ Deixe uma estrela no repositório

🍴 Faça um Fork

📢 Compartilhe com a comunidade

☕ Continue acompanhando os projetos Bellacosa Mainframe & Data Science.