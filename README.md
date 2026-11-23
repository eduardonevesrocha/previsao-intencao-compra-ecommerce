# Previsão de intenção de compra em e-commerce

Projeto prático de classificação da disciplina CIN0209 Aprendizado de Máquina 1 (CIn/UFPE, 2026.2), Prof. Leandro Maciel Almeida.

**Dupla:** Eduardo Neves e Wallace Santana

[![Abrir a Entrega 2 no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Kxut_kjA3RjyU5claOY9W4M8MOixOe64)

## Pergunta

Olhando só para o comportamento de navegação de uma sessão, dá para prever se ela termina em compra?

## Dados

[Online Shoppers Purchasing Intention Dataset](https://archive.ics.uci.edu/dataset/468/online+shoppers+purchasing+intention+dataset), UCI (id 468), Sakar et al., 2018. São 12.330 sessões, 17 atributos (11 numéricos e 6 categóricos) e o alvo `Revenue`, com 15,5% de compras. Os dados são baixados direto do UCI pelo pacote `ucimlrepo`, então não há arquivo de dados no repositório.

## Protocolo

- Divisão 60/20/20 estratificada com semente 42 (7.398 / 2.466 / 2.466), a mesma nas duas entregas.
- Desenvolvimento = treino + validação (9.864 sessões), com validação cruzada estratificada de 5 folds.
- Pré-processamento (`OneHotEncoder` e `StandardScaler`) dentro do `Pipeline`, ajustado em cada fold.
- Métrica principal: acurácia balanceada, escolhida antes da busca.
- Teste avaliado uma única vez, depois da declaração dos campeões (registrado em `test_log.csv`).

## Resultados

| Família | CV (acc. balanceada, média ± EP) | Teste |
|---|---|---|
| Árvore de decisão | 0,854 ± 0,003 | **0,839** |
| Regressão logística | 0,820 ± 0,008 | 0,803 |
| Perceptron | 0,773 ± 0,011 | 0,774 |
| Naive Bayes | 0,751 ± 0,006 | 0,728 |
| MLP | 0,757 ± 0,008 | 0,722 |
| kNN | 0,689 ± 0,004 | 0,657 |

Campeão: árvore de decisão com `max_depth=4` e `class_weight='balanced'`. No teste, encontra 83,2% das compras e acerta 84,6% das não compras, com precisão de 49,8% na classe compra.

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `notebooks/entrega1_exploracao_baselines.ipynb` | Entrega 1: exploração dos dados e baselines |
| `notebooks/entrega2_comparacao_modelos.ipynb` | Entrega 2: comparação das seis famílias, estudo de overfitting e avaliação no teste |
| `docs/relatorio_entrega2.pdf` | Notebook da Entrega 2 em PDF, com as saídas |
| `docs/slides_seminario.pdf` | Slides do seminário final |

## Como executar

Abra `notebooks/entrega2_comparacao_modelos.ipynb` no Google Colab e use *Ambiente de execução → Executar tudo*. A execução completa leva cerca de 7 minutos. A célula do teste não reavalia o teste se o resultado já estiver salvo.

## Uso de IA

Usamos o Claude (Anthropic) como apoio na estrutura do notebook, no código do protocolo e na redação. A declaração completa está na Seção 11 do notebook da Entrega 2.
