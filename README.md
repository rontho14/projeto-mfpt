# Detecção e diagnóstico de falhas em rolamentos — dados MFPT

Projeto do 2º semestre de ECM514 — Ciência de Dados.

Usamos gravações reais de vibração de um rolamento em bancada para responder duas perguntas: o rolamento tem algum problema (detecção) e, se tem, qual é o defeito, na pista externa ou na pista interna (diagnóstico).

## Entregas

| Entrega | Onde está |
|---|---|
| Notebook revisado com relatório técnico | [MFPT_deteccao_diagnostico_revisado.ipynb](MFPT_deteccao_diagnostico_revisado.ipynb) · [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/rontho14/projeto-mfpt/blob/main/MFPT_deteccao_diagnostico_revisado.ipynb) |
| Versão anterior, preservada | [MFPT_deteccao_diagnostico.ipynb](MFPT_deteccao_diagnostico.ipynb) |
| Dados | [MFPT Fault Datasets no Kaggle](https://www.kaggle.com/datasets/emperorpein/mfpt-fault-datasets), baixados pelo próprio notebook |
| Vídeo (até 5 min) | a fazer |
| Slides | a fazer |

## Como rodar

Abra o notebook no Colab pelo botão acima e execute todas as células (Ambiente de execução → Executar tudo). O notebook baixa os dados sozinho e instala `kagglehub` caso o downloader não esteja disponível. A execução precisa de internet. As bibliotecas científicas são as fornecidas pelo Colab, e suas versões são impressas no início. As saídas salvas na revisão vieram de execução local com kernel novo; a conferência no Colab deve ser feita com **Executar tudo**.

## Resultados

Nos resultados principais, gravações inteiras são separadas entre treino e avaliação: uma gravação usada para avaliar nunca tem janelas no treino. A comparação exploratória com janelas sorteadas é identificada no notebook. As taxas da tabela abaixo são por janela, não por voto majoritário de gravação. Na detecção, cada rodada deixa uma gravação normal inteira de fora (3 rodadas) e os valores são médias. No diagnóstico, as gravações são divididas em 3 rodadas, e cada janela é classificada por um modelo que não viu a gravação dela.

| Dataset | Técnica | Tipo de falha identificada | Taxa de detecção (TPR) | Falso positivo (FPR) | Acurácia por classe |
|---|---|---|---|---|---|
| MFPT | Isolation Forest (detecção, medidas genéricas) | não se aplica | 0,889 | 0,014 | não se aplica |
| MFPT | Isolation Forest (detecção, medidas do ritmo do defeito) | não se aplica | 0,107 | 0,000 | não se aplica |
| MFPT | Distância com PCA (detecção, medidas genéricas) | não se aplica | 1,000 | 0,014 | não se aplica |
| MFPT | Distância com PCA (detecção, medidas do ritmo do defeito) | não se aplica | 0,990 | 0,028 | não se aplica |
| MFPT | Regressão logística / Random Forest (diagnóstico, medidas genéricas) | pista externa, pista interna | 0,942 | 0,083 | normal 0,917 · pista externa 0,859 · pista interna 1,000 |
| MFPT | Knn (k=3) (diagnóstico, medidas do ritmo do defeito) | pista externa, pista interna | 0,996 | 0,028 | normal 0,972 · pista externa 1,000 · pista interna 0,988 |

As matrizes de confusão completas estão na seção 5 do notebook, e a discussão na seção 7.

A revisão mantém modelos, features, limiares e a avaliação principal. Acrescenta uma tabela com as taxas de cada gravação, médias com peso igual por arquivo e cinco divisões fixas (seeds 11, 23, 37, 51 e 79) com a mesma seleção aninhada. A comparação exploratória de janelas sorteadas usa três folds, como a de gravações separadas. As faixas descrevem sensibilidade à partição, não intervalos de confiança; as cinco divisões reutilizam os mesmos arquivos. A redação distingue evidência observada de possíveis efeitos de carga, montagem ou sessão.

## Grupo

| Nome | RA |
|---|---|
| | |

## Uso de inteligência artificial

Usamos Claude (Anthropic) e Codex (OpenAI) como assistentes para escrever e revisar o código, rodar e conferir as análises, levantar referências e redigir a primeira versão dos textos. As decisões sobre o método, a revisão dos resultados e o texto final são do grupo.
