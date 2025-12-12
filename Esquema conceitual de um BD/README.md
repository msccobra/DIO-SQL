# Esquema conceitual de um BD

A idéia deste projeto é fazer um projeto simples para um BD de uma oficina/concessionária. Para tal, fiz esse projeto com oito tabelas: Cliente, Veículo, Orçamento, Ordem de Serviço, Responsável e Pagamento, além das tabelas que são provenientes dos relacionamentos que eu defini no meu modelo, Execução de OS e Orçamento has Responsável.

### Cliente

Esta tabela trata a respeito da identificação do cliente, portanto possui como PK a sua identificação (número interno), que também é uma chave única, além de entredas paar seu nome, seu CPF (única) e seu telefone.

### Produto

É uma tabela relacionada à identificação do produto, composta pelos valores de SKU (INT), quantidade em estoque (INT), valor (FLOAT), departamento (INT) e descrição (LONGTEXT). O Workbench importou algumas FK da tabela Clientes devido ao relacionamento 1:N entre as tabelas, onde 1 cliente pode escolher diversos produtos. Há também um relacionamento N:M com a tabela Entrega. Escolhi esse tipo de relacionamento, pois, não necessariammente, todos os produtos serão despachados no mesmo pacote/lote ao cliente, devido a restrições de tamanho e disponibilidade.

### Entrega

Essa tabela possui identificadores relacionados ao processo de despacho das mercadorias ao cliente, sendo composta por: Tipo de entrega (INT/PK), que pode ser realacionada a entrega comum ou expressa, ID transportadora (INT), endereço e CEP, que são FKs importadas da tabela de clientes e prazo (INT)

### Pagamento

Essa tabela é composta integralmente de chaves estrangeiras, advindas das tabelas de Ordem de Serviço, de onde foi importado o número da OS, que é a PK dessa tabela. Dessa maneira, é possível sabermos todos os dados relacionados a ela, desde informações sobre o veículo e seu dono, até o tipo de serviço e descrição do mesmo. Outra FK que foi importada foi o valor, também de Ordem de Serviço. Pode parecer redundante, já que a chave anteriormente descrita, por ser uma PK, já traz todas as informações consigo, mas optei por essa redundância. A outra entrada dessa tabela é referente ao id do cliente, que poderia ser obtida através do número da OS, mas por uma questão de facilidade, decidi colocá-la também.


Dessa maneira, o esquema descrito acima pode ser visto na figura:


![esquema](https://github.com/msccobra/DIO-SQL/blob/main/Esquema%20conceitual%20de%20um%20BD/oficina.png)
