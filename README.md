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

Todas as avaliações são feitas por gravação: uma gravação usada para avaliar nunca tem janelas no treino. Na detecção, cada rodada deixa uma gravação normal inteira de fora (3 rodadas) e os valores são médias. No diagnóstico, as gravações são divididas em 3 rodadas, e cada janela é classificada por um modelo que não viu a gravação dela.

| Dataset | Técnica | Tipo de falha identificada | Taxa de detecção (TPR) | Falso positivo (FPR) | Acurácia por classe |
|---|---|---|---|---|---|
| MFPT | Isolation Forest (detecção, medidas genéricas) | não se aplica | 0,889 | 0,014 | não se aplica |
| MFPT | Isolation Forest (detecção, medidas do ritmo do defeito) | não se aplica | 0,107 | 0,000 | não se aplica |
| MFPT | Distância com PCA (detecção, medidas genéricas) | não se aplica | 1,000 | 0,014 | não se aplica |
| MFPT | Distância com PCA (detecção, medidas do ritmo do defeito) | não se aplica | 0,990 | 0,028 | não se aplica |
| MFPT | Regressão logística / Random Forest (diagnóstico, medidas genéricas) | pista externa, pista interna | 0,942 | 0,083 | normal 0,917 · pista externa 0,859 · pista interna 1,000 |
| MFPT | Knn (k=3) (diagnóstico, medidas do ritmo do defeito) | pista externa, pista interna | 0,996 | 0,028 | normal 0,972 · pista externa 1,000 · pista interna 0,988 |

As matrizes de confusão completas estão na seção 5 do notebook, e a discussão na seção 7.

## Grupo

| Nome | RA |
|---|---|
| | |

## Uso de inteligência artificial

Usamos o Claude (Anthropic) como assistente para escrever e revisar o código, rodar e conferir as análises, levantar referências e redigir a primeira versão dos textos. As decisões sobre o método, a revisão dos resultados e o texto final são do grupo.
