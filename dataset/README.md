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

[Veja a tabela e mais detalhes](https://sol.sbc.org.br/index.php/cblockchain/article/view/29606/29409)
