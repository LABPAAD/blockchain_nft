# Dataset

> Como foi feita a coleta de dados?

A API _OpenSea_ oferece uma variedade de pontos de acesso via API REST (end-
points), cada um fornecendo dados específicos sobre as colelções da plataforma, como
preços, histórico de transações e informações de propriedade. Desenvolvemos um coletor em _Python3_ para realizar requisições HTTP aos endpoints gratuitos da API REST
_OpenSea_. Utilizamos endpoints das versões 1 e 2 da API; entretanto, em 01/2024, a
versão 1 foi descontinuada, permanecendo apenas a versão 2. Os endpoints usados foram
/api/v1/collection/collection-name (endpoint-1), que solicita dados de uma colecção individual, e /api/v2/collections?chain=ethereum&limit=limit&next=next (endpoint-2), que
fornece uma lista de identificadores _(slug)_ de todas as coleções. Ressaltamos que a API
gratuita aplica limitações a requisições sem uma chave de acesso. Para este trabalho, solicitamos uma chave de acesso para fins de pesquisa, permitindo requisições de alto volume de dados.

Primeiramente, realizamos requisições no _endpoint_-2 para obter identificadores do maior número possível de coleções na plataforma. Em seguida, para cada coleção identificada, fizemos requisições no _endpoint_-1 para coletar seus metadados. Ao todo, coletamos 7.182.800 coleções, cada uma armazenada em um arquivo formato _JSON_, conforme o padrão da API _OpenSea_. Essas requisições foram realizadas entre 01/10/2023 e 31/11/2023, de modo que as coleções e seus metadados referem-se a esse período. Após a coleta, processamos os metadados. Inicialmente, selecionamos apenas coleções com o atributo _category_ definido em seu JSON, dado o foco do trabalho na categorização de coleções. Assim, das coleções coletadas, 427.788 possuíam este atributo. A _OpenSea_ define nove categorias distintas, conforme descrito na Tabela abaixo. A categoria é escolhida pelo autor da coleção no ato de sua criação, a partir das opções oferecidas pela plataforma. Com os metadados das coleções de NFT coletados em formato JSON, procedemos ao processamento desses dados. A tabela seguinte detalha os metadados extraídos.

**Tabela 1. Atributos contidos em metadados de coleções de NFTs extraídos da plataforma _OpenSea_}**

| **Atributo**    | **Descrição**                                                        |
| --------------- | -------------------------------------------------------------------- |
| _total-volume_  | Total de vendas no _OpenSea_ em ETH.                                 |
| _total-sales_   | Número total de transações de venda que ocorreram dentro da coleção. |
| _total-supply_  | Total de NFTs criados para uma coleção.                              |
| _num-owners_    | Número de proprietários de NFTs distintos na coleção.                |
| _average-price_ | Preço médio de venda dos itens da coleção no _OpenSea_.              |
| _num-reports_   | Número de relatórios de abuso no _OpenSea_ sobre NFTs da coleção.    |
| _market-cap_    | Capitalização de mercado da coleção no _OpenSea_.                    |
| _qtd-traits_    | Número de características visuais de todos os NFTs da coleção.       |
| _floor-price_   | Preço mínimo de venda dos NFTs da coleção no _OpenSea_.              |
| _qtd-editors_   | Quantidade de editores da coleção.                                   |
| _category_      | Categoria da coleção utilizada no _OpenSea_.                         |

Para mais detalhes confira o artigo

> Classificação de Coleções de NFTs Explorando Metadados e Aprendizagem de Máquina. In: COLÓQUIO EM BLOCKCHAIN E WEB DESCENTRALIZADA (CBLOCKCHAIN), 2. , 2024, Brasília/DF. Anais [...]. Porto Alegre: Sociedade Brasileira de Computação, 2024 . p. 50-55. DOI:
> [https://doi.org/10.5753/cblockchain.2024.3172](https://doi.org/10.5753/cblockchain.2024.3172)
