## Aguardando Estoque

Caso esse pedido seja uma pendência ele deverá estar na fila de tickets da Sales Force(Drop-Pendência) para ser tratado como pendência e seguir com a tratativa devida, caso contrário ele está com esse status pois está aguardando recebimento fiscal dar entrada e então seguir o faturamento.

### Pedidos DROP em pendência

* Quando notificarmos o fornecedor com o pedido de compra e não houver estoque, através de webservice o fornecedor deverá comunicar pedidos que não possuem estoque e sua previsão de atendimento.

* Na Sales force existe uma fila chamada Pendências – Drop, onde ouvidoria tratará e nessa fila irá conter tickets relacionados a cada pedido que conter pendências com itens de DropShipping. Nesses tickets haverá as seguintes informações: (1. Número do pedido; 2. Item em pendência (código do item); 3. Data de Previsão 4. Status (fornecedor ira nos informar o motivo pelo qual não tem o produto), para que o responsável no atendimento siga com as tratativas ao cliente.

* O atendimento entra em contato com o cliente com a previsão de entrega para o mesmo decidir se mantém o pedido, cancela ou gera o vale crédito.

* Após o fluxo ConnectParts ser concluído, é enviado ao fornecedor a nota fiscal faturada da ConnectParts (via webservice) para que o mesmo possa emitir a nota de Remessa por conta e ordem de terceiros que deve referenciar nos dados adicionais o número da nota fiscal de venda sendo necessário o fornecedor enviar uma cópia da nf de Remessa para a ConnectParts, para que possamos encaminhar um e-mail para o cliente com informações do rastreamento da transportadora, que será enviado 24hs após o fornecedor nos enviar a NF de Remessa.

* Assim que o fornecedor nos enviar a NF de Remessa, devemos enviar para a transportadora a nossa NF faturada, com os seguintes dados:

    _Enviar para:  pesquisa2.320@rte.com.br / rte320@rte.com.br   e flaviolisse@rte.com.br_
    
    >**Dados de Destinatário:**
    **Nome**: Paula Coradi, **CPF**: 00033323347862
    **Endereço**: Rua Diogo Melhado, **Bairro**: Jardim Luciana, **Número**: 515
    **CEP**: 17514310, **Município**: MARILIA, **Estado**: SP
    >
    >**Dados da Nota Fiscal:**
    **Número**: 400261, **Série**: 4, **Data Emissão**: 20/04/2017 16:49:19
    **Chave**: 35170408677036000116550040004002611505081997
    **Natureza**: VENDA DE PRODUTOS
    **CNPJ**: 08677036000116, Inscrição Estadual: 438241764116
    **Valor da NF**: 341,61
    **Peso Bruto**: 4,9, **Peso Liquido**: 4,9
    **Quantidade de Volumes:** 1, CFOP: 5405
    

Após concluído o faturamento de ambas as partes o fornecedor começa o processo logístico juntamente com as transportadoras, que deverão coletar os produtos. A coleta é realizada pela transportadora **Rodonaves** de Segunda/ Quarta das 14 até as 16hs e de Sexta das 14 até as 15:30hs. E a transportadora irá disponibilizar via API seu código de rastreio para que seja consumido pelos ERPs ou integradores e enviados por e-mail para o cliente acompanhar o trajeto da mercadoria.

> **Atenção:** Em caso de pendência que o atendimento entrar em contato com o cliente para informa-lo e o mesmo quiser cancelar, o atendente deverá seguir o fluxo normal de cancelamento (ticket Sales force, cancelar ERP, plataformas, devoluções...) porém o atendente deverá cancelar esse pedido no SIGECO. 


**Sigeco 2.0: Atendimento>ábacos>Pedidos digite o número do pedido do cliente**.


![](/assets/atendimentoPedidos06.png)


No centro inferior da tela, existe um botão cancelar pedido onde o atendente deverá cancelá-lo, porém não cancelará no ERP nem nas plataformas, o processo de cancelamento deverá ser seguido como de costume ( ticket sales force, cancelar ERP, plataformas, devoluções...)

![](/assets/atendimentoPedidos07.png)

Esse botão cancelar serve somente para que o pedido seja cancelado na tela de logs:

![](/assets/atendimentoPedidos08.png)

Lembrando que todo pedido cancelado deverá ser enviado um e-mail para o fornecedor informando número pedido e motivo do cancelamento.





---

![](/assets/atendimentoPedidos14.png)

![](/assets/atendimentoPedidos15.png)
