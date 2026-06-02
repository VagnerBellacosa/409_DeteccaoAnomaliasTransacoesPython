# 🚨 Detecção de Fraudes em Transações Financeiras com Machine Learning

## 📌 Visão Geral

Este projeto demonstra a aplicação de técnicas de Ciência de Dados e Machine Learning para detecção de fraudes em transações de cartão de crédito.

Utilizamos uma das bases de dados mais conhecidas da área de Data Science, amplamente empregada em pesquisas acadêmicas, cursos e experimentos de detecção de anomalias.

O objetivo é compreender os desafios envolvidos na identificação de operações fraudulentas e construir modelos capazes de detectar comportamentos suspeitos em meio a milhões de transações legítimas.

------

## 📊 Base de Dados Utilizada

Dataset: **Credit Card Fraud Detection**

Fonte:

https://storage.googleapis.com/download.tensorflow.org/data/creditcard.csv

### Características da Base

- 284.807 transações
- 31 colunas
- Dados reais anonimizados
- Transações realizadas por cartões de crédito europeus
- Problema de classificação binária

### Variáveis

| Campo    | Descrição                                      |
| -------- | ---------------------------------------------- |
| Time     | Segundos decorridos desde a primeira transação |
| V1 a V28 | Componentes gerados por PCA                    |
| Amount   | Valor da transação                             |
| Class    | Indica fraude ou não fraude                    |

------

## 🔒 Privacidade dos Dados

Por questões de confidencialidade, os atributos originais foram transformados utilizando:

**PCA (Principal Component Analysis)**

Dessa forma, as variáveis originais foram convertidas em componentes matemáticos:

```text
V1
V2
V3
...
V28
```

Isso impede a identificação de clientes ou estabelecimentos envolvidos.

------

## 🎯 Variável Alvo

A coluna **Class** indica se a transação é fraudulenta.

| Valor | Significado        |
| ----- | ------------------ |
| 0     | Transação legítima |
| 1     | Fraude             |

Exemplo:

```python
Class = 0
```

Transação normal.

```python
Class = 1
```

Transação fraudulenta.

------

## ⚠️ O Grande Desafio: Classes Desbalanceadas

Ao analisar a distribuição da variável alvo:

```python
df["Class"].value_counts(normalize=True)
```

Obtivemos:

| Classe | Proporção |
| ------ | --------- |
| 0      | 0.998273  |
| 1      | 0.001727  |

Convertendo para percentual:

| Classe | Percentual |
| ------ | ---------- |
| Normal | 99,8273%   |
| Fraude | 0,1727%    |

------

## 📉 Por Que Isso É Um Problema?

Fraudes representam apenas:

```text
0,17%
```

das transações.

Isso significa que um modelo poderia simplesmente responder:

```text
"Tudo é normal"
```

e ainda obter aproximadamente:

```text
99,83% de acurácia
```

Mesmo sem detectar nenhuma fraude.

Por esse motivo, a métrica de acurácia isoladamente não é suficiente para avaliar modelos antifraude.

------

## 📈 Métricas Mais Adequadas

Para esse tipo de problema são utilizadas métricas como:

### Precision

Entre as transações classificadas como fraude, quantas realmente eram fraude.

### Recall

Entre todas as fraudes existentes, quantas foram encontradas.

### F1-Score

Equilíbrio entre Precision e Recall.

### ROC-AUC

Capacidade geral do modelo distinguir fraudes e operações legítimas.

------

## 🧠 Técnicas Utilizadas

O projeto explora conceitos como:

- Análise Exploratória de Dados (EDA)
- Feature Engineering
- Normalização de Dados
- Machine Learning Supervisionado
- Machine Learning Não Supervisionado
- Detecção de Anomalias
- Balanceamento de Classes

------

## 🔧 Bibliotecas Utilizadas

```python
pandas
numpy
matplotlib
seaborn
scikit-learn
```

------

## 🚀 Carregamento da Base

```python
import pandas as pd

url = "https://storage.googleapis.com/download.tensorflow.org/data/creditcard.csv"

df = pd.read_csv(url)

df.head()
```

------

## 📊 Análise Inicial

```python
df.info()

df.describe()

df.isnull().sum()
```

------

## 🏗️ Próximas Etapas

O fluxo típico do projeto inclui:

1. Carregamento dos dados
2. Análise exploratória
3. Tratamento de valores
4. Engenharia de atributos
5. Balanceamento das classes
6. Treinamento dos modelos
7. Avaliação das métricas
8. Identificação de transações suspeitas

------

## 🏦 Aplicações Reais

Os conceitos demonstrados neste projeto são amplamente utilizados em:

- Bancos
- Fintechs
- Operadoras de cartão de crédito
- Sistemas PIX
- Plataformas de pagamento
- Sistemas de auditoria financeira

------

## ☕ Curiosidade Mainframe

Grande parte das transações financeiras do mundo continua sendo processada por ambientes IBM Z (Mainframe).

Em muitos bancos, o fluxo real ocorre da seguinte forma:

```text
POS / ATM
      ↓
API Gateway
      ↓
CICS
      ↓
COBOL
      ↓
DB2
      ↓
Motor Antifraude
      ↓
Autorização da Transação
```

Os modelos de Machine Learning analisam dados produzidos por aplicações críticas executadas em ambientes z/OS, demonstrando a integração entre tecnologias modernas de IA e plataformas tradicionais de missão crítica.

------

## 👨‍💻 Autor

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

## ⭐ Apoie o Projeto

Se este conteúdo foi útil:

⭐ Deixe uma estrela no repositório

🍴 Faça um Fork

📢 Compartilhe com a comunidade

☕ Continue acompanhando os projetos do Bellacosa Mainframe & Data Science.

