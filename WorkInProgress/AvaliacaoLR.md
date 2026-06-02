# 🚨 Avaliação de Modelo Logistic Regression para Detecção de Fraudes

## 📌 Visão Geral

Neste projeto utilizamos o algoritmo **Logistic Regression** para identificar transações fraudulentas em uma base de cartões de crédito.

Após o treinamento do modelo, realizamos a avaliação utilizando o **Classification Report** do Scikit-Learn, que fornece métricas detalhadas para cada classe.

------

# 🎯 Objetivo

Classificar cada transação em uma das categorias:

| Classe | Significado           |
| ------ | --------------------- |
| 0      | Transação legítima    |
| 1      | Transação fraudulenta |

------

# 🏗️ Treinamento do Modelo

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)

model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

Durante o treinamento foi exibido o aviso:

```text
ConvergenceWarning:
lbfgs failed to converge
STOP: TOTAL NO. OF ITERATIONS REACHED LIMIT
```

Esse aviso indica que o algoritmo atingiu o limite máximo de iterações antes de encontrar a solução ótima.

Embora o modelo funcione normalmente, recomenda-se:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

model = LogisticRegression(
    class_weight='balanced',
    max_iter=5000
)
```

------

# 📊 Resultados Obtidos

Classification Report:

```text
              precision    recall   f1-score   support

0               1.00       1.00      1.00      85295

1               0.87       0.68      0.77        148

accuracy                              1.00     85443

macro avg       0.94       0.84      0.88

weighted avg    1.00       1.00      1.00
```

------

# 🔍 Interpretação dos Resultados

## Classe 0 — Transações Normais

```text
Precision = 1.00
Recall    = 1.00
F1-Score  = 1.00
```

O modelo praticamente não comete erros ao identificar operações legítimas.

------

## Classe 1 — Fraudes

```text
Precision = 0.87
Recall    = 0.68
F1-Score  = 0.77
```

Esses valores merecem atenção especial.

------

# 📈 Precision

```text
87%
```

Das transações classificadas como fraude:

```text
87%
```

realmente eram fraudes.

Isso significa que o número de falsos alarmes é relativamente baixo.

------

# 📈 Recall

```text
68%
```

Das fraudes existentes na base de teste:

```text
68%
```

foram identificadas.

Em outras palavras:

```text
32%
```

das fraudes passaram despercebidas.

------

# 📈 F1-Score

```text
0.77
```

O F1-Score representa o equilíbrio entre Precision e Recall.

Para problemas desbalanceados, essa métrica é muito mais relevante que a acurácia.

------

# ⚠️ Cuidado com a Accuracy

O relatório apresenta:

```text
Accuracy = 1.00
```

Ou seja:

```text
100%
```

de acurácia aparente.

Entretanto, a base possui aproximadamente:

```text
99,83%
```

de transações legítimas.

Por isso, a acurácia isoladamente pode gerar uma falsa sensação de desempenho perfeito.

Em problemas de fraude, devemos focar principalmente em:

- Recall
- Precision
- F1-Score
- ROC-AUC

------

# 📊 Análise de Negócio

Supondo:

```text
148 fraudes reais
```

e um Recall de:

```text
68%
```

o modelo conseguiu identificar aproximadamente:

```text
101 fraudes
```

mas deixou escapar cerca de:

```text
47 fraudes
```

que continuariam circulando pelo sistema financeiro.

------

# 🚀 Possíveis Melhorias

Para aumentar a capacidade de detecção de fraudes:

### Balanceamento de Classes

```python
class_weight='balanced'
```

------

### Oversampling

```python
SMOTE
```

------

### Random Forest

```python
RandomForestClassifier()
```

------

### XGBoost

```python
XGBClassifier()
```

------

### LightGBM

```python
LGBMClassifier()
```

------

### Detecção de Anomalias

- Isolation Forest
- One-Class SVM
- Local Outlier Factor

------

# 🏦 Aplicação no Mercado Financeiro

Modelos semelhantes são utilizados em:

- Bancos
- Operadoras de cartão
- Fintechs
- Sistemas PIX
- Gateways de pagamento

O objetivo é atribuir um score de risco para cada operação antes da autorização financeira.

------

# ☕ Curiosidade Mainframe

Em grandes instituições financeiras, os dados utilizados por modelos de Machine Learning normalmente são produzidos por aplicações executadas em IBM Z.

Fluxo simplificado:

```text
POS / ATM
      ↓
CICS
      ↓
COBOL
      ↓
DB2
      ↓
Motor Antifraude
      ↓
Aprovação ou Bloqueio
```

Embora a análise seja realizada em Python, a origem das informações frequentemente está em sistemas COBOL responsáveis por bilhões de transações diariamente.

------

# 📚 Conclusão

O modelo Logistic Regression apresentou excelente desempenho geral e conseguiu identificar uma parcela significativa das fraudes.

Resultados observados:

✅ Precision de 87%

✅ Recall de 68%

✅ F1-Score de 77%

✅ Excelente baseline para comparação com modelos mais avançados

Apesar disso, ainda existem oportunidades para melhorar a detecção da classe fraudulenta utilizando técnicas de balanceamento e algoritmos mais sofisticados.

