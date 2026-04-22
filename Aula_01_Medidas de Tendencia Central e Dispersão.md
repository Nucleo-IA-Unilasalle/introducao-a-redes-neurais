2. Estatística aplicada para AIs

Fornece as técnicas para algoritmos identificarem padrões, como regressão linear, regressão logística e algoritmos de agrupamento.

	Medidas de Tendência Central: Média, Mediana e Moda (Foco em: Tratamento de dados ausentes e preenchimento de lacunas).
	Medidas de Dispersão: Variância e Desvio Padrão (Foco em: Entender o espalhamento dos dados e base para a Normalização).
	Análise de Correlação: Coeficiente de Pearson (Foco em: Identificar quais variáveis realmente impactam o modelo e eliminar dados redundantes).
	Inferência Estatística e Amostragem: População vs. Amostra (Foco em: Como o modelo generaliza o que aprendeu no treino para o mundo real).
	Distribuições de Probabilidade: Distribuição Normal/Gaussiana e Softmax (Foco em: Inicialização de pesos e saída final de classificação).
	Métricas de Erro e Performance: Erro Médio Quadrático (MSE), Erro Absoluto (MAE) e Acurácia (Foco em: Medir o sucesso do treinamento).


2.1. Medidas de Tendência Central

2.1.1. Média

É a soma de todos os valores pertencentes a um conjunto de dados e dividindo o resultado pela quantidade de elementos. Para as AIs, é uma ferramenta de equilíbrio.

Aplicação:

	Tratamento de Dados Faltantes: Quando uma base de dados tem buracos (ex: idades faltando em um cadastro), usamos a média do grupo para preencher esses vazios sem alterar o comportamento geral do conjunto.

	Normalização: Para que um neurônio não dê importância demais a um número grande (ex: Salário) e ignore um pequeno (ex: Idade), usamos a média para centralizar todos os dados em torno de zero.

	Formula:

    ![] (Imagens_Formula/formula_01.png)


	 (O "x" com barra): É o resultado final, a nossa Média. No exemplo, é o valor 5.
	  (Sigma Maiúsculo): Esse símbolo bonitão é apenas uma ordem de comando. Ele diz: "Some tudo o que vem depois de mim".
	  (O elemento): Representa cada número individual da sua lista (o 2, o 4, o 6 e o 8). O "i" é como um índice (1º número, 2º número...).
	  (O divisor): É a quantidade total de itens que você tem. No nosso caso, como temos quatro números (2, 4, 6, 8), o   = 4

Exemplo:

Imagine que temos os erros de 4 predições de uma IA: 2, 4, 6 e 8.

	Identificamos os dados ( ): x1=2, x2=4, x3=6 e x4=8
	Contamos quantos são (n): São 4 números.
	Executamos o Sigma (  ) 2 + 4 + 6 + 8 = 20.
	Finalizamos a fórmula ( ): 20 \ 4 = 5


Fixação:

a) Uma rede neural processou 5 imagens. O tempo de processamento de cada uma foi: 10ms, 12ms, 15ms, 13ms e 10ms. Qual o tempo médio de processamento por imagem?

b) Em uma tabela de "Idade de Clientes", você encontrou 4 registros: 20, 30, 40 e 50 anos. No 5º registro, o dado está faltando. Se decidirmos preencher esse dado faltante com a média dos outros quatro, qual valor será inserido?


2.1.2. Mediana

Diferente da média, a Mediana é o valor central que divide seus dados ao meio. Na Engenharia de IA, ela é o nosso "filtro de ruído". Para achar a Mediana (Md), primeiro precisamos ordenar os dados (o Rol). O cálculo também depende se o número de elementos (n) do conjunto é par ou ímpar.

Aplicação:

	Resistência a Outliers (Valores Discrepantes): Imagine que você treina uma IA com salários. Se houver um bilionário na lista, a Média vai lá para o alto e engana o modelo. A Mediana ignora esse valor extremo e foca no que é comum.

	Limpeza de Dados Sujos: Quando os sensores (como câmeras ou termômetros) falham e geram um número absurdo (ex: um sensor de temperatura marcando 500°C por erro técnico), usamos a Mediana para ignorar esse erro e manter o treinamento estável.

	Formula:

	Se for par: A mediana é a média dos dois valores centrais.

    ![] (Imagens_Formula/formula_02.png)


	Se for ímpar: A mediana é a posição central.

    ![] (Imagens_Formula/formula_03.png)



(Obs.: Considerando um conjunto com quantidade par de elementos “n”)

	x(n/2): É o valor que está na posição da "primeira metade"
	x(n/2 + 1): É o valor que está na posição imediatamente seguinte ("segunda metade").


Exemplo:

Imagine os tempos de resposta de uma IA em segundos: 1.2, 0.5, 30.0, 0.8, 1.0 .

Criar o Rol (Ordenar): 0.5, 0.8, 1.0, 1.2, 30.0
Contar os itens (n): Temos 5 itens (Ímpar)
Aplicar a posição: (5+1) / 2 = 3ª posição
Identificar o valor: O 3º item é o 1.0

Nota: Repare que o valor 30.0 (muito alto) não afetou a Mediana, mas destruiria a Média.


Fixação:

	Uma rede neural classificou 7 imagens com as seguintes confianças (0 a 100): 85, 90, 70, 95, 60, 100, 80. Qual a Mediana de confiança desse lote? (Dica: coloque em ordem primeiro!).

	Analisando o uso de memória de 6 servidores: 4GB, 8GB, 2GB, 16GB, 4GB, 32GB. Qual é a Mediana de consumo de memória deste cluster?


2.1.3. Moda

Ao monitorar os erros de um modelo por uma hora e obteve os seguintes códigos de erro: 404, 500, 404, 403, 500, 404, 502. É simplesmente o valor que mais se repete em um conjunto de dados. Na IA, ela é a nossa ferramenta para Dados Categóricos (textos, classes, etiquetas).

Aplicação:

	Preenchimento de Categorias (Imputação de Classes): Se você tem uma base de dados de "Tipos de Veículos" e em alguns registros a coluna está vazia, você não pode tirar a "média" entre um Carro e uma Moto. Você usa a Moda (o tipo que mais aparece, ex: "Sedan") para preencher o vazio.

	Voto Majoritário (Ensemble Learning): Em sistemas de IA avançados, onde várias redes neurais "votam" no que viram em uma imagem, o resultado final escolhido é a Moda das respostas. Se 3 IAs dizem "Gato" e 1 diz "Cachorro", a resposta final é a Moda: "Gato".

	Formula: A Moda não possui uma fórmula algébrica complexa como a média. Ela é definida pela frequência.

Mo = Valor com maior frequência absoluta (fi)

•  fi: É a contagem de quantas vezes cada item aparece.
•  Amodal: Quando nenhum valor se repete.
•  Bimodal: Quando dois valores diferentes empatam no topo da repetição.

Exemplo:

Imagine as etiquetas de saída de um classificador de objetos em um vídeo: [Pessoa, Carro, Pessoa, Árvore, Pessoa, Carro]

	Contagem (fi):
	Pessoa: 3 vezes
	Carro: 2 vezes
	Árvore: 1 vez

	Identificar a maior frequência: O valor “pessoa” aparece mais.
	Resultado: Mo = Pessoa


Fixação:

	Uma base de dados de sensores de temperatura registrou: 22°C, 25°C, 22°C, 28°C, 22°C, 30°C. Qual é a temperatura modal desse sensor?

	Monitorando os erros de um modelo por uma hora e obteve os seguintes códigos de erro: 404, 500, 404, 403, 500, 404, 502.

	Qual é a Moda desses erros?
	Se você fosse o engenheiro, em qual erro focaria primeiro baseado apenas na estatística?


2.2. Medidas de Dispersão: Variância e Desvio Padrão

Se a Média diz onde os dados estão "amontoados", a Dispersão diz o quão espalhados eles estão. Na IA, isso é o que separa um modelo estável de um modelo que chuta valores aleatórios.

2.2.1. Variância

A Variância mede a distância média de cada dado em relação à média do conjunto.

Aplicação:

	Na Engenharia de IA: Ela indica a Instabilidade. Se a variância do erro da sua IA é alta, significa que ela acerta muito em alguns casos e erra feio em outros. Queremos uma variância baixa e controlada.

	Variância Populacional (σ²):

É aplicada quando tem todos os dados possíveis do universo que se está estudando.
	Exemplo: 
Você quer a variância da idade de todos os funcionários da sua empresa (e você tem a lista completa de todos os 50 funcionários).
	Divisor: Você divide pelo número total de itens (n).

	Formula:

"σ" ^"2"  "="  (∑▒(xi-¯x)^2 )/n

Ordem discriminada para o cálculo da Variância populacional (geral):

	¯x: calcular a média;
	xi: dado individual do conjunto;
	∑: Representa do somatório total dos desvios individuais somados após serem 
elevados ao quadrado (xi-¯x)².
Aqui calcula-se cada desvio (xi-¯x)  – diferença do dado menos a média, eleva-se ao quadrado e soma-se os resultados;
	“n”: total de elemento do conjunto
	"σ" ^"2" :  é o resultado do somatório ( ∑ ) dividido pelo número total de elementos (n), resultando na variância.



Fixação:

Lembrete: Use esta quando você tem o conjunto total de dados.

	Um pequeno modelo de IA processou apenas 4 requisições. Os erros de tempo (em ms) foram: 2, 4, 6 e 8.
	Calcule a média (¯x).
	Calcule a Variância Populacional ("σ" ^"2" ).
(Dica: Como são apenas esses 4 dados no universo do teste, use o divisor n=4).

	Um rack de servidores possui exatamente 5 sensores de temperatura. Em um momento crítico, as leituras foram: 30°C, 32°C, 30°C, 35°C e 33°C.
	Encontre a média das temperaturas.
	Calcule a Variância Populacional 〖"(σ" 〗^"2" ) para entender o quão instável está o resfriamento desse rack específico.


	Variância Amostral (s²):

É aplicada quando tem todos os dados possíveis do universo que se está estudando.
	Exemplo: 
Você quer saber a variância do tempo de resposta de uma IA no mundo, mas você só testou 100 vezes no seu computador.
	Divisor: Você divide pelo número total de itens (n-1).

	Formula:

"s" ^"2"  "="  (∑▒(xi-¯x)^2 )/(n-1)

Ordem discriminada para o cálculo da Variância Amostral:
	¯x: calcular a média;
	xi: dado individual do conjunto;
	∑: Representa do somatório total dos desvios individuais somados após serem 
elevados ao quadrado (xi-¯x)².
Aqui se calcula cada desvio (xi-¯x)  – diferença do dado menos a média, eleva-se  ao quadrado e soma-se todos os resultados;
	“n - 1”: total de elemento do conjunto – 1.
	"s" ^"2" :  é o resultado do somatório ( ∑ ) dividido pelo número total de elementos  (n – 1) resultando na variância amostral.


Fixação:

Lembrete: Use esta quando os dados são apenas uma parte (amostra) de um todo maior (IA em produção).

	É extraído uma amostra aleatória de 3 logs de erro de um modelo que roda milhões de vezes por dia. Os valores foram: 1, 3 e 5.
	Calcule a média.
	Calcule a Variância Amostral ("s" ^"2" ).
(Dica: Como é uma amostra, o divisor deve ser n-1, ou seja, 3-1 = 2).

	Para testar a qualidade de um novo Dataset, um engenheiro separou uma amostra de 6 imagens e mediu o tempo de classificação (em segundos): 0.5, 0.7, 0.5, 0.8, 0.6 e 0.5.
	Determine a Média.
	Calcule a Variância Amostral ("s" ^"2" ).
	Explique por que, neste caso, dividir por n-1 é mais seguro para a Engenharia de IA do que dividir apenas por n.


2.2.2. Desvio Padrão

É a distância média (grau de dispersão) que os seus dados estão em relação à média do grupo (¯x). Ele funciona como uma "Régua de Erro".

	Desvio Padrão Baixo: Significa que os dados estão "comportados" e muito próximos da média. (Ex: Uma linha de produção muito precisa).
	Desvio Padrão Alto: Significa que os dados estão "espalhados" e longe da média. (Ex: Um processo instável ou imprevisível).

	Formula: 
"s ="  √((∑▒(xi-x ̅ )^2 )/(n-1))
	¯x: calcular a média;
	xi: dado individual do conjunto;
	∑: Representa do somatório total dos desvios individuais somados após serem elevados ao quadrado (xi-¯x)².
Aqui se calcula cada desvio (xi-¯x)  – diferença do dado menos a média, eleva-se  ao quadrado e soma-se todos os resultados;
	“n - 1”: total de elemento do conjunto – 1.
	"s" : Desvio Padrão Amostral (resultado)


	Exemplo:
Imagine que o tempo de processamento de três tarefas na IA foi de 2s, 4s e 6s.

	Média (¯x): 4s.
	Variância ("s" ^"2" ): s²=  √(((2-4)^2+(4-4)^2+(6-4)^2)/(n-1)) = (4+0+4)/2 = 4s²

	Desvio Padrão (s):  s =  √4  = 2s

Interpretação: O tempo médio é 4 segundos, com uma variação padrão de 2 segundos para cima ou para baixo.

	Fixação:

a) Um sensor de temperatura em um servidor registrou três leituras em uma hora: 20°C, 24°C e 28°C. Sabendo que a variância dessas leituras é 16, calcule o Desvio Padrão desse sensor.

b) Monitorando o erro de predição de uma IA em 5 testes. Os valores encontrados foram: 2, 3, 5, 7 e 8. Calcule a média, a variância amostral e, por fim, o Desvio Padrão desse conjunto de erros.


Atividades de fixação no forms:
https://docs.google.com/forms/d/1fuu8Nj6tjhI7dprVhwpOWmuiKDpJw6YR23imXMwdFtQ/edit

Gabarito no forms:
https://docs.google.com/forms/d/1F9BbDz_2nZTWhNvI7Gk7fSEAAKwGE-N6vOCD5_8imqE/edit

