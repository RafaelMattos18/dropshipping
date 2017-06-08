# Aguardando estoque

Caso esse pedido seja uma pendência ele deverá estar na fila de tickets da Sales Force(Drop-Pendência) para ser tratado como pendência e seguir com a tratativa devida, caso contrário ele está com esse status pois está aguardando recebimento fiscal dar entrada e então seguir o faturamento.

## Pedidos DROP em pendência

Quando notificarmos o fornecedor com o pedido de compra e não houver estoque, através de webservice o fornecedor deverá comunicar pedidos que não possuem estoque e sua previsão de atendimento.

Na Sales force existe uma fila chamada Pendências–Drop, onde ouvidoria tratará e nessa fila irá conter tickets relacionados a cada pedido que conter pendências com itens de DropShipping. Nesses tickets haverá as seguintes informações: (1. Número do pedido; 2. Item em pendência (código do item); 3. Data de Previsão 4. Status (fornecedor ira nos informar o motivo pelo qual não tem o produto), para que o responsável no atendimento siga com as tratativas ao cliente.
