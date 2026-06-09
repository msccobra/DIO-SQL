# Construindo seu Primeiro Projeto Lógico de Banco de Dados

O desafio da vez consistia em passar o modelo EER de um e-commerce para o modelo de um BD em si, com a definição e população (persistência de dados) das tabelas, definições de PK e FK, garantindo a integridade referencial do BD.

Eu remodelei o esquema do BD da tarefa anterior, para que não houvesse necessidade de queries muito extensas, conforme figura abaixo. Eu procurei fazer esse BD com pouca, se alguma,  É bom que se diga que eu criei o EER relativo ao meu BD de maneira automática, com a função 'Reverse Engineering' do Workbench, pois, a fim de remodelar o que havia antes, já fui criando as tabelas e relacionamentos necessarios diretamente, apenas baseando-me no EER anterior e fazendo as modificações necessárias.

![esquema](https://github.com/msccobra/DIO-SQL/blob/main/Projeto%20l%C3%B3gico%20de%20um%20BD/ecommerce.png)

Na questão dos dados persistidos, populei algumas das tabelas com cerca de 5 entradas, para que fosse possível fazer-se as queries mais complexas. Alguns exemplos de queries estão logo abaixo:


Nesse primeiro exemplo, apenas fiz alguns joins em sequência, a informação retornada não foi de grande utilidade. No caso, o número de clientes que pagaram por boleto ou por cartão, a soma dos valores de todas as compras em cada modalidade de pagamento e as médias por compra em cada modalidade. 
```
select round(sum(c.valor), 2) as soma, round(avg(c.valor), 2) as média, p.Tipo_pagamento, count(p.tipo_pagamento)
from pagamento p
right join compra_efetuada c
on p.id_compra = c.id_compra
right join cliente cl
on cl.id_cliente = c.id_cliente
group by p.Tipo_pagamento;
```

Já na segunda query, quis descobrir a quantidade de produtos do tipo 'lgoled65g5' vendidos. Vendo essa query, terei de reformular essa parte do schema, pois as consultas estão demasiadamente complexas para a obtenção de algo tão simples. O ifnull foi necessário, pois valor default da tabela estava em null, em vez de zero, outra coisa a ser corrigida no futuro.

```
select ifnull(quantidade1,0) + ifnull((select quantidade2
from compra_efetuada c
where sku2 = 'lgoled65g5'),0) +  ifnull((select quantidade3
from compra_efetuada c
where sku3 = 'lgoled65g5'),0) as 'Soma total'
from compra_efetuada
where sku1 = 'lgoled65g5';
```
Alternativamente:
```
SELECT
    ifnull((SELECT SUM(quantidade1) FROM compra_efetuada WHERE sku1 = 'lgoled65g5'), 0) +
    ifnull((SELECT SUM(quantidade2) FROM compra_efetuada WHERE sku2 = 'lgoled65g5'),0) +
    ifnull((SELECT SUM(quantidade2) FROM compra_efetuada WHERE sku3 = 'lgoled65g5'),0) AS soma_total;
```


A terceira query tem alguns joins e uma cláusula group by, e serviu para ver todas as compras de cada cliente cadastrado, seu valor e o tipo de pagamento efetuado:

```
select p.id_compra, cl.nome, cl.tipo_cliente as 'PF=1, PJ=2', ce.valor, p.tipo_pagamento as '1=cartão, 2=boleto', p.parcelas
from compra_efetuada ce
right join cliente cl
on ce.id_cliente = cl.id_cliente
left join pagamento p
on ce.id_compra = p.id_compra
order by ce.valor desc;
```

# Construindo seu Primeiro Projeto Lógico de Banco de Dados v2

Para essa tarefa, fiz algumas modificações na estrutura do banco de dados, de maneira a facilitar as consultas e inserção de dados. Foi mudada a estrutura das inserções das compras e produtos associados a elas. Antes, cada compra era limitada a três produtos, agora o número de produtos é ilimitado. É aberto um id_compra na tabela compra_efetuada e daí serão adicionados os produtos comprados, com seu respectivo id_compra através da tabela item_compra. Facilitou e escalou bastante esse processo. Dessa maneira, o EER mudou para o formato da figura abaixo:

![ecommercev3](https://github.com/msccobra/DIO-SQL/blob/main/Projeto%20l%C3%B3gico%20de%20um%20BD/ecommerce%20v3.png)
