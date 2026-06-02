# Aplicando a etapa de treinamento da **Logistic Regression** 

O código executado é semelhante a:

```python
from sklearn.model_selection import train_test_split

X = df.drop("Class", axis=1)
y = df["Class"]

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    stratify=y,
    test_size=0.3,
    random_state=42
)
```

Em seguida:

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)

model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

Durante o treinamento apareceu o aviso:

```text
ConvergenceWarning:
lbfgs failed to converge
STOP: TOTAL NO. OF ITERATIONS REACHED LIMIT
```

------

# O que significa esse aviso?

O algoritmo tentou encontrar os melhores coeficientes matemáticos para separar:

```text
Fraudes
vs
Transações Normais
```

Mas não conseguiu convergir antes de atingir o limite de:

```python
max_iter = 1000
```

Ou seja:

> O treinamento parou porque atingiu o número máximo de iterações permitidas.

------

# Isso é um erro?

Não.

É um aviso.

O modelo foi treinado e produziu previsões:

```python
y_pred = model.predict(X_test)
```

Porém existe uma chance de os coeficientes ainda não terem alcançado a solução ótima.

------

# Por que isso acontece?

Na base Credit Card Fraud Detection existem alguns fatores que dificultam a convergência:

## 1. Grande volume de dados

A base possui:

```text
284.807 registros
```

------

## 2. Muitas variáveis

Temos:

```text
V1 até V28
Amount
Time
```

Total:

```text
30 atributos preditores
```

------

## 3. Escalas diferentes

Exemplo:

```text
Amount = 149.62
```

Enquanto:

```text
V1 = -1.35
V2 = 0.26
V3 = 2.53
```

As magnitudes são diferentes.

------

## 4. Forte desbalanceamento

```text
99,83% normais

0,17% fraudes
```

Isso torna a fronteira de decisão mais difícil de encontrar.

------

# Como corrigir?

## Solução 1 (Mais comum)

Padronizar os dados.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)

X_test = scaler.transform(X_test)
```

Depois:

```python
model = LogisticRegression(
    max_iter=1000
)
```

------

## Solução 2

Aumentar o número de iterações.

```python
model = LogisticRegression(
    max_iter=5000
)
```

------

## Solução 3

Usar pesos para compensar as fraudes.

```python
model = LogisticRegression(
    class_weight="balanced",
    max_iter=5000
)
```

Essa costuma ser uma excelente prática neste dataset.

------

# Melhor versão para este projeto

```python
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

model = LogisticRegression(
    class_weight="balanced",
    max_iter=5000,
    random_state=42
)

model.fit(X_train, y_train)
```

------

# O que significa Logistic Regression?

Apesar do nome, ela não faz regressão.

Ela faz:

```text
CLASSIFICAÇÃO
```

Calculando a probabilidade de uma transação ser fraude.

A função central utilizada é:

P(y=1)=\frac{1}{1+e^{-z}}

Quando o resultado se aproxima de:

```text
1
```

a chance de fraude aumenta.

Quando se aproxima de:

```text
0
```

a transação é considerada legítima.

------

# Curiosidade Mainframe ☕💣

A lógica por trás da Logistic Regression lembra muito os antigos **Credit Scoring Systems** implementados em COBOL nos anos 80 e 90.

Em vez de redes neurais complexas, os sistemas bancários calculavam pontuações de risco utilizando fórmulas lineares ponderadas:

```text
Risco =
Peso_Renda
+ Peso_Idade
+ Peso_Histórico
+ Peso_Endividamento
```

A Logistic Regression é, em essência, uma evolução matemática desse mesmo conceito, adicionando uma função probabilística para transformar o score em uma probabilidade de fraude ou inadimplência. Isso explica por que ela continua sendo amplamente utilizada em bancos, seguradoras e instituições financeiras até hoje.