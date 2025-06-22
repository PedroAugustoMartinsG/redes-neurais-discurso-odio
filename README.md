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

## Resultados da Parte 1 (Unimodal - Texto)

Nesta etapa, foram avaliados 5 modelos diferentes para a tarefa de classificação binária ("Hate" vs "Não Hate").  Abaixo, a tabela consolidada com os resultados finais no conjunto de teste.


### Análise e Conclusão da Parte 1

A análise comparativa revela que . Para a Parte 2, será utilizado o modelo [Modelo Vencedor] como base para a fusão com a modalidade de imagem.

---

## Parte 2 (Multimodal)

*(Esta seção será desenvolvida para a segunda entrega do trabalho.)*
