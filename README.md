# Projeto de Redes Neurais: Detecção Multimodal de Discurso de Ódio

## Integrantes do Grupo
* **Amanda Joioso**
* **Angela Muñante**
* **Gabriel Andreghetti**
* **Lucas Almeida**
* **Lucas Ferreira**
* **Pedro Gagini**
* **Pedro Salmaze**

---

## Descrição do Projeto

Este repositório contém a implementação do projeto final da disciplina de Redes Neurais, que visa avaliar a capacidade de implementar e avaliar arquiteturas de redes neurais para resolver problemas práticos do mundo real.

O problema escolhido é a **detecção de discurso de ódio em tweets**, utilizando o dataset **MMHS150K**, disponível em [https://www.kaggle.com/datasets/victorcallejasf/multimodal-hate-speech](https://www.kaggle.com/datasets/victorcallejasf/multimodal-hate-speech).

O projeto é dividido em duas etapas:
1.  **Parte 1 (Unimodal - Texto):** Análise comparativa de diferentes arquiteturas de Transformer (e uma baseline não-LLM) para a classificação de tweets baseada apenas em seu conteúdo textual.
2.  **Parte 2 (Multimodal):** Extensão da melhor abordagem da Parte 1 para incorporar a informação visual (imagens dos tweets), criando um classificador multimodal.

---

## Estrutura do Repositório

```
/
│
├── README.md             # Este arquivo
│
└── notebooks/
    ├── parte1_texto/     # Notebooks da 1ª entrega (análise por texto)
    └── parte2_multimodal/  # Código da 2ª entrega (análise multimodal)
```

---

## ⚠️ Visualização dos Notebooks

O visualizador padrão do GitHub pode apresentar um erro (`Invalid Notebook: ... 'state' key is missing ...`) ao tentar renderizar os notebooks deste projeto. Isso ocorre por um problema de compatibilidade conhecido com os widgets de saída do treinamento no Google Colab.

**Para visualizar os notebooks com todas as saídas (gráficos, tabelas e resultados), por favor, utilize os links do `nbviewer` abaixo, que renderizam os arquivos corretamente:**

* **[Visualizar Notebook do BiLSTM_Word2Vec_Classifier](https://nbviewer.org/github/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte1_texto/BiLSTM_Word2Vec_Classifier.ipynb)**
* **[Visualizar Notebook do BERT](https://nbviewer.org/github/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte1_texto/BERT.ipynb)**
* **[Visualizar Notebook do RoBERTa](https://nbviewer.org/github/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte1_texto/Redes_Neurais_RoBERTa.ipynb)**
* **[Visualizar Notebook do XLNet](https://nbviewer.org/github/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte1_texto/XLNet.ipynb)**
* **[Visualizar Notebook do Llama Meta Hate](https://nbviewer.org/github/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte1_texto/llamaMetaHate.ipynb)**
* **[Visualizar Notebook do BERT e do SWIM com Multihead Attention](https://nbviewer.org/github/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte2_multimodal/BERT_SWIM%20-%20Detec%C3%A7%C3%A3o%20de%20Discurso%20de%20%C3%93dio.ipynb)**
---

## Resultados da Parte 1 (Unimodal - Texto)

Nesta etapa, foram avaliados cinco modelos diferentes para a tarefa de classificação binária ("Hate" vs "Não Hate"), incluindo modelos baseados em redes neurais tradicionais e em modelos de linguagem (LLMs). Cada notebook contém a implementação completa, incluindo pré-processamento, treinamento e teste de um desses modelos, permitindo comparar seus desempenhos de forma individual.

### Pré-processamento

Originalmente, o dataset conta com seis categorias diferentes: Não Hate, Racista, Sexista, Homofóbico, Religião e Outros. Ao analisar a distribuição das labels, observa-se uma grande predominância da classe "Não Hate", enquanto as demais estão distribuídas de forma desigual e com representatividade bem menor. 

<img src="https://github.com/user-attachments/assets/cbeee146-a371-40d8-a380-3509f24ef1e1" width="500" />

Por conta do desbalanceamento original, optou-se pela binarização das labels, ou seja, as categorias Racista, Sexista, Homofóbico, Religião e Outros foram agrupadas em uma única classe chamada Hate. Após essa transformação, a distribuição das classes ficou da seguinte forma:

<img src="https://github.com/user-attachments/assets/cf03be18-b292-442a-9a1e-ff20f3fb5ed4" width="500" />

Apesar dessa binarização, ainda existe um desbalanceamento significativo entre as classes. Por isso, foi aplicado um undersampling na classe majoritária para equilibrar a quantidade de exemplos entre as duas classes. Os conjuntos de validação e teste foram mantidos com a distribuição original para garantir que a avaliação do modelo reflita um cenário realista.

<img src="https://github.com/user-attachments/assets/6c301868-769f-4548-91a7-16146c9090cf" width="500" />

#### Tokenização

Os textos foram tokenizados de acordo com o modelo utilizado, respeitando os requisitos específicos de cada arquitetura.

### Treinamento dos modelos

Os modelos foram treinados conforme as especificações de cada um, adaptando os parâmetros e configurações quando necessário.

### Avaliação dos Modelos

#### BiLSTM_Word2Vec_Classifier

Uma abordagem com modelo BiLSTM (Bidirectional Long Short-Term Memory) e Word2Vec combina técnicas de aprendizado de máquina para o processamento de linguagem natural (PLN). O Word2Vec é um modelo de embedding que converte palavras em vetores numéricos densos, capturando relações semânticas entre elas com base em seu contexto. Já o BiLSTM é uma arquitetura de rede neural recorrente que processa sequências de texto em duas direções: uma do início para o fim e outra do fim para o início, permitindo que o modelo capture informações contextuais de longo alcance, tanto passadas quanto futuras. Juntas, essas abordagens possibilitam uma compreensão profunda e bidirecional do texto, sendo eficazes no nosso objetivo de análise de Hate Speech, em que a classificação pode depender do contexto.

Com o método de undersampling aplicado a nossa base de dados obtemos os seguintes resultados:

* Acurácia: 0,6303
* Precisão: 0,5741
* Recall: 0,6390
* F1-Score: 0,6048

Também plotamos uma matriz de confusão que demonstrou um bom equilíbrio entre verdadeiros positivos e verdadeiros negativos, indicando que o modelo conseguiu generalizar razoavelmente bem para ambas as classes.

#### BERT

Para a tarefa de detecção de discurso de ódio, foi escolhido testar tambem o modelo BERT (bert-base-uncased), uma arquitetura baseada em transformadores conhecido por seu bom desempenho em tarefas de classificação de texto.

A avaliação foi feita com a partição de teste, dando os seguintes resultados:

* Acurácia: 0,666
* Precisão: 0,616
* Recall: 0,653
* F1-score: 0,634

A matriz de confusão mostrou que o modelo teve um desempenho razoável nas duas classes ("Hate" e "Não Hate"), apesar de alguns erros de classificação. Também foi analisada a curva de perda (loss) por época, que indicou sinais de overfitting, com a perda de validação aumentando ao longo do tempo. No entanto, como foi utilizado o early stopping, o treinamento foi interrompido no momento certo para evitar que o modelo se ajustasse demais aos dados de treino.

#### RoBERTa

Para esta análise, foi selecionada também uma variante especializada do RoBERTa, o modelo cardiffnlp/twitter-roberta-base-offensive. A escolha deste modelo se deve ao fato de ele já ser pré-treinado com milhões de tweets para identificar linguagem ofensiva.

Os seguintes resultados foram alcançados no conjunto de teste:

* Acurácia: 0,6700
* Precisão: 0,6289
* Recall: 0,6207
* F1-Score: 0,6248


O RoBERTa apresentou um bom equilíbrio entre Precisão (62,9%) e Recall (62,1%). A matriz de confusão revelou um modelo com um comportamento equilibrado, sem um viés extremo para nenhuma das classes. O número de Falsos Positivos (1621) e Falsos Negativos (1679) é relativamente próximo. Portanto, modelo aprendeu a identificar ambas as classes de forma moderada, mas ainda com uma margem de erro considerável para ambos os tipos de falha, o que é refletido em um F1-Score de 0,6248. Além disso, análise da dinâmica de treinamento ao longo das épocas revelou sinais de overfitting, com a performance no conjunto de validação atingindo seu pico na segunda época antes de começar a declinar. Para assegurar a robustez do resultado final, foi utilizado o mecanismo load_best_model_at_end=True, que retorna o modelo do checkpoint com a melhor performance de generalização, mitigando os efeitos do overfitting.
    
#### XLNet

Foi avaliado também o modelo XLNet-base-cased, uma arquitetura baseada em transformadores que utiliza modelagem autoregressiva permutada para capturar padrões contextuais complexos em sequências de texto. O treinamento foi realizado com undersampling e poucas épocas, em razão de limitações de hardware que impediram uma exploração mais ampla dos hiperparâmetros.

Os resultados no conjunto de teste foram:

* Acurácia: 0,6508
* Precisão: 0,7398
* Recall: 0,3257
* F1-Score: 0,4523

Apesar da boa precisão, o modelo apresentou baixo recall, indicando dificuldade em identificar casos reais de discurso de ódio. A matriz de confusão confirmou uma tendência a favorecer a classe majoritária (não hate), gerando muitos falsos negativos. Além disso, a curva de perda sugeriu subajuste, com pouca melhoria ao longo do treino. No geral, o XLNet mostrou certo potencial, mas teve desempenho inferior aos demais modelos testados.

#### Llama Meta Hate

A abordagem implementada utiliza o modelo pré-treinado Llama-3-8B-Distil-MetaHate, desenvolvido através de destilação de conhecimento a partir do modelo Llama-3-70B-Instruct. Este modelo especializado emprega metodologias Chain-of-Thought (CoT) para realizar análise contextual profunda de sentenças. O modelo passou por um processo de fine-tuning específico para detecção de hate speech, incorporando técnicas de Parameter-Efficient Fine-Tuning (PEFT) que mantêm alta performance com maior eficiência computacional.

Com o conjunto de dados de teste passados como input para o modelo obtivemos os seguintes resultados:

* Acurácia: 0,5147
* Precisão: 0,5084
* Recall: 0,8511
* F1-Score: 0,6365

A análise de performance revelou características interessantes do modelo. A matriz de confusão demonstrou um desequilíbrio significativo, com alta sensibilidade para detectar hate speech (recall de 85.11%) mas baixa especificidade para casos não-hate speech (17.93% de acurácia). O modelo apresentou uma tendência pronunciada para classificar textos como hate speech, resultando em 3.725 falsos positivos contra apenas 674 falsos negativos. Esta característica indica um comportamento conservador do modelo, priorizando a detecção de possíveis casos de discurso de ódio.


Abaixo, a tabela consolidada com os resultados finais no conjunto de teste.

| Métrica | BiLSTM_Word2Vec_Classifier | BERT | RoBERTa | XLNet | Llama Meta Hate |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **F1 (Hate)** | 0,60 | 0,63 | 0,62 | 0,45 | **0,64** |
| **Recall (Hate)** | 0,64 | 0,65 | 0,62 | 0,32 | **0,85** |
| **Precisão (Hate)** | 0,57 | 0,62 | 0,63 | **0,74** | 0,51 |
| **Acurácia Geral** | 0,63 | **0,67** | **0,67** | 0,65 | 0,51 |

### Análise e Conclusão da Parte 1

Ao analisar os resultados observados, percebe-se que os modelos baseados em transformadores (BERT e  RoBERTa) superam arquiteturas tradicionais como o BiLSTM na tarefa de detecção de discurso de ódio — embora este tenha apresentado desempenho próximo — provavelmente devido à sua maior capacidade de capturar o contexto semântico das frases. O desempenho do BERT e do RoBERTa, mesmo com a base sendo reduzida, evidencia que modelos pré-treinados são mais robustos e demandam menos ajuste fino para alcançar bons resultados.

Além disso, os resultados do Llama Meta Hate indicam que, embora modelos especializados possam alcançar alta sensibilidade, existe um trade-off importante entre recall e precisão, e que um alto recall não necessariamente representa um modelo confiável para aplicações práticas, em que falsos positivos podem gerar problemas significativos. Por outro lado, o comportamento do XLNet sugere que arquiteturas mais complexas não garantem melhor desempenho se não forem bem ajustadas ou se a capacidade computacional for limitada.

## Resultados da Parte 2 (Multimodal - Texto + Imagem)

Nesta etapa, exploramos modelos que combinam informações textuais e visuais para a tarefa de classificação binária ("Hate" vs "Não Hate"). O objetivo é avaliar se a adição de sinais visuais pode melhorar a detecção de discurso de ódio em conteúdos multimodais, como postagens que combinam imagem e legenda. Foram desenvolvidas cinco arquiteturas diferentes, cada uma com estratégias distintas de fusão de embeddings. Todos os modelos foram treinados com os embeddings textuais provenientes do BERT (`bert-base-uncased`) e embeddings visuais extraídos com o Swin Transformer (`swin-tiny-patch4-window7-224`), previamente salvos.

### Concatenação simples com MLP

O modelo mais direto combina os embeddings textuais e visuais por concatenação, formando um único vetor de entrada. Esse vetor é passado por uma MLP (rede neural totalmente conectada) que realiza a classificação.

Apesar de sua simplicidade, essa abordagem apresentou bom desempenho inicial, beneficiando-se de menor complexidade e menor risco de overfitting. No entanto, como não modela interações entre texto e imagem, pode deixar passar nuances contextuais importantes.

### Concatenação simples com Focal Loss

Neste modelo, utilizamos a mesma estratégia de concatenação simples dos embeddings, mas com algumas melhorias:

* A rede MLP utiliza camadas lineares com ativação ReLU e dropout.
* A função de perda utilizada é a **Focal Loss**, que prioriza amostras difíceis por meio dos hiperparâmetros `alpha` e `gamma`.

O treinamento inclui early stopping e avaliação dinâmica em múltiplos thresholds para encontrar a melhor combinação de parâmetros que maximize o F1-score macro. O modelo final é reavaliado no conjunto de validação com matriz de confusão e relatório de classificação.

Essa abordagem teve ganhos notáveis na identificação da classe minoritária, com melhora significativa no recall, mas ainda apresentou trade-offs em relação à precisão.

### Multihead Attention

Este modelo aplica **atenção multi-cabeças** para integrar embeddings textuais (BERT) e visuais (Swin). Ambos são projetados para um espaço vetorial comum (`hidden_dim=1024`) e concatenados como uma sequência de dois tokens (texto + imagem). A camada `MultiheadAttention` permite que as modalidades interajam diretamente, capturando relações cruzadas.

Após a atenção, aplica-se **pooling médio** sobre os dois tokens, seguido por uma rede feedforward com normalização, ReLU e dropout. A saída é passada por um classificador MLP que prevê a classe final.

Essa arquitetura obteve o **melhor desempenho geral**, com **F1-score macro de 0.63**, equilibrando precisão e recall nas duas classes. Sua força está na capacidade de capturar interações relevantes entre texto e imagem sem o custo computacional de Transformers completos.

A atenção possibilita que o modelo atribua pesos diferenciados às modalidades, capturando interações mais sutis entre elas. Como resultado, o modelo apresentou equilíbrio entre precisão e recall nas duas classes, indicando boa generalização.

### Baseado em Transformers

Esse modelo usa uma abordagem ainda mais avançada, tratando os embeddings das duas modalidades como uma sequência de dois tokens e processando-os com um Transformer Encoder completo, com múltiplas camadas de autoatenção e positional embeddings. Ele é projetado para capturar relações contextuais profundas entre as modalidades, semelhante aos Transformers usados em NLP. Após o encoding, aplica-se um pooling médio seguido de um classificador MLP. Embora poderoso, sua complexidade pode levar ao overfitting em datasets pequenos ou desbalanceados, como é o caso. Por fim, o modelo demonstrou potencial, com desempenho razoável no conjunto de validação, mas levemente inferior ao Multihead Attention em termos de F1-score macro, e com um custo computacional muito alto.

### Desempenho no Conjunto de Validação (Multimodal: Texto + Imagem)

| Métrica                  | Concat. + MLP   | Concat. + Focal Loss | Multihead Attention | Baseado em Transformers |
| ------------------------ | :-------------: | :------------------: | :-----------------: | :---------------------: |
| **F1 (Hate)**            |     **0.62**    |         0.60         |         0.61        |           0.61          |
| **Recall (Hate)**        |     **0.62**    |         0.57         |         0.60        |           0.60          |
| **Precisão (Hate)**      |       0.61      |       **0.63**       |         0.62        |           0.61          |
| **F1-Score Macro**       |       0.65      |         0.65         |       **0.65**      |           0.65          |
| **Acurácia Geral**       |       0.65      |         0.66         |       **0.66**      |           0.65          |
| **Melhor Val F1**        |      0.6506     |        0.6504        |      **0.6511**     |          0.6471         |
| **Melhor Época**         |        1        |           —          |          2          |            3            |
| **Loss na Melhor Época** |      0.4417     |           —          |        0.4247       |        **0.4110**       |

### Desempenho no Conjunto de Teste (Multimodal: Texto + Imagem)

Multihead Attention obteve desempenho equilibrado entre as classes "hate" e "não hate", com acurácia geral de 63%. A classe "não hate" teve maior precisão (0.69), indicando menos falsos positivos, enquanto a classe "hate" apresentou maior recall (0.65), mostrando boa capacidade de identificar discursos de ódio, embora com mais falsos positivos. O F1-score macro de 0.63 indica desempenho médio consistente entre as classes, o que é desejável em tarefas com importância equivalente para ambas. Esses resultados refletem que a atenção multi-cabeça consegue capturar relações relevantes nos dados, mas ainda há espaço para melhorias, especialmente na distinção entre as classes em cenários ambíguos. A Matriz de Confusão é exibida abaixo.

![Matriz de Confusão no Conjunto de Teste](https://github.com/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte2_multimodal/confusion_matrix.png?raw=true)


## Concusão

Este trabalho investigou diferentes abordagens para a detecção de discurso de ódio, tanto no formato unimodal (texto) quanto multimodal (texto + imagem). Os resultados demonstraram que modelos baseados em transformadores, como BERT e RoBERTa, oferecem desempenho superior em relação a arquiteturas tradicionais como BiLSTM, especialmente em tarefas puramente textuais, devido à sua capacidade de capturar melhor o contexto semântico.

Na etapa multimodal, os modelos que combinam embeddings textuais e visuais também apresentaram resultados promissores. A arquitetura com atenção multi-cabeça foi a que obteve o melhor desempenho geral, alcançando equilíbrio entre precisão e recall, além de uma boa acurácia. Isso mostra que a combinação de texto e imagem pode ser vantajosa para detectar nuances de discurso de ódio em conteúdos multimodais, como postagens em redes sociais.

No entanto, limitações computacionais representaram um desafio significativo ao longo do trabalho. Restrições de hardware dificultaram a exploração completa de modelos mais robustos, como Transformers com múltiplas camadas e fine-tuning mais aprofundado. Com maior capacidade computacional, seria possível aplicar arquiteturas mais sofisticadas, ajustar melhor os hiperparâmetros e, possivelmente, alcançar resultados ainda mais expressivos.

Apesar dessas limitações, os modelos propostos apresentaram desempenho satisfatório, com um bom trade-off entre acurácia, capacidade de generalização e custo computacional. Assim, a abordagem desenvolvida mostra-se viável e pode ser útil como ferramenta auxiliar para identificação automatizada de discursos de ódio, contribuindo para a moderação de conteúdo e promoção de ambientes digitais mais seguros.

