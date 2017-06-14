# Informações Técnicas


## Integrações

Os produtos serão expostos no site [www.connectparts.com.br](https://www.connectparts.com.br) através da integração.

### Integração Ábacos / Vtex

Ábacos/Vtex e caberá ao integrador imputar o estoque de produtos do fornecedor no Ábacos, utilizando como base comum o Código de Fornecedor. Caberá ao Ábacos, através do integrador Ábacos/Vtex, enviar a informação de estoque à Loja Virtual da ConnectParts. Após integrado e exposto o anuncio no site, ao ser feita uma venda destes itens, o integrador ábacos Vtex consome esta compra e imputa no Ábacos normalmente.

Em paralelo será gerado um pedido de compra nos ábacos \(mesma numeração pedido Vtex-Fornecedor\), de acordo com tabela de preços \(custo + R$15,00 embalagem\) fornecida pelo fornecedor \(já possuímos a tabela\). Qualquer alteração desta tabela deve ser comunicada com antecedência de 20 dias.

**No máximo em 03 minutos**, será disparada uma ordem de compra para o fornecedor, onde é dispara uma OC com todos os campos abaixo:

1. Nome cliente, se cliente é pessoa jurídica ou não, CPF, inscrição estadual \(se pessoa física CPF\)

2. Se é contribuinte de ICMS, tem suframa ou não, número suframa, em tipo de estabelecimento: outros

3. Suframa pins e COFINS

4. Telefone cliente, cel.  

5. Cliente vai em branco.

6. E-mail cliente.

7. E-mail que vai ser enviado a NF para o cliente \(sempre o mesmo\)

8. Endereço, número, complemento, cep, bairro.

9. Cidade, estado, pais.

10. Número pedido, código IBGE.

Texto fixo:  "**IMPOSTO RECOLHIDO POR SUBSTITUICAO TRIBUTARIA CFE ARTIGO 313-0 DO DECRETO N. 45.490/00**"

Quantidade itens DropShipping que existe nota fiscal, total da soma deles, lista de itens \(_contém código fornecedor, quantidade, preço venda, multiplicação: qtde x preço venda_\).

**Abaixo código que está no sistema:**

```
return new XDocument(
	new XDeclaration("1.0", "utf-8", ""),
	new XElement("SALESORDER",
		new XElement("SALESTABLE",
			new XElement("SALESNAME", pedido.Cliente.RazaoSocial.ToUpper()),
			new XElement("DELIVERYCUSTCATEGORY", pedido.Cliente.TipoPessoa.Equals("F") ? 1 : 2),
			new XElement("DELIVERYCUSTCNPJCPFNUM",CpfOuCnjp(pedido.Cliente.TipoPessoa.Equals("F"),pedido.Cliente.Documento)),
			new XElement("DELIVERYCUSTIENUM", pedido.Cliente.InscricaoEstadual),
			new XElement("ESTABLISHMENTTYPE", "OUTROS"),
			new XElement("ICMSCONTRIBUTOR", 0),
			new XElement("SUFRAMA", 0),
			new XElement("SUFRAMANUMBER"),
			new XElement("SUFRAMAPISCOFINS", 0),
			new XElement("PHONE", pedido.Cliente.Telefone.ToUpper()),
			new XElement("CELLULARPHONE", ""),
			new XElement("EMAIL", pedido.Cliente.Email.ToUpper()),
			new XElement("DS_EMAILNFE", pedido.Cliente.Email.ToUpper()),
			new XElement("DELIVERYSTREET", pedido.Cliente.Endereco.Entrega.Logradouro.ToUpper()),
			new XElement("DELIVERYADDRESSNUMBER", pedido.Cliente.Endereco.Entrega.Numero.ToUpper()),
			new XElement("DELIVERYADDRESSCOMPLEMENT", (pedido.Cliente.Endereco.Entrega.Complemento?? "").ToUpper()),
			new XElement("DELIVERYZIPCODE", pedido.Cliente.Endereco.Entrega.Cep.ToUpper()),
			new XElement("DELIVERYDISTRICTNAME", pedido.Cliente.Endereco.Entrega.Bairro.ToUpper()),
			new XElement("DELIVERYCITY", pedido.Cliente.Endereco.Entrega.Municipio.ToUpper()),
			new XElement("DELIVERYSTATE", pedido.Cliente.Endereco.Entrega.Estado.ToUpper()),
			new XElement("DELIVERYCOUNTRYREGIONID", pedido.Cliente.Endereco.Entrega.Pais.ToUpper()),
			new XElement("PURCHORDERFORMNUM", pedido.CodigoExterno.ToUpper()),
			new XElement("IBGECode", pedido.Cliente.Endereco.Entrega.CodigoIbge),
			new XElement("SALESLEGALTXT", "IMPOSTO RECOLHIDO POR SUBSTITUICAO TRIBUTARIA CFE ARTIGO 313-0 DO DECRETO N. 45.490/00"),
			new XElement("SALESAMOUNT", dropShippingPedidoItems.Sum(s => s.PrecoUnitarioVenda * s.Quantidade)),
			new XElement("QTY", dropShippingPedidoItems.Sum(s => s.Quantidade)),dropShippingPedidoItems.Select((s, i) =>
			new XElement("SALESLINE", new XAttribute("LINE", i + 1),
				new XElement("LINENUM", i + 1),
					new XElement("ITEMID", s.Produto.CodigoFabricacao),
					new XElement("SALESQTY", s.Quantidade),
					new XElement("LINEAMOUNT", s.PrecoUnitarioVenda * s.Quantidade),
					new XElement("SALESPRICE", s.PrecoUnitarioVenda)
				)
			)
		)
	)
);

```

Caso não tenhamos estoque no sistema, geraremos o pedido de compra para o fornecedor (pois trabalharemos com estoque virtual) que irá nos notificar o prazo que o produto estará disponível para envio ao cliente (conforme informação anterior de campos preenchidos com dados para contato com cliente).

Será solicitada para o fornecedor via WebService um prazo para que o produto entre em estoque, desta forma, a ConnectParts poderá negociar com o cliente final se o pedido prosseguirá ou não, caso de não prosseguir o ônus administrativo será da ConnectParts.

Quanto batermos na API do fornecedor para consultar o estoque e o estoque for igual ou menor que 10 unidades, iremos atualizar como 0 nosso sistema para não vendermos e não termos perigo de não conseguir atender o cliente.

Dentro do Sigeco 2.0 em T.I/Admin> Integrações > Log Dropshipping> existe o controle dos status de cada etapa do Dropshipping.
Se um status não alterar em 24hs úteis (exceto sábado, domingo e feriado) ficará em vermelho para acompanhamento e cobrança. 

**As descrições sobre LOGS estão logo abaixo**.

![](http://developers.connectparts.com.br/imagens/atendimentoPedidos09.png)

### Processos

#### Integração Ábacos Vtex

![](http://developers.connectparts.com.br/imagens/Fluxo DropShipping Pedido Vtex.png)

#### Tratamento Ábacos Pedido

![](http://developers.connectparts.com.br/imagens/Tratamento Pedido Ábacos.png)


### Informações para desenvolvedores

#### Restrições

O fornecedor vai precisar de uma ou mais APIs para comunicação com a ConnectParts, são necessários os seguintes Endpoint:

* Para receber pedidos, os dados serão enviados padrão JSon
	* Fornecedor irá nos informar dos dados que ele precisa para gerar um pedido de compras
 
* Para receber dados de NF, os dados serão enviados padrão JSon
	* Precisa passar quais dados ele precisa para executar o faturamento nf de remessa.

* Para disponibilizar quantidade de estoque dos produtos, padrão de retorno JSon.
	* Filtro de um produto por vez, uma lista de produtos (todos)
	* Filtro de data de modificação de estoque. 

* Notificar nf de remessa (faturamento do fornecedor)
	* Fornecedor deverá enviar um post para API /NotaFiscalRemessa/Inserir, informando os dados abaixo:



```
{
	PedidoCodigo (string),
	Rastreio (string, optional),
	Chave (string)stringMax. Length:44,
	NotificacaoTransportadora (boolean, optional),
	Numero (string, optional)stringMax. Length:9,
	DataEmissao (string),
	DataDespacho (string, optional),
	DataConfirmacao (string, optional),
	DataCriacaoRegistro (string, optional)
} 
```



* Notificar despacho de mercadoria ()
	* Fornecedor deverá enviar um post para API /NotaFiscalRemessa/NotificarDespacho, informando os dados abaixo:



```
{
	PedidoCodigo (string),
	DataDespacho (string)
} 
```



API que irá fazer um post para ConnectParts quando o fornecedor não tiver estoque do produto, deverá enviar estes dados abaixo:


```
{
	PedidoFornecedorCodigo (string),
	FabricacaoCodigo (string),
	FornecedorCodigo (string),
	Motivo (string),
	DataPrevisao (string),
	DataConfirmacao (string, optional)
}
```

## LOGS

### Funcionalidade

Apresentar todo o processo do pedido em uma linha do tempo.


#### Time Line

![](http://developers.connectparts.com.br/imagens/statusDropShipping.png)

**Time line** indicando todo o trajeto feito pelo pedido.

1. **Pedido integrado ao Ábacos**
    * Pedido foi inserido/integrado no ERP Ábacos.
2. **Fornecedor confirmou recebimento**
    * Pedido enviado para o fornecedor e confirmado.
3. **Fornecedor enviou NF de Compra**
    * Pedido de compra recebido, fornecedor enviou NF Compra para Connect.
4. **Pedido faturado pela ConnectParts**
5. **Connect enviou NF ao fornecedor**
6. **NF de remessa recebida**
    * Fornecedor encaminha NF para Connect que comunica ao cliente do rastreio, envia dados na nota para transportadora, inclui informações no sistema de CRM, caso não tenha pedido no sistema de CRM fica notificando até localizar pedido.
7. **Rastreamento enviado ao cliente**
    * Dados enviados ao cliente, este status é alterado quando o sistema conseguir fazer 3 notificações supracitadas.
8. **Despachada pelo fornecedor**
    * Concluído, fornecedor informa a Connect o despacho da mercadoria


## Processo

Sempre que subir um novo dk ou alterar preço de custo  para  venda de Produtos Dropshipping, deverá incluír no sistema Sigeco, para que esse produto seja atualizado o preço de custo, e caso seja produto novo, deverá ser inserido estoque de acordo com estoque do fornecedor.

> **Sigeco 2.0 > T.I / Admin / Importar Planilha de Custos**.
>
> Selecione o fornecedor e suba a planilha para o sistema. Feito isso clique em enviar Planilha. A Planilha deverá conter as informações em anexo.
DK CONNECT / COD; FABRICANTE / $ CUSTO ( Acrescidos o valor de embalagem e manuseio )
>
> **Em ativo:** Utilize 1 caso queira que consulte o estoque e alimente o ábacos ou 0 para não.



![](http://developers.connectparts.com.br/imagens/descricao03.png)


