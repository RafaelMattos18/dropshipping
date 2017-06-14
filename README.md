# Dropshipping

## Descrição

Dropshipping é uma técnica de gestão da cadeia logística na qual a CONNECTPARTS não mantém os produtos em estoque, apresentando os produtos a seus clientes através da **[loja virtual](http://www.connectparts.com.br/)**, **Marketplace** e **Mercado Livre**; assim que o pedido do cliente for aprovado o pagamento (_entre status pronto para manuseio e preparando entrega -verificar imagem abaixo_), a **ConnectParts** informa a venda ao fornecedor. Dessa maneira o fornecedor emite uma NF de venda do produto pra ConnectParts que dará entrada na Nota Fiscal e fará o faturamento e então o fornecedor realizará o processo de embalagem e envio diretamente ao cliente. 

A mercadoria só será enviada ao cliente via transportadora após a ConnectParts enviar a NF de faturamento desse para-choque para o fornecedor e o mesmo emitir a NF de Remessa para acompanhar a mercadoria até o cliente.

Haverá uma informação na política de entrega do nosso site: "**_Por questões operacionais relativas à Logística é possível que a postagem e entrega dos produtos ocorram em dias diferentes_**".

Quando um pedido dropshipping for faturado pela Connect, independente do fornecedor, ele não será despachado pela Connect, dessa forma assim que ele for  faturado, a Logística da Connect deverá alterar o status no ERP para despachado.

### Fluxo Básico

<!--![Fluxo Basico](/assets/FluxoBásico.png)-->
![](http://developers.connectparts.com.br/imagens/FluxoBásicoNew.png)




## CFOP utilizados para emissão de NF

* ConnectParts irá emitir NF de venda para nosso cliente: 
    * **5.405** produtos dentro estado SP 
    * **6.403** produtos fora do estado de SP 
    * **6.108** produtos não contribuintes fora do estado 
    * **6.102** produtos para estados que não tem protocolo 41/2008 - acordo da ST entre os estados (CE,RO e MS).

* Connect emitir NF de coleta para Transportadora coletar mercadoria (acompanhamento de produto) no cliente e entregar no fornecedor: Outras Saídas - 1949 dentro estado / 2949 fora estado – Iremos emitir uma NF de Remessa pois não tem tributação, apenas para transitar mercadoria e não precisaremos cancelar caso cliente não esteja no local da coleta poderá ser coletado em outro dia.

* Connect emitir NF de devoluções de mercadoria em casos de troca/devoluções: 1.411 (dentro estado) 2.411 (fora estado).

* Fornecedor emitir NF de acompanhamento de mercadoria até o cliente: 5923 e 6923

* Fornecedor emitir NF de venda para Connect: 5403



