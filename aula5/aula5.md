# Análise Exploratória de Dados como Investigação Estatística 
A Análise Exploratória de Dados existe porque datasets reais não nascem prontos para modelagem.

Eles contêm:

- observações incompletas;
- erros de medição;
- pressupostos ocultos;
- variáveis ambíguas;
- amostras enviesadas;
- outliers;
- tipos de dados misturados;
- sumarizações enganosas;
- contexto social, histórico ou operacional.

Portanto, o objetivo da EDA não é meramente “visualizar dados”. O objetivo é reduzir a incerteza sobre nossas premissas antes de modelarmos a solução.

# Por quê EDA existe?
Antes de modelar, precisamos entender que tipo de objeto estamos analisando.

Um dataset não é meramente uma tabela. Ele é resultado de um processo:

1. Fenômeno do mundo real
2. Medição/registro
3. Representação dos dados
4. Limpeza e transformação
5. Análise
6. Modelagem
7. Decisão

Em cada etapa, informação pode ser perdida, distorcida, simplificada ou enviesada.

# Problemas que a EDA tenta mitigar

## Dados são incompletos
Alguns valores estão ausentes porque não foram coletados, não se aplicam, foram perdidos, censurados ou omitidos intencionalmente.

Exemplo:

- A idade pode estar ausente para alguns passageiros.
- A informação da cabine pode estar ausente para muitos passageiros.

Q: A ausência é aleatória ou carrega informação?

## Dados são codificados, não autoexplicativos
Variáveis podem parecer simples, mas esconder complexidade semântica.

Exemplo:

```python
pclass = 1, 2, 3
```
Isso é armazenado numericamente, mas não é uma variável _numérica contínua_. É uma variável _categórica ordinal_ representando a classe do bilhete.

*Atenção*: O tipo de dado em memória nem sempre é o mesmo que o tipo estatístico.

## Estatísticas resumidas podem enganar
Média, mediana, desvio-padrão e correlação são úteis, mas comprimem a realidade.

- Uma média pode esconder assimetria.
- Uma correlação pode esconder subgrupos.
- Uma tabela limpa pode esconder contexto histórico ou social.

## Padrões visuais são hipóteses, não conclusões
Um gráfico pode sugerir:

- Mulheres tiveram taxas maiores de sobrevivência.
- Passageiros da primeira classe tiveram taxas maiores de sobrevivência.
- Crianças podem ter tido padrões diferentes de sobrevivência.

Mas isso ainda não são afirmações causais.

A EDA nos ajuda a formar hipóteses. Ela não as prova por si só.

## Modelar sem EDA é perigoso

Sem EDA, podemos:

- Usar o tipo errado de variável;
- Imputar valores ausentes incorretamente;
- Codificar categorias de forma ruim;
- Treinar com vazamento de dados;
- Ignorar desbalanceamento de classes;
- Confiar demais em correlações;
- Deixar de perceber estruturas de subgrupos.

Isso cria uma boa transição:

EDA é a ponte entre dados brutos e modelagem responsável.

# Contexto Histórico
A estatística clássica frequentemente se concentrou em inferência formal: estimar parâmetros, testar hipóteses e tirar conclusões sobre populações a partir de amostras.

A Análise Exploratória de Dados, fortemente associada a _John Tukey_, deslocou a atenção para o ato de olhar diretamente para os dados: encontrar padrões, anomalias, estruturas e perguntas antes de se comprometer com um modelo formal.

Na ciência de dados moderna, a EDA cumpre um papel semelhante: ela nos ajuda a entender o dataset antes do pré-processamento, da engenharia de atributos, da seleção de modelos e da avaliação.

> A inferência formal pergunta: _“O que podemos concluir?”_
> A EDA pergunta primeiro: _“O que estamos olhando?”_

# Dataset Titanic
O dataset Titanic é útil porque é pequeno, intuitivo, historicamente situado e cheio de problemas comuns em dados.

Interpretação: 

- Cada linha representa um passageiro.
- Cada coluna representa um atributo registrado sobre esse passageiro.
- A variável-alvo é a sobrevivência.
- A pergunta de modelagem é:

Podemos usar informações dos passageiros para estimar a probabilidade de sobrevivência?

## Estrutura
| Variável   | Significado                | Tipo estatístico                   |
| ---------- | -------------------------- | ---------------------------------- |
| `survived` | Se o passageiro sobreviveu | Categórica binária                 |
| `pclass`   | Classe do bilhete          | Categórica ordinal                 |
| `sex`      | Sexo registrado            | Categórica nominal                 |
| `age`      | Idade do passageiro        | Numérica contínua                  |
| `sibsp`    | Irmãos/cônjuges a bordo    | Numérica discreta                  |
| `parch`    | Pais/filhos a bordo        | Numérica discreta                  |
| `fare`     | Tarifa paga                | Numérica contínua                  |
| `embarked` | Porto de embarque          | Categórica nominal                 |
| `ticket`   | Número do bilhete          | Identificador / semelhante a texto |
| `cabin`    | Número da cabine           | Texto / parcialmente estruturada   |

