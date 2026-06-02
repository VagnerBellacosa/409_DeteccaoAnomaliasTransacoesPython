# README.md — Detecção de Anomalias em Transações com Python

# 🚨 Detecção de Anomalias em Transações Financeiras com Python

Projeto desenvolvido para identificar transações suspeitas utilizando técnicas de **Machine Learning Não Supervisionado**, permitindo detectar comportamentos incomuns que podem indicar fraudes, erros operacionais ou atividades atípicas.

------

## 📋 Sobre o Projeto

Em ambientes financeiros, nem sempre existem registros históricos rotulados de fraude para treinar modelos supervisionados.

Neste cenário, algoritmos de **Detecção de Anomalias** são extremamente úteis, pois aprendem o comportamento normal dos dados e sinalizam eventos que fogem do padrão esperado.

Neste projeto são aplicadas técnicas de Ciência de Dados e Machine Learning para:

- Analisar transações financeiras
- Identificar comportamentos anormais
- Gerar indicadores de risco
- Apoiar processos de prevenção a fraudes

------

## 🎯 Objetivos

- Explorar dados transacionais
- Realizar tratamento e preparação dos dados
- Aplicar algoritmos de detecção de anomalias
- Visualizar resultados
- Avaliar a eficiência do modelo
- Identificar possíveis transações suspeitas

------

## 🧠 Conceitos Utilizados

### Análise Exploratória de Dados (EDA)

- Estatísticas descritivas
- Distribuição dos valores
- Correlação entre variáveis
- Identificação de outliers

### Machine Learning

- Aprendizado Não Supervisionado
- Clustering
- Detecção de Outliers
- Engenharia de Atributos

### Métricas

- WSS (Within Cluster Sum of Squares)
- Silhouette Score
- Taxa de Anomalias Detectadas
- Distância ao Centroide

------

## 🛠 Tecnologias Utilizadas

- Python 3.x
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- Jupyter Notebook

------

## 📂 Estrutura do Projeto

```text
409_DeteccaoAnomaliasTransacoesPython/
│
├── dados/
│   ├── transacoes.csv
│
├── notebooks/
│   ├── deteccao_anomalias.ipynb
│
├── imagens/
│   ├── distribuicao.png
│   ├── clusters.png
│
├── README.md
└── requirements.txt
```

------

## ⚙️ Instalação

Clone o repositório:

```bash
git clone https://github.com/VagnerBellacosa/409_DeteccaoAnomaliasTransacoesPython.git
```

Entre no diretório:

```bash
cd 409_DeteccaoAnomaliasTransacoesPython
```

Crie um ambiente virtual:

### Windows

```bash
python -m venv venv

venv\Scripts\activate
```

### Linux / Mac

```bash
python3 -m venv venv

source venv/bin/activate
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

------

## ▶️ Executando o Projeto

Abra o Jupyter Notebook:

```bash
jupyter notebook
```

ou

```bash
jupyter lab
```

Execute:

```text
notebooks/deteccao_anomalias.ipynb
```

------

## 📊 Exemplo de Fluxo

### 1. Carregamento dos Dados

```python
import pandas as pd

df = pd.read_csv("dados/transacoes.csv")
```

### 2. Normalização

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

dados = scaler.fit_transform(df)
```

### 3. Criação do Modelo

```python
from sklearn.cluster import KMeans

modelo = KMeans(
    n_clusters=3,
    random_state=42
)

modelo.fit(dados)
```

### 4. Identificação de Anomalias

```python
df["cluster"] = modelo.labels_
```

------

## 📈 Resultados Esperados

O projeto permite:

- Detectar transações fora do padrão
- Visualizar agrupamentos de comportamento
- Apoiar investigações de fraude
- Gerar alertas automáticos
- Melhorar processos de auditoria

------

## 🔍 Aplicações Reais

Este tipo de solução pode ser utilizada em:

### Bancos

- Fraudes bancárias
- Movimentações incomuns
- Lavagem de dinheiro

### Fintechs

- Monitoramento em tempo real
- Score de risco

### Empresas

- Auditoria financeira
- Controle de pagamentos
- Detecção de inconsistências

------

## 📚 Conceitos Importantes

### O que é uma Anomalia?

Uma anomalia é uma observação que apresenta comportamento significativamente diferente do restante do conjunto de dados.

Exemplos:

- Compras com valores muito acima da média
- Grande quantidade de transações em curto período
- Movimentações em horários incomuns
- Operações fora do perfil do cliente

------

## 📖 Referências

- Scikit-Learn Documentation
- Pandas Documentation
- NumPy Documentation
- Machine Learning with Python
- Introduction to Anomaly Detection

------

## 👨‍💻 Autor

**Vagner Bellacosa**

Especialista em:

- IBM Mainframe
- COBOL
- CICS
- DB2
- Python para Data Science
- Machine Learning
- Inteligência Artificial

LinkedIn: [www.linkedin.com/in/vagnerbellacosa](http://www.linkedin.com/in/vagnerbellacosa)

GitHub: https://github.com/VagnerBellacosa

------

## ⭐ Apoie o Projeto

Se este conteúdo foi útil para seus estudos:

⭐ Deixe uma estrela no repositório

🍴 Faça um fork

📢 Compartilhe com a comunidade

☕ Continue acompanhando os projetos e conteúdos do **Bellacosa Mainframe & Data Science**.
