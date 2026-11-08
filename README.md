# Detecção e diagnóstico de falhas em rolamentos — dados MFPT

Projeto do 2º semestre de ECM514 — Ciência de Dados.

Usamos gravações reais de vibração de um rolamento em bancada para responder duas perguntas: o rolamento tem algum problema (detecção) e, se tem, qual é o defeito, na pista externa ou na pista interna (diagnóstico).

## Entregas

| Entrega | Onde está |
|---|---|
| Notebook com relatório técnico | [MFPT_deteccao_diagnostico.ipynb](MFPT_deteccao_diagnostico.ipynb) · [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/rontho14/projeto-mfpt/blob/main/MFPT_deteccao_diagnostico.ipynb) |
| Dados | [MFPT Fault Datasets no Kaggle](https://www.kaggle.com/datasets/emperorpein/mfpt-fault-datasets), baixados pelo próprio notebook |
| Vídeo (até 5 min) | a fazer |
| Slides | a fazer |

## Como rodar

Abra o notebook no Colab pelo botão acima e execute todas as células (Ambiente de execução → Executar tudo). O notebook baixa os dados sozinho e instala `kagglehub` caso o downloader não esteja disponível. A execução precisa de internet. As bibliotecas científicas são as fornecidas pelo Colab, e suas versões são impressas no início.
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

As matrizes de confusão completas, por janela e por gravação, estão na seção 5 do notebook, a exploração na seção 6 e a discussão na seção 8.

Além da avaliação principal, o notebook traz análises de sensibilidade, todas nas mesmas gravações e sem trocar o resultado principal:

- **Limite de alerta e curva ROC.** As notas dos detectores separam bem defeito de normal (AUC média de 0,969 a 1,000). Com as medidas do ritmo, o Isolation Forest ordena bem as janelas, mas detecta poucas falhas com o limite principal. Reduzir o limite aumenta a detecção e também os falsos alarmes; a análise das pontuações é compatível com saturação fora da faixa de treino.
- **Voto por gravação.** Pelo voto da maioria das janelas, as medidas do ritmo acertam as 20 gravações e as genéricas 18.
- **Busca de hiperparâmetros.** A busca em grade dentro da avaliação por gravação não melhorou o diagnóstico (84,6% e 98,7% por janela, contra 91,0% e 99,0%).
- **Tamanho da janela.** Com 0,1, 0,25 e 0,5 s, o ritmo do defeito fica mais nítido em janelas longas, ao custo de menos janelas normais e mais alarme falso.
- **KMeans.** Sem usar as classes, separa a pista interna sozinha e junta as normais com parte da pista externa.
- **Cinco divisões fixas das gravações.** Mostram a sensibilidade à partição; não são intervalos de confiança.

## Grupo

| Nome | RA |
|---|---|
| | |

## Uso de inteligência artificial

Usamos Claude (Anthropic) e Codex (OpenAI) como assistentes para escrever e revisar o código, rodar e conferir as análises, levantar referências e redigir a primeira versão dos textos. As decisões sobre o método, a revisão dos resultados e o texto final são do grupo.
