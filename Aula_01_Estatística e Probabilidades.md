# 2. Estatística aplicada para AIs

Fornece as técnicas para algoritmos identificarem padrões, como regressão linear, regressão logística e algoritmos de agrupamento.

a) **Medidas de Tendência Central:** Média, Mediana e Moda (Foco em: Tratamento de dados ausentes e preenchimento de lacunas).
b) **Medidas de Dispersão:** Variância e Desvio Padrão (Foco em: Entender o espalhamento dos dados e base para a Normalização).
c) **Análise de Correlação:** Coeficiente de Pearson (Foco em: Identificar quais variáveis realmente impactam o modelo e eliminar dados redundantes).
d) **Inferência Estatística e Amostragem:** População vs. Amostra (Foco em: Como o modelo generaliza o que aprendeu no treino para o mundo real).
e) **Distribuições de Probabilidade:** Distribuição Normal/Gaussiana e Softmax (Foco em: Inicialização de pesos e saída final de classificação).
f) **Métricas de Erro e Performance:** Erro Médio Quadrático (MSE), Erro Absoluto (MAE) e Acurácia (Foco em: Medir o sucesso do treinamento).

## 2.1. Medidas de Tendência Central

### 2.1.1. Média

É a soma de todos os valores pertencentes a um conjunto de dados e dividindo o resultado pela quantidade de elementos. Para as AIs, é uma ferramenta de equilíbrio.

**Aplicação:**

* **Tratamento de Dados Faltantes:** Quando uma base de dados tem buracos (ex: idades faltando em um cadastro), usamos a média do grupo para preencher esses vazios sem alterar o comportamento geral do conjunto.
* **Normalização:** Para que um neurônio não dê importância demais a um número grande (ex: Salário) e ignore um pequeno (ex: Idade), usamos a média para centralizar todos os dados em torno de zero.
* **Formula:**

$$\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}$$

* **$\bar{x}$ (O "x" com barra):** É o resultado final, a nossa Média. No exemplo, é o valor 5.
* **$\sum$ (Sigma Maiúsculo):** Esse símbolo bonitão é apenas uma ordem de comando. Ele diz: "Some tudo o que vem depois de mim".
* **$x_i$ (O elemento):** Representa cada número individual da sua lista (o 2, o 4, o 6 e o 8). O "i" é como um índice (1º número, 2º número...).
* **$n$ (O divisor):** É a quantidade total de itens que você tem. No nosso caso, como temos quatro números (2, 4, 6, 8), o $n = 4$

**Exemplo:**

Imagine que temos os erros de 4 predições de uma IA: 2, 4, 6 e 8.

1) Identificamos os dados ($x_i$): x1=2, x2=4, x3=6 e x4=8
2) Contamos quantos são (n): São 4 números.
3) Executamos o Sigma ($\sum$) 2 + 4 + 6 + 8 = 20.
4) Finalizamos a fórmula ($\bar{x}$): 20 / 4 = 5

**Fixação:**

a) Uma rede neural processou 5 imagens. O tempo de processamento de cada uma foi: 10ms, 12ms, 15ms, 13ms e 10ms. Qual o tempo médio de processamento por imagem?

b) Em uma tabela de "Idade de Clientes", você encontrou 4 registros: 20, 30, 40 e 50 anos. No 5º registro, o dado está faltando. Se decidirmos preencher esse dado faltante com a média dos outros quatro, qual valor será inserido?

### 2.1.2. Mediana

Diferente da média, a Mediana é o valor central que divide seus dados ao meio. Na Engenharia de IA, ela é o nosso "filtro de ruído". Para achar a Mediana (Md), primeiro precisamos ordenar os dados (o Rol). O cálculo também depende se o número de elementos (n) do conjunto é par ou ímpar.

**Aplicação:**

* **Resistência a Outliers (Valores Discrepantes):** Imagine que você treina uma IA com salários. Se houver um bilionário na lista, a Média vai lá para o alto e engana o modelo. A Mediana ignora esse valor extremo e foca no que é comum.
* **Limpeza de Dados Sujos:** Quando os sensores (como câmeras ou termômetros) falham e geram um número absurdo (ex: um sensor de temperatura marcando 500°C por erro técnico), usamos a Mediana para ignorar esse erro e manter o treinamento estável.
* **Formula:**

1) Se for **par**: A mediana é a média dos dois valores centrais.

$$Md = \frac{x(\frac{n}{2}) + x(\frac{n}{2} + 1)}{2}$$

2) Se for **ímpar**: A mediana é a posição central.

$$Posição = \frac{n + 1}{2}$$

(Obs.: Considerando um conjunto com quantidade par de elementos “n”)

* **$x(n/2)$:** É o valor que está na posição da "primeira metade"
* **$x(n/2 + 1)$:** É o valor que está na posição imediatamente seguinte ("segunda metade").

**Exemplo:**

Imagine os tempos de resposta de uma IA em segundos: 1.2, 0.5, 30.0, 0.8, 1.0 .

* Criar o Rol (Ordenar): 0.5, 0.8, 1.0, 1.2, 30.0
* Contar os itens (n): Temos 5 itens (Ímpar)
* Aplicar a posição: (5+1) / 2 = 3ª posição
* Identificar o valor: O 3º item é o 1.0

**Nota:** Repare que o valor 30.0 (muito alto) não afetou a Mediana, mas destruiria a Média.

**Fixação:**

a) Uma rede neural classificou 7 imagens com as seguintes confianças (0 a 100): 85, 90, 70, 95, 60, 100, 80. Qual a Mediana de confiança desse lote? (Dica: coloque em ordem primeiro!).

b) Analisando o uso de memória de 6 servidores: 4GB, 8GB, 2GB, 16GB, 4GB, 32GB. Qual é a Mediana de consumo de memória deste cluster?

### 2.1.3. Moda

Ao monitorar os erros de um modelo por uma hora e obteve os seguintes códigos de erro: 404, 500, 404, 403, 500, 404, 502. É simplesmente o valor que mais se repete em um conjunto de dados. Na IA, ela é a nossa ferramenta para Dados Categóricos (textos, classes, etiquetas).

**Aplicação:**

* **Preenchimento de Categorias (Imputação de Classes):** Se você tem uma base de dados de "Tipos de Veículos" e em alguns registros a coluna está vazia, você não pode tirar a "média" entre um Carro e uma Moto. Você usa a Moda (o tipo que mais aparece, ex: "Sedan") para preencher o vazio.
* **Voto Majoritário (Ensemble Learning):** Em sistemas de IA avançados, onde várias redes neurais "votam" no que viram em uma imagem, o resultado final escolhido é a Moda das respostas. Se 3 IAs dizem "Gato" e 1 diz "Cachorro", a resposta final é a Moda: "Gato".
* **Formula:** A Moda não possui uma fórmula algébrica complexa como a média. Ela é definida pela frequência.

**Mo = Valor com maior frequência absoluta (fi)**

* **fi:** É a contagem de quantas vezes cada item aparece.
* **Amodal:** Quando nenhum valor se repete.
* **Bimodal:** Quando dois valores diferentes empatam no topo da repetição.

**Exemplo:**

Imagine as etiquetas de saída de um classificador de objetos em um vídeo: [Pessoa, Carro, Pessoa, Árvore, Pessoa, Carro]

1.  **Contagem (fi):**
    * Pessoa: 3 vezes
    * Carro: 2 vezes
    * Árvore: 1 vez
2.  **Identificar a maior frequência:** O valor “pessoa” aparece mais.
3.  **Resultado:** Mo = Pessoa

**Fixação:**

a) Uma base de dados de sensores de temperatura registrou: 22°C, 25°C, 22°C, 28°C, 22°C, 30°C. Qual é a temperatura modal desse sensor?

b) Monitorando os erros de um modelo por uma hora e obteve os seguintes códigos de erro: 404, 500, 404, 403, 500, 404, 502.

1) Qual é a Moda desses erros?
2) Se você fosse o engenheiro, em qual erro focaria primeiro baseado apenas na estatística?

## 2.2. Medidas de Dispersão: Variância e Desvio Padrão

Se a Média diz onde os dados estão "amontoados", a Dispersão diz o quão espalhados eles estão. Na IA, isso é o que separa um modelo estável de um modelo que chuta valores aleatórios.

### 2.2.1. Variância

A Variância mede a distância média de cada dado em relação à média do conjunto.

**Aplicação:**

* **Na Engenharia de IA:** Ela indica a Instabilidade. Se a variância do erro da sua IA é alta, significa que ela acerta muito em alguns casos e erra feio em outros. Queremos uma variância baixa e controlada.
* **Variância Populacional ($\sigma^2$):**

É aplicada quando tem todos os dados possíveis do universo que se está estudando.
* **Exemplo:** Você quer a variância da idade de todos os funcionários da sua empresa (e você tem a lista completa de todos os 50 funcionários).
* **Divisor:** Você divide pelo número total de itens (n).
* **Formula:**

$$\sigma^2 = \frac{\sum (x_i - \mu)^2}{n}$$

Ordem discriminada para o cálculo da Variância populacional (geral):

* **$\mu$**: calcular a média;
* **$x_i$**: dado individual do conjunto;
* **$\sum$**: Representa do somatório total dos desvios individuais somados após serem elevados ao quadrado. Aqui calcula-se cada desvio – diferença do dado menos a média, eleva-se ao quadrado e soma-se os resultados;
* **“n”**: total de elemento do conjunto
* **$\sigma^2$**: é o resultado do somatório ( $\sum$ ) dividido pelo número total de elementos (n), resultando na variância.

**Fixação:**

Lembrete: Use esta quando você tem o conjunto total de dados.

a) Um pequeno modelo de IA processou apenas 4 requisições. Os erros de tempo (em ms) foram: 2, 4, 6 e 8.
1. Calcule a média ($\mu$).
2. Calcule a Variância Populacional ($\sigma^2$). (Dica: Como são apenas esses 4 dados no universo do teste, use o divisor n=4).

b) Um rack de servidores possui exatamente 5 sensores de temperatura. Em um momento crítico, as leituras foram: 30°C, 32°C, 30°C, 35°C e 33°C.
1. Encontre a média das temperaturas.
2. Calcule a Variância Populacional para entender o quão instável está o resfriamento desse rack específico.

* **Variância Amostral ($s^2$):**

É aplicada quando tem todos os dados possíveis do universo que se está estudando.
* **Exemplo:** Você quer saber a variância do tempo de resposta de uma IA no mundo, mas você só testou 100 vezes no seu computador.
* **Divisor:** Você divide pelo número total de itens (n-1).
* **Formula:**

$$s^2 = \frac{\sum (x_i - \bar{x})^2}{n - 1}$$

Ordem discriminada para o cálculo da Variância Amostral:
* **$\bar{x}$**: calcular a média;
* **$x_i$**: dado individual do conjunto;
* **$\sum$**: Representa do somatório total dos desvios individuais somados após serem elevados ao quadrado. Aqui se calcula cada desvio – diferença do dado menos a média, eleva-se ao quadrado e soma-se todos os resultados;
* **“n - 1”**: total de elemento do conjunto – 1.
* **$s^2$**: é o resultado do somatório ( $\sum$ ) dividido pelo número total de elementos (n – 1) resultando na variância amostral.

**Fixação:**

Lembrete: Use esta quando os dados são apenas uma parte (amostra) de um todo maior (IA em produção).

a) É extraído uma amostra aleatória de 3 logs de erro de um modelo que roda milhões de vezes por dia. Os valores foram: 1, 3 e 5.
1. Calcule a média.
2. Calcule a Variância Amostral ($s^2$). (Dica: Como é uma amostra, o divisor deve ser n-1, ou seja, 3-1 = 2).

b) Para testar a qualidade de um novo Dataset, um engenheiro separou uma amostra de 6 imagens e mediu o tempo de classificação (em segundos): 0.5, 0.7, 0.5, 0.8, 0.6 e 0.5.
1. Determine a Média.
2. Calcule a Variância Amostral ($s^2$).
3. Explique por que, neste caso, dividir por n-1 é mais seguro para a Engenharia de IA do que dividir apenas por n.
### 2.2.2. Desvio Padrão

É a distância média (grau de dispersão) que os seus dados estão em relação à média do grupo ($\bar{x}$). Ele funciona como uma "Régua de Erro".

* **Desvio Padrão Baixo:** Significa que os dados estão "comportados" e muito próximos da média. (Ex: Uma linha de produção muito precisa).
* **Desvio Padrão Alto:** Significa que os dados estão "espalhados" e longe da média. (Ex: Um processo instável ou imprevisível).

* **Formula:**

$$s = \sqrt{\frac{\sum (x_i - \bar{x})^2}{n - 1}}$$

* **$\bar{x}$**: calcular a média;
* **$x_i$**: dado individual do conjunto;
* **$\sum$**: Representa do somatório total dos desvios individuais somados após serem elevados ao quadrado .
Aqui se calcula cada desvio – diferença do dado menos a média, eleva-se ao quadrado e soma-se todos os resultados;
* **“n - 1”**: total de elemento do conjunto – 1.
* **$s$**: Desvio Padrão Amostral (resultado)

* **Exemplo:**
Imagine que o tempo de processamento de três tarefas na IA foi de 2s, 4s e 6s.

1. Média ($\bar{x}$): 4s.
2. Variância ($s^2$): 4s²
3. Desvio Padrão (s): $s = \sqrt{4} = 2s$

Interpretação: O tempo médio é 4 segundos, com uma variação padrão de 2 segundos para cima ou para baixo.

* **Fixação:**

a) Um sensor de temperatura em um servidor registrou três leituras em uma hora: 20°C, 24°C e 28°C. Sabendo que a variância dessas leituras é 16, calcule o Desvio Padrão desse sensor.

b) Monitorando o erro de predição de uma IA em 5 testes. Os valores encontrados foram: 2, 3, 5, 7 e 8. Calcule a média, a variância amostral e, por fim, o Desvio Padrão desse conjunto de erros.

Atividades de fixação no forms:
https://docs.google.com/forms/d/1fuu8Nj6tjhI7dprVhwpOWmuiKDpJw6YR23imXMwdFtQ/edit

Gabarito no forms:
https://docs.google.com/forms/d/1F9BbDz_2nZTWhNvI7Gk7fSEAAKwGE-N6vOCD5_8imqE/edit

## 2.3. Análise de Correlação: Coeficiente de Pearson (r).

É a ferramenta estatística que mede o grau de parentesco ou dependência entre duas variáveis. Ela nos diz, numericamente, se quando uma coisa muda, a outra muda junto.

**Aplicação:**

● Identificar Variáveis de Impacto: Serve para descobrir quais dados realmente têm peso no seu estudo. Por exemplo, medir se o "Tempo de Estudo" tem relação direta com a "Nota da Prova".

● Limpeza de Dados (Filtro): Na estatística, usamos o Pearson para eliminar dados redundantes. Se duas colunas dizem a mesma coisa (ex: "Idade em Anos" e "Ano de Nascimento"), o coeficiente será 1. Você identifica isso e remove uma delas para simplificar sua base.

**A Lógica da Dispersão (A Força da Relação):**

● O Número 1 ou -1 (Dispersão Zero): Os pontos estão perfeitamente alinhados, formando uma linha reta. Não há "bagunça". Isso indica uma conexão perfeita. Se você conhece um dado, você prevê o outro com 100% de precisão.

● Números Próximos de 0 (Dispersão Total): Os pontos estão espalhados como uma nuvem de fumaça, sem direção. Isso indica que não há conexão (independência). Um dado não ajuda em nada a prever o outro.

● **Representação gráfica**

![](introducao-a-redes-neurais/Imagens_Formulas/formula_08.png)


**Fórmula:**

$$r = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum (x_i - \bar{x})^2 \cdot \sum (y_i - \bar{y})^2}}$$

Onde:

● **$\bar{x}$**: calcular a média;
● **$x_i$**: dado individual do conjunto;
● **$\bar{y}$**: calcular a média;
● **$y_i$**: dado individual do conjunto;
● **$\sum$ (numerador):** Representa o somatório do produto entre os desvios de “x” e de “y”.
● **$\sum$ (denominador):** Representa do somatório total dos desvios somados após serem elevados ao quadrado $(x_i - \bar{x})^2$ e de $(y_i - \bar{y})^2$.

**A Lógica Final:**

● O Topo da fórmula usa a multiplicação simples para descobrir a direção (se é + ou -).
● A Base da fórmula usa os quadrados (como no Desvio Padrão) para medir o tamanho total da variação de cada um.

**Exemplo:**

Analisando um grupo de três alunos em uma prova de 10 questões, com o objetivo de verificar a correlação entre o tempo de estudo e o número de erros cometidos. O estudo registrou que o Aluno A estudou 1 hora e teve 9 erros; o Aluno B estudou 5 horas e teve 5 erros; e o Aluno C estudou 9 horas e teve apenas 1 erro. Ao aplicarmos a fórmula do Coeficiente de Pearson ($r$) a esses dados, foi possível gerar a seguinte representação gráfica:

![](introducao-a-redes-neurais/Imagens_Formulas/formula_10.png)

● **Interpretação:**

Como se pode observar no gráfico, ao calcularmos o coeficiente de Pearson para esse estudo estatístico, o resultado foi r = -1.0. Isso significa que, para esse grupo específico, a relação entre as horas de estudo e o número de erros é perfeitamente conectada e inversamente proporcional (ou seja, quando um dado aumenta, o outro diminui na mesma proporção). Em outras palavras, estatisticamente, o tempo dedicado ao estudo explica 100% da variação no número de erros obtidos, sem qualquer influência de "sorte" ou "chute" (dispersão zero).

**Fixação:**

a) Imagine que você está analisando a correlação entre "Quantidade de Chuva" e "Venda de Guarda-chuvas". Ao plotar o gráfico, você observa que os pontos estão muito próximos uns dos outros, formando uma linha que sobe da esquerda para a direita.

1. O valor de r será mais próximo de +0.90 ou de -0.90?
2. Como você descreve a dispersão desses dados?

b) Um pesquisador calculou o Coeficiente de Pearson entre o "Peso de um Carro" e a "Eficiência de Combustível (km/l)" e obteve um resultado de r = - 0.95.

1. O que o sinal negativo indica sobre a relação entre o peso e a eficiência?
2. O que o valor 0.95 (próximo de 1) diz sobre a dispersão dos pontos no gráfico e a confiança para prever a eficiência baseando-se no peso?

## 2.4. Inferência Estatística e Amostragem: População vs. Amostra

### 2.4.1. Inferência Estatística

É o processo de tirar conclusões sobre uma população inteira com base em dados coletados de apenas uma parte dela — a amostra. Em vez de analisar todos os dados existentes (o que seria impossível na maioria dos casos), usamos técnicas matemáticas para estimar, com certo grau de confiança, como a população se comporta.

Pense assim: imagine que uma IA precisa aprender o padrão de comportamento de todos os usuários de um aplicativo. São milhões de pessoas. Analisar cada uma delas é inviável. A inferência estatística permite que a IA aprenda a partir de uma amostra representativa e generalize esse aprendizado para todos.

**Aplicação:**

● **Estimação de parâmetros:** Em IA, quando treinamos um modelo de aprendizado de máquina, estamos essencialmente estimando parâmetros (pesos, coeficientes) que descrevem o comportamento do dado como um todo. Cada vez que o modelo é alimentado com um lote de dados (mini-batch), ele está fazendo uma inferência sobre o padrão geral a partir daquela amostra.

● **Teste de hipóteses:** Quando uma equipe de IA quer saber se um novo modelo é realmente melhor que o anterior, ela aplica um teste de hipóteses estatístico. A hipótese nula (H₀) afirma que não há diferença entre os modelos; a hipótese alternativa (H₁) afirma que há. Os dados coletados nos testes determinam qual hipótese é sustentada — e essa decisão é baseada em inferência.

**Fórmula:** a inferência é calculada por base no intervalo de confiança

$$IC = \bar{x} \pm z \cdot \frac{\sigma}{\sqrt{n}}$$

**Onde:**
IC = Intervalo de confiança — a faixa de valores onde o parâmetro real provavelmente está
x̄ = Média amostral — a média calculada a partir da amostra coletada
z = Valor crítico da distribuição normal (ex.: z = 1,96 para 95% de confiança – tabela padrão)
σ = Desvio padrão da população (ou da amostra, quando o da população é desconhecido)
n = Tamanho da amostra — quantos dados foram usados

### 2.4.2. Amostragem Infinita

É o processo de selecionar um subconjunto de dados de uma população maior para estudo. É o passo que vem antes da inferência: primeiro você coleta a amostra, depois você infere sobre a população.
A qualidade da inferência depende diretamente da qualidade da amostragem. Uma amostra ruim gera conclusões erradas — por mais sofisticada que seja a matemática aplicada depois.

**Aplicação:**

**Amostragem aleatória simples:** Cada elemento da população tem a mesma chance de ser selecionado. Em IA, quando dividimos um conjunto de dados em treino e teste de forma aleatória, estamos aplicando esse princípio.

**Amostragem estratificada:** A população é dividida em grupos (estratos) e amostras são coletadas de cada grupo proporcionalmente. Em modelos de IA para detecção de fraudes, por exemplo, como fraudes são raras, usa-se amostragem estratificada para garantir que o modelo veja exemplos suficientes de fraude durante o treinamento.

**Formula: Tamanho Amostral Mínimo**

$$n = \frac{z^2 \cdot p \cdot (1-p)}{e^2}$$

**Onde:**
n = Tamanho mínimo necessário da amostra
z = Valor crítico correspondente ao nível de confiança desejado
p = Proporção estimada do fenômeno na população (quando desconhecida, usa-se 0,5 como valor mais conservador).

**Dica:** Caso não se tenha ideia de qual é essa proporção, deve-se usar 0,5 (50%). Isso porque 0,5 é o valor que exige o maior tamanho de amostra possível, garantindo que a pesquisa seja segura (é o chamado "valor conservador").

e = Margem de erro aceitável (ex.: 0,05 para 5%)

**Exemplo:**

Uma empresa de streaming quer saber se seu novo algoritmo de recomendação agrada mais aos usuários. Em vez de testar com todos os 10 milhões de usuários, ela seleciona aleatoriamente 1.000 usuários (amostragem). Após o teste, a média de satisfação da amostra é 8,2 (em uma escala de 0 a 10), com desvio padrão de 1,5. Aplicando inferência estatística, a equipe calcula que, com 95% de confiança, a satisfação real de todos os usuários está entre 7,9 e 8,5. Essa faixa é o intervalo de confiança, e permite que a empresa tome uma decisão sem precisar testar com todos os usuários.

**Dados:**
n = 1.000
z = 1,96 ( valor retirado da Tabela de Confiança Z para 95%)
p (substituindo o p da fórmula por ser média) = 1,5
e = 0,3 (para chegar no valor subtrai-se da média 8,2 )
Limite Superior: 8,5 - 8,2 = 0,3
Limite Inferior: 8,2 - 7,9 = 0,3
N = 10.000.000

**Diagrama mostrando a relação entre população, amostragem e inferência:**

![](introducao-a-redes-neurais/Imagens_Formulas/formula_13.png)

**Fixação:**

a) Uma IA de detecção de spam foi testada em uma amostra de 400 e-mails. O modelo acertou 92% dos casos. Com z = 1,96 e margem de erro de 3%, qual intervalo de confiança podemos afirmar para a taxa de acerto real do modelo em toda a base de e-mails? (Dica: use a fórmula $IC = p \pm z \cdot \sqrt{\frac{p(1-p)}{n}}$)

b) Uma equipe de IA quer estimar a proporção de usuários que clicam em anúncios em uma plataforma. Eles não sabem essa proporção de antemão. Desejam uma margem de erro de 4% com 95% de confiança (z = 1,96). Qual é o tamanho mínimo de amostra necessário? Interprete o resultado: o que aconteceria com esse tamanho se a margem de erro fosse reduzida para 2%?

## 2.5. Distribuições de Probabilidade: Distribuição Normal/Gaussiana e Softmax (Foco).

Uma distribuição de probabilidades define como os valores são espalhados em um intervalo. Na prática da IA, ela atua em dois momentos cruciais:

1. **Inicialização de Pesos:** É usada para definir os valores iniciais das conexões da rede neural. Uma distribuição (geralmente Normal) garante que os pesos não comecem nem zerados, nem extremos, permitindo que o aprendizado comece de forma equilibrada.
2. **Saída de Classificação:** É o resultado final do modelo. A IA não diz "é um gato"; ela gera uma distribuição de probabilidades onde cada categoria recebe uma nota (ex: Gato 92%, Cachorro 8%). A categoria com a maior probabilidade é a escolhida.

### 2.5.1. Distribuição Normal (Gaussiana)

A distribuição normal é a distribuição mais importante da estatística. Ela descreve fenômenos onde os valores se concentram em torno de uma média e se afastam dela de forma simétrica — quanto mais longe da média, menos provável. Seu gráfico tem o famoso formato de "sino".

**Aplicação:**

● **Em redes neurais:** Os pesos iniciais de uma rede neural são frequentemente inicializados seguindo uma distribuição normal. Isso ajuda o aprendizado a começar de forma equilibrada, sem valores extremos que poderiam travar o treinamento.

● **Em normalização de dados:** Antes de alimentar dados a uma IA, é comum transformá-los para que tenham distribuição próxima da normal (média zero e desvio padrão um). Isso melhora a eficiência do aprendizado

**Fórmula:**

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}$$

**Onde:**
f(x) = Densidade de probabilidade no ponto x — a "altura" da curva naquele ponto
μ (mu) = Média da distribuição — o centro da curva, o valor mais provável
σ (sigma) = Desvio padrão — controla o "espalhamento" da curva; quanto maior, mais achatada
π = Pi ≈ 3,14159
e = Base do logaritmo natural ≈ 2,71828

**Exemplo:**

Em um modelo de IA de reconhecimento de voz, os erros de predição da probabilidade de cada fonema seguem uma distribuição normal. Conhecer essa distribuição permite ao engenheiro identificar quando o modelo está sistematicamente errando (a média se deslocou) ou quando erros extremos estão ocorrendo com mais frequência do que deveriam (as caudas estão pesadas demais)

### 2.5.2. Distribuição Binomial

A distribuição binomial descreve o número de sucessos em uma série de tentativas independentes, onde cada tentativa tem apenas dois resultados possíveis (sucesso ou fracasso) e a probabilidade de sucesso é constante.

**Aplicação:**

Em classificadores binários: Quando uma IA decide se um e-mail é spam (1) ou não (0), cada decisão é uma tentativa binomial. Analisar o resultado de 1.000 classificações seguindo a distribuição binomial permite calcular a probabilidade de o modelo errar acima de um certo número de vezes.

Em testes A/B de IA: Quando se compara se usuários clicam ou não em uma recomendação feita pela IA (clicou = sucesso, não clicou = fracasso), o total de cliques em n tentativas segue uma distribuição binomial.

**Fórmula:**

$$P(X = k) = \binom{n}{k} \cdot p^k \cdot (1-p)^{n-k}$$

**Onde:**
P(X = k) = Probabilidade de obter exatamente k sucessos
n = Número total de tentativas
k = Número de sucessos desejados
p = Probabilidade de sucesso em cada tentativa individual
(1-p) = Probabilidade de fracasso em cada tentativa
C(n,k) = Combinação de n elementos tomados k a k — o número de formas possíveis de obter k sucessos em n tentativas

**Exemplo:**

Um modelo de IA detecta tumores em radiografias com 90% de precisão por imagem (p = 0,9). Se analisarmos 10 imagens, qual a probabilidade de o modelo acertar exatamente 9? Aplicando a fórmula com n=10, k=9, p=0,9, obtemos aproximadamente 38,7%. Em IA médica, essa análise é crítica para entender o comportamento do modelo em lotes de diagnósticos.

### 2.5.3. Distribuição Poisson

A distribuição de Poisson descreve o número de eventos que ocorrem em um intervalo fixo de tempo ou espaço, quando esses eventos acontecem de forma independente e a uma taxa média constante.

**Aplicação:**

● **Em monitoramento de sistemas de IA:** O número de falhas ou erros que um sistema de IA comete por hora, o número de requisições maliciosas que chegam a um servidor por minuto, ou o número de anomalias detectadas por turno seguem distribuição de Poisson.

● **Em modelos de linguagem:** A distribuição de Poisson é usada para modelar a frequência de palavras raras em grandes textos — base dos modelos de linguagem que alimentam as IAs de texto.

**Fórmula:**

$$P(X = k) = \frac{e^{-\lambda} \cdot \lambda^k}{k!}$$

**Onde:**
P(X = k) = Probabilidade de ocorrer exatamente k eventos
λ (lambda) = Taxa média de ocorrências no intervalo (média esperada de eventos)
e = Base do logaritmo natural ≈ 2,71828
k = Número de eventos que queremos calcular a probabilidade
k! = Fatorial de k (ex.: 4! = 4×3×2×1 = 24)

**Exemplo:**

Um sistema de IA que monitora redes sociais detecta em média 3 posts ofensivos por hora (λ = 3). Qual a probabilidade de detectar exatamente 5 posts ofensivos em uma determinada hora? Aplicando a fórmula: P(5) = (e⁻³ × 3⁵) / 5! ≈ 10,1%. Esse resultado ajuda a equipe a calibrar os alertas do sistema.

![](introducao-a-redes-neurais/Imagens_Formulas/formula_17.png)

**Fixação:**

a) Um modelo de IA classifica imagens de defeitos em uma linha de produção. A taxa de detecção correta é de 80% por imagem (p = 0,8). Em um lote de 5 imagens, qual é a probabilidade de o modelo acertar exatamente 4? Use a fórmula binomial.

b) Um chatbot de atendimento ao cliente recebe em média 4 reclamações por hora que ele não consegue resolver (λ = 4). Usando a distribuição de Poisson, calcule a probabilidade de ocorrerem exatamente 0, 2 e 6 reclamações não resolvidas em uma hora. Com base nos resultados, interprete: o sistema está operando dentro de um comportamento esperado se, em determinada hora, chegarem 10 reclamações não resolvidas?

### 2.5.1. Distribuição Softmax:

Ou Função Softmax é uma função matemática utilizada em aprendizado de máquina e redes neurais para converter um vetor de números reais brutos (chamados de logits) em uma distribuição de probabilidade. Ela é fundamental em problemas de classificação multiclasse, onde cada saída representa a probabilidade de uma entrada pertencer a uma classe específica

**Aplicação:**

● **Classificação Multiclasse:** Decidir se um objeto em uma imagem é um carro, uma moto ou um caminhão.

● **Redes Neurais:** É a camada final que traduz o "processamento interno" da máquina em uma resposta que o ser humano entende (porcentagem).

**Fórmula:**

● A Softmax utiliza o número de Euler (e ≈ 2.718) para garantir que nenhum valor seja negativo e para destacar as maiores diferenças.

$$S(x_i) = \frac{e^{x_i}}{\sum_{j=1}^{n} e^{x_j}}$$

**Onde:**
S(xi): resultado da probabilidade de saída (de 0 a 1)
Xi: classe específica a ser avaliada
Xj: são as entradas (inputs)
∑: soma de todos os valores de entrada

**Exemplo:**

Um sistema de IA analisa uma biópsia e gera "pesos" para três possíveis diagnósticos: Saudável (8.0), Inflamação (4.0) e Tumor (1.0). Como esses números sozinhos não dizem muito ao médico, aplicamos a Distribuição Softmax para converter esses pesos em probabilidades claras.

**Interpretação:** Neste caso, a Softmax transformou os pesos brutos em probabilidades: Saudável (98,1%), Inflamação (1,8%) e Tumor (0,1%). Note que a soma total fecha em 100%. A lógica aqui é dar clareza ao diagnóstico: a IA não está apenas "chutando" que está saudável, ela está mostrando que, estatisticamente, a probabilidade é esmagadora em relação às outras opções.

**Fixação:**

a) **Nível Fácil:** Uma rede neural entrega os seguintes valores após a Softmax: Classe A (0.70), Classe B (0.20) e Classe C (0.10).

1. Qual a probabilidade de a entrada pertencer à Classe A?
2. Se somarmos as três classes, qual deve ser o resultado obrigatório?

b) **Nível Médio:** Em um problema de classificação, a Softmax transformou os pesos (logits) em 0.95 para "Gato" e 0.05 para "Cão".

1. O que o valor 0.95 indica sobre a confiança da IA na decisão?
2. Por que é mais útil para um usuário ver "95%" do que ver um número bruto como "12.4"?

## 2.6. Métricas de Erro e Performance: Erro Médio Quadrático (MSE), Erro Absoluto (MAE) e Acurácia

Métricas de erro são medidas numéricas que quantificam o quanto as previsões de um modelo de IA se afastam dos valores reais. Elas são a linguagem que usamos para responder à pergunta mais básica da IA: "o modelo está indo bem ou mal?". Sem métricas bem escolhidas, é impossível saber se um modelo está aprendendo, se melhorou com um ajuste, ou se está pronto para uso real.
É importante entender que não existe "a métrica perfeita" — cada problema exige a métrica mais adequada. Usar a métrica errada pode levar a decisões equivocadas sobre um modelo aparentemente bom que na prática falha gravemente.

**Relação com a Performance:**

Performance de um modelo é a avaliação geral de seu comportamento em dados que ele nunca viu antes (dados de teste). As métricas de erro são os instrumentos dessa avaliação. Uma boa performance não significa zero erro — significa que os erros estão dentro de um nível aceitável para o problema em questão e que o modelo generaliza bem, ou seja, não apenas "decorou" os dados de treino (overfitting), mas aprendeu padrões reais.

### 2.6.1. Erro Absoluto:

Mede a média das diferenças absolutas entre os valores previstos e os valores reais. É a métrica mais intuitiva: "em média, quanto o modelo erra?"

**Aplicação:**

Em IAs de previsão de preços: Um modelo que prevê o preço de ações ou imóveis usa MAE para medir o erro médio em reais ou dólares — fácil de interpretar por qualquer pessoa, incluindo gestores não técnicos.

Em sistemas de recomendação: O MAE mede o quanto as notas previstas por um motor de recomendação diferem das notas reais que os usuários deram.

**Fórmula:**

$$MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|$$

**Onde:**
MAE = Erro Médio Absoluto
n = Número total de exemplos avaliados
yᵢ = Valor real do i-ésimo exemplo
ŷᵢ (y-chapéu) = Valor previsto pelo modelo para o i-ésimo exemplo
|yᵢ - ŷᵢ| = Valor absoluto da diferença (sem sinal negativo)

**Exemplo:**

Um sistema de logística prevê o tempo de entrega de mercadorias.

● Entrega 1: Real: 10 min | Previsto: 12 min (Erro: 2)
● Entrega 2: Real: 20 min | Previsto: 15 min (Erro: 5)
● Entrega 3: Real: 15 min | Previsto: 15 min (Erro: 0)

**Interpretação:**

Somamos os erros absolutos (2 + 5 + 0 = 7) e dividimos pelo total de entregas (3). O resultado é um MAE de 2,33 minutos. Isso significa que, em média, as previsões do sistema erram por cerca de 2 minutos e 20 segundos, seja para mais ou para menos. Diferente do MSE, aqui um erro grande não é "punido" com o quadrado; todos os erros têm o mesmo peso na média.

**Fixação:**

a) Um aplicativo de clima previu a temperatura para dois dias. No primeiro dia, errou por 4°C. No segundo, errou por 2°C. Qual o Erro Médio Absoluto (MAE) dessas duas previsões?

b) Por que em um sistema de controle de estoque de medicamentos de alto custo, o gestor pode preferir analisar o MSE em vez do MAE para avaliar os erros de previsão?

### 2.6.2.1. Erro Quadrático Médio (Mean Squared Error):

O MSE mede a média dos erros elevados ao quadrado. Sua principal característica é "punir" severamente os erros grandes: quanto maior o erro, muito maior será o valor do MSE.

**Aplicação:**

● **Ajuste de Modelos de IA:** É a métrica padrão para treinar algoritmos. Ele força o modelo a evitar erros grandes, pois o quadrado transforma um erro de "2" em "4", mas um erro de "10" em "100".

**Fórmula MSE:**

$$MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

**Onde:**
MSE = Erro Quadrático Médio
n = Número total de exemplos avaliados
yᵢ = Valor real do i-ésimo exemplo
ŷᵢ (y-chapéu) = Valor previsto pelo modelo para o i-ésimo exemplo
(yᵢ - ŷᵢ)² = Quadrado da diferença entre valor real e previsto (sem sinal negativo)
∑: somatório de todos os erros quadrados

● **Lógica de interpretação:**

Imagine que você está atirando em um alvo. Se você erra por 1 cm, o erro é pequeno. Se erra por 10 cm, o MSE entende que você não errou apenas 10 vezes mais, mas sim 100 vezes mais. Ele serve para mostrar que erros grandes são inaceitáveis.

### 2.6.2.2. Raiz do Erro Quadrático Médio (Root Mean Squared Error):

O RMSE é simplesmente a raiz quadrada do MSE. Ele é criado para trazer o erro de volta para a unidade original dos dados (metros, reais, quilos), facilitando a interpretação humana.

**Aplicação:**

● **Comunicação de Resultados:** Enquanto o computador usa o MSE para aprender, o ser humano usa o RMSE para entender o erro na prática. Se você está prevendo preços em Reais (R$), o MSE dará um resultado em "Reais ao quadrado" (o que não faz sentido), enquanto o RMSE dará o erro em Reais.

**Fórmula RMSE:**

$$RMSE = \sqrt{MSE}$$

● **Lógica de interpretação:**

Se o MSE é a "punição" matemática, o RMSE é a "realidade". Ele nos diz, em média, o quanto o modelo está errando na mesma escala do que está sendo medido.

**Exemplo:**

Um corretor usa uma IA para prever o valor de três casas.

● Casa 1: Valor Real: R$ 200k | Previsão: R$ 210k (Erro = - 10)
● Casa 2: Valor Real: R$ 300k | Previsão: R$ 290k (Erro = 10)
● Casa 3: Valor Real: R$ 500k | Previsão: R$ 550k (Erro = - 50)

● **Interpretação:**

1. **Cálculo do MSE:** Primeiro elevamos os erros ao quadrado ( (-10)², 10², (-50)² → 100, 100, 2500). A média desses quadrados é 900. Note como o erro de 50 dominou o resultado.

2. **Cálculo do RMSE:** Tiramos a raiz de 900, resultando em 30.
Conclusão: O MSE de 900 ajudou a IA a ver que a "Casa 3" foi um erro grave. Já o RMSE de 30 diz ao corretor que, em média, o modelo erra por R$ 30 mil para mais ou para menos.

● **Resolução:**

1. Cálculo do MSE
● n (Total de exemplos): 3 (Pois analisamos 3 casas).
● yi (Valores Reais): 200, 300, 500 (Os preços reais das casas).
● ŷi (Valores Previstos): 210, 290, 550 (O que a IA "chutou").
● (yi - ŷi) (A Diferença/Erro):
Casa 1: 200 - 210 = -10
Casa 2: 300 - 290 = 10
Casa 3: 500 - 550 = -50
● (yi - ŷi)² (O Quadrado do Erro):
● (-10)² = 100
● (10)² = 100
● (-50)² = 2500
● ∑ (Somatório dos Quadrados): 100 + 100 + 2500 = 2700.
● MSE (Resultado Final): 2700 ÷ 3 = 900

2. Cálculo do RMSE
● RMSE (Resultado Final): $RMSE = \sqrt{900} = 30$ mil

**Fixação:**

a) Um modelo de previsão de temperatura apresentou um MSE de 16.

1. Qual é o valor do RMSE deste modelo?
2. Se a temperatura é medida em Graus Celsius (°C), em qual unidade o resultado 16 está expresso?

b) Dois modelos de IA (A e B) tentam prever o peso de recém-nascidos.

● O Modelo A teve erros pequenos e constantes em todos os bebês.
● O Modelo B acertou quase todos, mas errou feio (por muito) em um único bebê

1. Qual dos dois modelos provavelmente terá o MSE mais alto? Por quê?
2. Por que o pesquisador prefere usar o RMSE na hora de apresentar o relatório final para os pediatras?

### 2.6.3. Acurácia

A acurácia mede a proporção de acertos totais sobre o total de exemplos. É a métrica mais simples, mas pode ser enganosa em dados desbalanceados.

**Aplicação:**

Limitação crítica em IA: Se 99% dos e-mails não são spam, um modelo que classifica tudo como "não spam" terá 99% de acurácia — mas será completamente inútil para detectar spam real. Por isso, em IA, raramente a acurácia sozinha é suficiente.

**Matriz de Confusão e seus derivados:**
Antes de entender as métricas de classificação, é preciso entender a Matriz de Confusão. Ela organiza os resultados de um classificador em quatro categorias:
Verdadeiro Positivo (VP): o modelo disse "positivo" e estava certo
Verdadeiro Negativo (VN): o modelo disse "negativo" e estava certo
Falso Positivo (FP): o modelo disse "positivo" mas estava errado (alarme falso)
Falso Negativo (FN): o modelo disse "negativo" mas estava errado (perdeu um caso real)

**Fórmula:**

$$Acurácia = \frac{VP + VN}{VP + VN + FP + FN}$$

**Exemplo:**

Um sistema de IA foi testado em um lote de 100 exames de raio-X. O objetivo era identificar quais pacientes tinham pneumonia. A análise da Matriz de Confusão revelou o seguinte:
● 85 vezes a IA disse "positivo" e acertou (VP).
● 5 vezes a IA disse "negativo" e acertou (VN).
● 7 vezes a IA deu um alarme falso (FP).
● 3 vezes a IA não detectou a doença presente (FN).

**Interpretação:**
Ao aplicarmos a fórmula da Acurácia, somamos os acertos totais (85 + 5 = 90) e dividimos pelo total de casos (100). O resultado é uma Acurácia de 0.90 (ou 90%). Isso indica que, de cada 10 exames analisados, a IA acerta o diagnóstico em 9 deles. Porém, o médico deve ficar atento aos 3 casos de Falso Negativo, onde a doença passou despercebida, mostrando que a acurácia alta nem sempre significa que o modelo é perfeito para situações críticas.

**Fixação:**

a) Um filtro de e-mails processou 50 mensagens. Ele classificou corretamente 30 como "Spam" e 15 como "Não Spam". As outras 5 mensagens ele errou a classificação.

1. Qual o valor total de acertos (VP + VN) desse modelo?
2. Qual a Acurácia final desse filtro de e-mails?

b) Imagine um sistema de segurança de um banco que analisa 1.000 transações. Dessas, 990 são normais e 10 são fraudes. O sistema está mal configurado e classifica todas as 1.000 transações como "Normais".

1. Qual será a Acurácia desse sistema (calcule a porcentagem de acertos sobre o total)?
2. Por que, neste caso específico, uma acurácia tão alta é considerada um resultado "enganoso" e perigoso para o banco?

Slide Canva:
https://www.canva.com/design/DAHGvwle7-M/iJyptYm9pcPVGFsBVYTOzw/edit

Forms de Fixação:
https://docs.google.com/forms/d/e/1FAIpQLScaJzhbCXkpu_F2lnivYz4F6wb-Fbx77DkmTLwsXgUIqj7X-g/viewform?usp=header