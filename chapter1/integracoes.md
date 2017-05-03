# Integrações

Os produtos serão expostos no site www.connectparts.com.br através da integração.

Ábacos/Vtex e caberá ao integrador Calipso imputar o estoque de produtos da DTS no Ábacos, utilizando como base comum o Código de Fornecedor. Caberá ao Ábacos, através do integrador Ábacos/Vtex, enviar a informação de estoque à Loja Virtual da Connect Parts. Após integrado e exposto o anuncio no site, ao ser feita uma venda destes itens, o integrador ábacos Vtex consome esta compra e imputa no Ábacos normalmente.

Em paralelo será gerado um pedido de compra nos ábacos \(mesma numeração pedido Vtex-DTS\), de acordo com tabela de preços \(custo + R$15,00 embalagem\) fornecida pelo fornecedor \(já possuímos a tabela\). Qualquer alteração desta tabela deve ser comunicada com antecedência de 20 dias.

No máximo em 10 minutos, será disparada uma ordem de compra para o fornecedor, onde é dispara uma OC com todos os campos abaixo:

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



