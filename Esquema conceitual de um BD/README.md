# Design inicial de um BD simples para um e-commerce

A idéia deste projeto é fazer um projeto simples para um BD de um e-commerce. Para tal, fiz apenas quatro tabelas de entidades: Cliente, Produto, Entrega e Pagamento, as quais detalharei a seguir.

### Cliente

Esta tabela trata a respeito da identificação do cliente, portanto possui como PK seu nome e sua identificação, que também é uma chave única, podendo ser CPF ou CNPJ. Há também os localçizadores, como o endereço e o CEP, além de uma entrada, do tipo INT, relacionada ao tipo de cliente (p.ex: 0 para PF e 1 para PJ).

### Produto

É uma tabela relacionada à identificação do produto, composta pelos valores de SKU (INT), quantidade em estoque (INT), valor (FLOAT), departamento (INT) e descrição (LONGTEXT). O Workbench importou algumas FK da tabela Clientes devido ao relacionamento 1:N entre as tabelas, onde 1 cliente pode escolher diversos produtos. Há também um relacionamento N:M com a tabela Entrega. Escolhi esse tipo de relacionamento, pois, não necessariammente, todos os produtos serão despachados no mesmo pacote/lote ao cliente, devido a restrições de tamanho e disponibilidade.

### Entrega

Essa tabela possui identificadores relacionados ao processo de despacho das mercadorias ao cliente, sendo composta por: Tipo de entrega (INT/PK), que pode ser realacionada a entrega comum ou expressa, ID transportadora (INT), endereço e CEP, que são FKs importadas da tabela de clientes e prazo (INT)

### Pagamento

Por fim, criei uma tabela relacionada ao pagamento, composta por: modo de pagamento (INT/PK), parcelamento (INT), que poderia ter o formato 0 para pagamento à vista e 1 para pagamento parcelado, número de parcelas (INT), que segue o mesmo modelo, com 1 sendo pagamento à vista e assim em diante, número do cartão, que aceita valores nulos, e.g, no caso de pagamento por Pix ou boleto, não há necessidade de armazenar-se esse valor e foram importados os registros de nome e identificação de cliente da tabela homônima, por conmsequência de seu relacionamento 1:1, pois nesse caso optei que o cliente possa apenas usar um meio de pagamento por compra.

Dessa maneira, o esquema descrito acima pode ser visto na figura:


![esquema]()
