---
title: Introdução ao Machine Learning com Scikit-Learn e Pandas
author: Diogo G. Bonofre dos Santos
description: Introdução prática à classificação com K-NN, análise exploratória e métricas de avaliação.
---

## Modelo Classificador K-NN (Iris)

### Análise Exploratória de Dados com Pandas

Antes de irmos às vias de fato e treinarmos o modelo com Scikit-Learn, precisamos compreender a estrutura dos dados com os quais estamos lidando e fazer o levantamento das necessidades de tratamento de dados para os métodos computacionais que desejamos utilizar.

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris

# Carrega os dados em um DataFrame Pandas
iris = load_iris(as_frame=True)

# DataFrame completo (variáveis preditoras + variável alvo)
df = iris.frame

# Mapeia a variável alvo para os nomes reais das espécies para facilitar a leitura
df['species'] = df['target'].map(dict(enumerate(iris.target_names)))

# Verifica a tabela de características e rótulos
print(3 * "5 PRIMEIRAS LINHAS ")
print(df.head())

# Informações sobre a estrutura dos dados
print(3 * "INFO ESTRUTURAL ")
print(df.info())

# Auxilia na detecção numérica de valores atípicos (outliers)
print(3 * "ESTATÍSTICAS DESCRITIVAS ")
print(df.describe())

# Pairplot: para visualização da relação cruzada entre todas as variáveis
# e a separabilidade das classes.
sns.pairplot(data=df.drop("target", axis=1), hue="species", diag_kind="kde")
plt.suptitle("Relação entre Variáveis (Pairplot)", y=1.02)

# Boxplot: o melhor para detectar visualmente valores atípicos em cada variável.
plt.figure(figsize=(10, 6))
sns.boxplot(data=df.drop(["target", "species"], axis=1), orient="h", palette="Set2")
plt.title("Distribuição e detecção de valores atípicos")

plt.show()
```

### Implementação do Modelo

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

# Carregamento dos dados
# A matriz `X` contém as características (features), enquanto `y` representa os rótulos de destino.
X, y = load_iris(as_frame=True).data, load_iris(as_frame=True).target

# Divisão entre treino e teste
# Dividiremos o conjunto de dados com 75% para treino e 25% para teste.
# Obs.: Treinar e testar um modelo com os mesmos dados é um erro metodológico (overfitting).
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=18)

# Pré-processamento e transformação
# É fundamental que a transformação aprenda os parâmetros apenas no conjunto de treino.
scaler = StandardScaler().fit(X_train)

X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Seleção do estimador e treinamento do modelo
# Instancia um modelo KNN com 5 vizinhos.
knn = KNeighborsClassifier(n_neighbors=5)

# Treina o modelo usando os dados padronizados.
knn.fit(X_train_scaled, y_train)

# Predição e avaliação
# Realiza a predição para a divisão de teste.
y_pred = knn.predict(X_test_scaled)

# Calcula e imprime métricas
print(f"Acurácia Global: {accuracy_score(y_test, y_pred):.2f}")
print("\nRelatório de Classificação:")
print(classification_report(y_test, y_pred))
print("\nMatriz de Confusão:")
print(confusion_matrix(y_test, y_pred))
```



### Interpretando as Métricas do Modelo

### Notas Metodológicas
- **Overfitting:** Treinar e testar no mesmo conjunto mascara a incapacidade do modelo de lidar com dados inéditos.
- **Escalonamento:** O KNN baseia-se em cálculos de distância (Euclidiana por padrão). Se uma característica tiver uma escala muito maior que as outras, ela dominará o cálculo injustamente.

### Exercícios Propostos
1. Pesquise e explique a diferença entre o `StandardScaler`, `MinMaxScaler` e `RobustScaler`.
2. Explique, com suas palavras, a diferença conceitual entre os métodos `.fit()`, `.transform()` e `.predict()`.
3. O que acontece com a fronteira de decisão se alterarmos o valor de `n_neighbors` para 1 ou para 50?

---

## Modelo de Regressão K-NN (California Housing)

## Referências
- [Scikit-Learn Documentation](https://scikit-learn.org/stable/)
- [Pandas Documentation](https://pandas.pydata.org/)
