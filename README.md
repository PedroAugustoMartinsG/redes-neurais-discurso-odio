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

* **[Visualizar Notebook do RoBERTa](https://nbviewer.org/github/amandajoioso/redes-neurais-discurso-odio/blob/main/notebooks/parte1_texto/Redes_Neurais_RoBERTa.ipynb)**

---

## Resultados da Parte 1 (Unimodal - Texto)

Nesta etapa, foram avaliados cinco modelos diferentes para a tarefa de classificação binária ("Hate" vs "Não Hate"), incluindo modelos baseados em redes neurais tradicionais e em modelos de linguagem (LLMs). Cada notebook contém a implementação completa, incluindo pré-processamento, treinamento e teste de um desses modelos, permitindo comparar seus desempenhos de forma individual.

### Pré-processamento

Originalmente, o dataset conta com seis categorias diferentes: Não Hate, Racista, Sexista, Homofóbico, Religião e Outros. Ao analisar a distribuição das labels, observa-se uma grande predominância da classe "Não Hate", enquanto as demais estão distribuídas de forma desigual e com representatividade bem menor. 

<img src="https://github.com/user-attachments/assets/cbeee146-a371-40d8-a380-3509f24ef1e1" width="600" />

Por conta do desbalanceamento original, optou-se pela binarização das labels, ou seja, as categorias Racista, Sexista, Homofóbico, Religião e Outros foram agrupadas em uma única classe chamada Hate. Após essa transformação, a distribuição das classes ficou da seguinte forma:

<img src="https://github.com/user-attachments/assets/cf03be18-b292-442a-9a1e-ff20f3fb5ed4" width="600" />

Apesar dessa binarização, ainda existe um desbalanceamento significativo entre as classes. Por isso, foi aplicado um undersampling na classe majoritária para equilibrar a quantidade de exemplos entre as duas classes.

<img src="https://github.com/user-attachments/assets/6c301868-769f-4548-91a7-16146c9090cf" width="600" />

#### Tokenização

Os textos foram tokenizados de acordo com o modelo utilizado, respeitando os requisitos específicos de cada arquitetura.

### Treinamento dos modelos

Os modelos foram treinados conforme as especificações de cada um, adaptando os parâmetros e configurações quando necessário.

### Avaliação dos Modelos

#### BiLSTM_Word2Vec_Classifier

Uma abordagem com modelo BiLSTM (Bidirectional Long Short-Term Memory) e Word2Vec combina técnicas de aprendizado de máquina para o processamento de linguagem natural (PLN). O Word2Vec é um modelo de embedding que converte palavras em vetores numéricos densos, capturando relações semânticas entre elas com base em seu contexto. Já o BiLSTM é uma arquitetura de rede neural recorrente que processa sequências de texto em duas direções: uma do início para o fim e outra do fim para o início, permitindo que o modelo capture informações contextuais de longo alcance, tanto passadas quanto futuras. Juntas, essas abordagens possibilitam uma compreensão profunda e bidirecional do texto, sendo eficazes no nosso objetivo de análise de Hate Speech, em que a classificação pode depender do contexto.

Com o método de undersampling aplicado a nossa base de dados obtemos os seguintes resultados:

Acurácia: 0.6303

Precisão: 0.5741

Recall: 0.6390

F1-Score: 0.6048

Também plotamos uma matriz de confusão que demonstrou um bom equilíbrio entre verdadeiros positivos e verdadeiros negativos, indicando que o modelo conseguiu generalizar razoavelmente bem para ambas as classes.

#### BERT

Para a tarefa de detecção de discurso de ódio, foi escolhido testar tambem o modelo BERT (bert-base-uncased), uma arquitetura baseada em transformadores conhecido por seu bom desempenho em tarefas de classificação de texto.

A avaliação foi feita com a partição de teste, dando os seguintes resultados:

Acurácia: 0,666
Precisão: 0,616
Recall: 0,653
F1-score: 0,634

A matriz de confusão mostrou que o modelo teve um desempenho razoável nas duas classes ("Hate" e "Não Hate"), apesar de alguns erros de classificação. Também foi analisada a curva de perda (loss) por época, que indicou sinais de overfitting, com a perda de validação aumentando ao longo do tempo. No entanto, como foi utilizado o early stopping, o treinamento foi interrompido no momento certo para evitar que o modelo se ajustasse demais aos dados de treino.

#### RoBERTa

bla bla bla escreve alguma coisa do modelo, resultado etc

#### XLNet-Twitter-Analysis

bla bla bla escreve alguma coisa do modelo, resultado etc

#### Llama Meta Hate

A abordagem implementada utiliza o modelo pré-treinado Llama-3-8B-Distil-MetaHate, desenvolvido através de destilação de conhecimento a partir do modelo Llama-3-70B-Instruct. Este modelo especializado emprega metodologias Chain-of-Thought (CoT) para realizar análise contextual profunda de sentenças. O modelo passou por um processo de fine-tuning específico para detecção de hate speech, incorporando técnicas de Parameter-Efficient Fine-Tuning (PEFT) que mantêm alta performance com maior eficiência computacional.

Com o conjunto de dados de teste passados como input para o modelo obtivemos os seguintes resultados:

Acurácia: 0.5147
Precisão: 0.5084
Recall: 0.8511
F1-Score: 0.6365

A análise de performance revelou características interessantes do modelo. A matriz de confusão demonstrou um desequilíbrio significativo, com alta sensibilidade para detectar hate speech (recall de 85.11%) mas baixa especificidade para casos não-hate speech (17.93% de acurácia). O modelo apresentou uma tendência pronunciada para classificar textos como hate speech, resultando em 3.725 falsos positivos contra apenas 674 falsos negativos. Esta característica indica um comportamento conservador do modelo, priorizando a detecção de possíveis casos de discurso de ódio.


Abaixo, a tabela consolidada com os resultados finais no conjunto de teste.



### Análise e Conclusão da Parte 1

A análise comparativa revela que . Para a Parte 2, será utilizado o modelo [Modelo Vencedor] como base para a fusão com a modalidade de imagem.

---

## Parte 2 (Multimodal)

*(Esta seção será desenvolvida para a segunda entrega do trabalho.)*
