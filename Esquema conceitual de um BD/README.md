# Esquema conceitual de um BD

A idéia deste projeto é fazer um projeto simples para um BD de uma oficina/concessionária. Para tal, fiz esse projeto com oito tabelas: Cliente, Veículo, Orçamento, Ordem de Serviço, Responsável e Pagamento, além das tabelas que são provenientes dos relacionamentos que eu defini no meu modelo, Execução de OS e Orçamento has Responsável.

### Cliente

Esta tabela trata a respeito da identificação do cliente, portanto possui como PK a sua identificação (número interno), que também é uma chave única, além de entredas para seu nome, seu CPF (única) e seu telefone.

### Veículo

É uma tabela relacionada à identificação do veículo, composta pelo seu id que é a PK, além de outras informações como marca, modelo e ano, além de uma chave importada, que é o idCliente, advinda do relacionamento 1:N entre essas tabelas.

### Orçamento

Essa tabela é relacionada ao orçamento feito para o serviço ou conjunto de serviços a serem feitos (ou não) no veículo. Desas maneira, sua PK é o número do orçamento, e para cada orçamento há diversas chaves descritivas, como: tipo de serviço, que pode ser revisão, emergência ou troca simples; temos o ID responsável, que é uma identificação interna sobre o funcionário que fará a avaliação (não necessariamente é o mesmo responsável pela execução do serviço, por isso não foi uma chave importada), tem o id do veículo, que é uma chave estrangeira, advinda de um relacionamento 1:1 entre a tabela orçamento e a tabela veículo, há também duas chaves descritivas dos serviços (em formato LONGTEXT), que são a descrição dos serviços e a lista de peças, o valor, que um float e o status de aprovação do orçamento, que pode ser total, parcial ou negativo.


### Pagamento

Essa tabela é composta integralmente de chaves estrangeiras, advindas das tabelas de Ordem de Serviço, de onde foi importado o número da OS, que é a PK dessa tabela. Dessa maneira, é possível sabermos todos os dados relacionados a ela, desde informações sobre o veículo e seu dono, até o tipo de serviço e descrição do mesmo. Outra FK que foi importada foi o valor, também de Ordem de Serviço. Pode parecer redundante, já que a chave anteriormente descrita, por ser uma PK, já traz todas as informações consigo, mas optei por essa redundância. A outra entrada dessa tabela é referente ao id do cliente, que poderia ser obtida através do número da OS, mas por uma questão de facilidade, decidi colocá-la também.


Dessa maneira, o esquema descrito acima pode ser visto na figura:


![esquema](https://github.com/msccobra/DIO-SQL/blob/main/Esquema%20conceitual%20de%20um%20BD/oficina.png)
