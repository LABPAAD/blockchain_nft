# Classificação de Coleções de NFT

A classificação de NFTs é uma tarefa importante para a sua comercialização mas dependente da definição do próprio autor, que pode se equivocar por inexperiência na área, ou da avaliação de um especialista.
Neste trabalho, analisamos classes de coleções de NFTs baseado em metadados dessas coleções extraídos do _OpenSea_, a maior plataforma de NFTs na atualidade.
Avaliamos a eficiência de aprendizagem de máquina supervisionada para aprender os atributos mais relevantes dessas coleções e classificá-las nas 9 categorias mais populares nessa plataforma.
Mostramos o quão desafiante é automatizar a classificação para auxiliar usuários e curadores da plataforma.

> Ferramentas (sklearn) e os modelos

Utilizamos um conjunto de classificadores para identificar de forma ternária as categorias de coleçõoes, considerando as duas maiores em número de coleções (i.e., _art_ e PFPs) e todas as demais categorias minoritárias em uma única classe, identificada como _outros_. Os modelos escolhidos foram: _Floresta Aleatória_ (RF), _K-Nearest Neighbors_ (KNN) e _Máquinas de Vetor de Suporte_ (SVM). Implementamos o balanceamento de classes utilizando _undersampling_, que remove aleatoriamente amostras da classe majoritária para igualar à minoritária, e _oversampling_, que suplementa as classes minoritárias com instâncias de dados sintéticos que seguem a distribuição das instâncias reais [Chawla et al. 2002].

Nossos experimentos foram realizados com as implementações de métodos de regressão da biblioteca _scikit-learn_ da linguagem _Python_ [[Pedregosa et al., 2011]](https://scikit-learn.org/stable/whats_new/v0.24.html).

Os métodos de aprendizado de máquina utilizados são:

- _Floresta Aleatória_ (RF)
- _Máquinas de Vetor de Suporte_ (SVM)
- _K-Nearest Neighbors_ (KNN) [[Drucker et al., 1997]](https://www.microsoft.com/en-us/research/people/cjdrucker/), [[Breiman, 2001]](https://www.stat.berkeley.edu/~breiman/RandomForests/cc_home.htm).

> Métodologia

Para avaliar os classificadores, dividimos a base de dados em 75% para treino e
25% para teste, treinando os classificadores com e sem balanceamento de classes.
[Mais detalhes](https://sol.sbc.org.br/index.php/cblockchain/article/view/29606/29409)

## Execução dos modelos

1. **Importação de Bibliotecas:**
   Importa bibliotecas necessárias, como pandas, numpy, matplotlib, e vários modelos de machine learning do scikit-learn.

2. **Leitura de Dados:**
   Lê o conjuntos de dados: "dataset_nft_collections.csv".
   Realiza algumas operações de pré-processamento nos dados.

3. **Random Forest:**
   Utiliza o modelo RandomForestRegressor para classificar as classes usando as características fornecidas em "dataset_nft_collections.csv".

4. **Support Vector Machine**
   Utiliza o modelo Support Vector Machine (SVM) com kernel linear para classificar as classes com as caracteísticas fornecidas em "dataset_nft_collections.csv"

5. **K-Nearest Neighbors:**
   Utiliza o modelo K-Nearest Neighbors (KNN) para prever as ocorrências criminais usando as características fornecidas em "dataset_features_users_POIs.csv".
   Usa LOO para validação cruzada.

6. **Analise dos Resultados:**
   Análise dos resultados atraves da matriz de confusão e resultados de classifcação dos modelos.

7. **Resumo de Métricas:**
   Calcula métricas como Precisão (P), Revocação (R), F1-score (F1), Acurácia (Acc) e F1-macro.

8. Observações

- Certifique-se de ter o ambiente apropriado configurado com as bibliotecas necessárias.
- Certifique-se de que os conjuntos de dados "dataset_nft_collections.csv" esteja disponível no mesmo diretório ou no Google Drive conforme esperado.
- Execute o código em um ambiente Python, como Jupyter Notebook ou Google Colab para ter mais flexibilidade nas execuções ou se preferir pode usar o arquivo "models.py".
- Pode também executar apenas o modelo especifico

## Resultados

Os resultados mostram que o modelo RF com _oversampling_ obteve um desempenho equilibrado em todas as métricas, destacando-se na classifição das categorias _art_ e _outros_. Comparativamente, os modelos KNN e SVM obtiveram desempenhos inferiores, especialmente na categoria _PFPs_, ao passo que _oversampling_ melhora o desempenho de
RF, tornando-o mais adequado para a classificação ternária.

**Tabela 1. Desempenho do modelos avaliados para a classe Art com as métricas Precisão (P), Revocação (R), F1-score (F1), Acurácia (Acc) e F1-macro.**
| aa | Art | | | Acc | F1-macro |
|:-------|:----------:|:----------:|:----------:|:----------:|:----------:|
| Modelos | P | R | F1 | | | | | | |
| KNN | 0,70 | 0,68 | 0,69 | 0,61| 0,50|
| SVM | 0,68 | 0,87 | 0,76 | 0,67| 0,50|
| RF (oversampling) | 0,72 | 0,72 | 0,72 | 0,64| 0,56|

**Tabela 2. Desempenho do modelos avaliados para a classe PFPs com as métricas Precisão (P), Revocação (R), F1-score (F1), Acurácia (Acc) e F1-macro.**
| aa | Art | | | Acc | F1-macro |
|:-------|:----------:|:----------:|:----------:|:----------:|:----------:|
| Modelos | P | R | F1 | | | | | | |
| KNN | 0,38 | 0,20 | 0,26 | 0,61| 0,50|
| SVM | 0,60 | 0,09 | 0,16 | 0,67| 0,50|
| RF (oversampling) | 0,30 | 0,45 | 0,36 | 0,64| 0,56|

**Tabela 3. Desempenho do modelos avaliados para a classe Outros com as métricas Precisão (P), Revocação (R), F1-score (F1), Acurácia (Acc) e F1-macro.**
| aa | Art | | | Acc | F1-macro |
|:-------|:----------:|:----------:|:----------:|:----------:|:----------:|
| Modelos | P | R | F1 | | | | | | |
| KNN | 0,51 | 0,61 | 0,56 | 0,61| 0,50|
| SVM | 0,67 | 0,51 | 0,58 | 0,67| 0,50|
| RF (oversampling) | 0,65 | 0,54 | 0,69 | 0,64| 0,56|
