# Status

## Aguardando separação de mercadoria


Se todos os itens constarem com estoque positivo de acordo com a quantidade pedida:

* Este pedido será importado via interface (webservice) para o sistema WMS (WIS) e entra em processo de separação pela equipe de logística.

* Nos itens de DropShipping serão somente bipadas as etiquetas que estarão expostas em uma pasta na central de operações e liberado este pedido para faturamento (por não constar o item fisicamente no estoque). O mesmo é encaminhado para o faturamento onde o faturamento irá digitar o DK manualmente e assim faturados de acordo com o processo existente. 

* A nota fiscal de venda em XML deve ser enviada imediatamente para o cliente juntamente com e-mail informativo abaixo, caso haja mais de um produto no pedido sendo um de DropShipping e outro item comum Connect:
> _**Assunto**: Informações sobre seu pedido **XXXXXX**_
>
>_“Olá, Fulano_
>
>_Somos da ConnectParts e informamos que seu pedido com número 12, por questões operacionais relativas a logística é possível que a postagem e entrega dos produtos ocorram em dias diferentes._
>
>_Por favor não responda esse e-mail, para maiores informações, entre em contato conosco pelos nossos canais de atendimento._
>
>_Equipe Connect Parts! ”_

**Obs:** Lembrando que será enviado o e-mail somente no faturamento da primeira NF do pedido e somente quando houver um produto DropShipping. A Danfe (nota fiscal em papel) pode ser descartada em caso de venda onde possui apenas produto DropShipping.


## Estoque reservado parcialmente

Pedido onde contém mais de um item e um dos itens são pendências (não temos em estoque para faturamento:


1. Central de Operações deverá acompanhar nos ábacos os pedidos que contém pendências ConnectParts através dos pedidos XXX-DROP para fazer a tratativa abaixo:

    2. Após passar pela pré analise e ser aprovado este cairá na pendencia por não constar quantidade em estoque do item Connect, este pedido passara por analise na central de operações e o mesmo deverá ser liberado parcialmente nos ábacos através da tela liberar pedidos reservados parcialmente no menu Comercial e Faturamento -> Movimentações -> Pedidos -> Análise de estoque -> liberar pedidos reservados parcialmente.
    3. Este pedido será enviado ao WMS apenas os itens que possuímos em estoque. Ao faturar o pedido liberado, será gerado um novo pedido no Ábacos com os mesmos números, este pedido possuirá apenas o item sem estoque.
    4. O pedido do item faltante entrará no status aguardando confirmação de pagamento e, assim que for liberado pela pré análise entrará no status aguardando estoque e deverá ser tratado pela equipe de atendimento conforme fluxo existente, para consulta no abaquinhos e ábacos, informa o número do pedido ou CPF do cliente que retornara os dois.
    5. Será faturado uma nota de venda somente como item que conter saldo.
    6. Futuramente quando chegar o produto Connect que estava em pendência, após dado entrada no sistema será emitida uma nova nota fiscal.

7. Pedidos contendo produto CONNECT e produto DROP ou contendo apenas produto DropShipping, porém a pendência é de produto Dropshipping:

    8. Quando notificarmos o FORNECEDOR com o pedido de compra e não houver estoque, através de webservice o fornecedor deverá comunicar pedidos que não possuem estoque e sua previsão de atendimento.
    9. Na Sales force existe uma fila chamada Pendências – DropShipping, onde ouvidoria tratará e nessa fila irá conter tickets relacionados a cada pedido que conter pendências com itens de DropShipping. Nesses tickets haverão as seguintes informações: (1. Número do pedido; 2. Item em pendência (código do item); 3. Data de Previsão 4. Status (DTS ira nos informar o motivo pelo qual não tem o produto), para que o responsável no atendimento siga com as tratativas ao cliente e então orientar a Central de Operações o que deverá ser feito com o pedido.
