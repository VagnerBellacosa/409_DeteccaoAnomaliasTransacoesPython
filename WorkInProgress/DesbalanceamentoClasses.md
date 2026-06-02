# **Desbalanceamento de classes**.



Vamos analisar os dados e tentar solucionar um dos maiores desafios de Machine Learning aplicado a fraudes.

 

O código executado foi algo semelhante a:

```python
df["Class"].value_counts(normalize=True)
```

O parâmetro `normalize=True` faz com que o Pandas retorne proporções em vez de quantidades.

O resultado exibido foi:

| Classe | Proporção |
| ------ | --------- |
| 0      | 0.998273  |
| 1      | 0.001727  |

Convertendo para percentual:

| Classe     | Percentual |
| ---------- | ---------- |
| 0 (Normal) | 99,8273%   |
| 1 (Fraude) | 0,1727%    |

------

## O que isso significa?

Para cada 10.000 transações:

```text
9983 normais
17 fraudulentas
```

Ou seja:

```text
apenas 17 fraudes
```

entre 10 mil operações.

Isso é exatamente o que acontece em bancos reais.

------

## Visualizando de forma simples

Imagine uma urna com 1.000 bolas:

```text
998 bolas azuis = operações normais

2 bolas vermelhas = fraudes
```

Se você tirar uma bola aleatoriamente, quase sempre será azul.

O algoritmo sofre o mesmo problema.

------

## O perigo para o modelo

Imagine um modelo extremamente preguiçoso:

```python
def prever():
    return 0
```

Ou seja:

```text
"Tudo é normal"
```

Para qualquer transação.

------

### Quantos acertos ele teria?

Como 99,83% das operações são normais:

```text
Acurácia ≈ 99,83%
```

Parece excelente.

Mas...

------

### Quantas fraudes detectaria?

```text
ZERO
```

Ele perderia:

```text
492 fraudes
```

da base inteira.

Por isso, em problemas de fraude:

### Acurácia é uma métrica perigosa.

------

## Métricas mais importantes

Em vez de olhar apenas:

```text
Accuracy
```

avaliamos:

### Precision

Das transações marcadas como fraude:

> quantas realmente eram fraude?

------

### Recall

Das fraudes existentes:

> quantas conseguimos encontrar?

------

### F1-Score

Equilíbrio entre Precision e Recall.

------

## Exemplo bancário

Suponha:

```text
100.000 transações
```

Destas:

```text
100 fraudes
```

Modelo A:

```text
99,9% de acurácia
0 fraudes detectadas
```

Modelo B:

```text
98% de acurácia
95 fraudes detectadas
```

Qual é melhor?

### Modelo B

Porque encontrou quase todas as fraudes.

------

# O que vem depois: Feature Engineering

A próxima seção do notebook mostra:

```text
Feature Engineering
```

Aqui normalmente criamos variáveis derivadas para ajudar o algoritmo.

Exemplos:

### Logaritmo do valor

```python
df["LogAmount"] = np.log1p(df["Amount"])
```

------

### Hora da transação

A partir do campo Time:

```python
df["Hour"] = df["Time"] // 3600
```

------

### Normalização

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
```

------

## Curiosidade Mainframe ☕💣

Em sistemas bancários COBOL, esse desbalanceamento também aparece em auditorias.

Imagine um arquivo VSAM com:

```text
100 milhões de transações
```

e apenas:

```text
5 mil suspeitas
```

Isso representa:

```text
0,005%
```

Ou seja, o problema é ainda mais extremo que nesta base de treinamento. É justamente por isso que bancos combinam regras COBOL/CICS tradicionais com modelos de IA e detecção de anomalias para localizar os poucos registros realmente suspeitos escondidos em um enorme volume de operações legítimas.