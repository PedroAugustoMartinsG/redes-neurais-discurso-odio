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

####Pré-processamento

Originalmente, o dataset conta com seis categorias diferentes: Não Hate, Racista, Sexista, Homofóbico, Religião e Outros. Ao analisar a distribuição das labels, observa-se uma grande predominância da classe "Não Hate", enquanto as demais estão distribuídas de forma desigual e com representatividade bem menor. 

<img src="https://github.com/user-attachments/assets/cbeee146-a371-40d8-a380-3509f24ef1e1" width="600" />

Por conta do desbalanceamento original, optou-se pela binarização das labels, ou seja, as categorias Racista, Sexista, Homofóbico, Religião e Outros foram agrupadas em uma única classe chamada Hate. Após essa transformação, a distribuição das classes ficou da seguinte forma:

<img src="https://github.com/user-attachments/assets/cf03be18-b292-442a-9a1e-ff20f3fb5ed4" width="600" />

Apesar dessa binarização, ainda existe um desbalanceamento significativo entre as classes. Por isso, foi aplicado um undersampling na classe majoritária para equilibrar a quantidade de exemplos entre as duas classes.

<img src="https://github.com/user-attachments/assets/6c301868-769f-4548-91a7-16146c9090cf" width="600" />


Abaixo, a tabela consolidada com os resultados finais no conjunto de teste.



### Análise e Conclusão da Parte 1

A análise comparativa revela que . Para a Parte 2, será utilizado o modelo [Modelo Vencedor] como base para a fusão com a modalidade de imagem.

---

## Parte 2 (Multimodal)

*(Esta seção será desenvolvida para a segunda entrega do trabalho.)*
