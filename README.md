# Detecção e diagnóstico de falhas em rolamentos — dados MFPT

Projeto do 2º semestre de ECM514 — Ciência de Dados.

Usamos gravações reais de vibração de um rolamento em bancada para responder duas perguntas: o rolamento tem algum problema (detecção) e, se tem, qual é o defeito, na pista externa ou na pista interna (diagnóstico).

## Entregas

| Entrega | Onde está |
|---|---|
| Notebook com o relatório técnico (roda no Colab) | [MFPT_deteccao_diagnostico.ipynb](MFPT_deteccao_diagnostico.ipynb) · [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/rontho14/projeto-mfpt/blob/main/MFPT_deteccao_diagnostico.ipynb) |
| Dados | [MFPT Fault Datasets no Kaggle](https://www.kaggle.com/datasets/emperorpein/mfpt-fault-datasets), baixados pelo próprio notebook |
| Vídeo (até 5 min) | a fazer |
| Slides | a fazer |

## Como rodar

Abra o notebook no Colab pelo botão acima e execute todas as células (Ambiente de execução → Executar tudo). O notebook baixa os dados sozinho.

## Resultados

| Dataset | Técnica | Tipo de falha identificada | Taxa de detecção (TPR) | Falso positivo (FPR) | Acurácia por classe |
|---|---|---|---|---|---|
| MFPT | Distância com PCA, medidas do ritmo do defeito | não se aplica | 0,968 | 0,000 | não se aplica |
| MFPT | Distância com PCA, medidas genéricas | não se aplica | 1,000 | 0,095 | não se aplica |
| MFPT | Isolation Forest, medidas genéricas | não se aplica | 0,905 | 0,000 | não se aplica |
| MFPT | Isolation Forest, medidas do ritmo do defeito | não se aplica | 0,032 | 0,000 | não se aplica |
| MFPT | Knn (k=3), medidas do ritmo do defeito | normal, pista externa, pista interna | | | normal 1,000 · pista externa 1,000 · pista interna 0,952 |
| MFPT | Random Forest, medidas genéricas | normal, pista externa, pista interna | | | normal 1,000 · pista externa 1,000 · pista interna 1,000 |

As matrizes de confusão completas estão na seção 5 do notebook.

No diagnóstico, o teste usa trechos das mesmas gravações vistas no treino. Numa gravação nova, a validação cruzada separada por gravação dá 99,5% de acerto com as medidas do ritmo do defeito e 92% com as medidas genéricas. A discussão está na seção 6 do notebook.

## Grupo

| Nome | RA |
|---|---|
| | |

## Uso de inteligência artificial

Usamos o Claude (Anthropic) como assistente para escrever e revisar o código, rodar e conferir as análises, levantar referências e redigir a primeira versão dos textos. As decisões sobre o método, a revisão dos resultados e o texto final são do grupo.
