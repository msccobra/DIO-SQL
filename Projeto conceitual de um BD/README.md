# Design inicial de um BD simples para um e-commerce

A idéia deste projeto é fazer um projeto simples para um BD de um e-commerce. Para tal, fiz apenas quatro tabelas de entidades: Cliente, Produto, Entrega e Pagamento, as quais detalharei a seguir.

### Cliente

Esta tabela trata a respeito da identificação do cliente, portanto possui como PK seu nome e sua identificação, que também é uma chave única, podendo ser CPF ou CNPJ. Há também os localçizadores, como o endereço e o CEP, além de uma entrada, do tipo INT, relacionada ao tipo de cliente (p.ex: 0 para PF e 1 para PJ).

### Produto

É uma tabela relacionada à identificação do produto, composta pelos valores de SKU (INT), quantidade em estoque (INT), valor (FLOAT), departamento (INT) e descrição (LONGTEXT). O Workbench importou algumas FK da tabela Clientes devido ao relacionamento 1:N entre as tabelas, onde 1 cliente pode escolher diversos produtos.

