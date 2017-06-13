# Estoque

Estoque dos produtos dos fornecedores serão alimentados no estoque virtual e quando informarmos o fornecedor sobre a venda, ele nos enviará uma NF de compra, o fiscal dará entrada na NF assim que for dado a entrada na NF alimentará o estoque connect e então logística fatura a venda.


## Falta de item em estoque 

Para comunicar a falta de item em estoque de produto de DropShippingvendido, o FORNECEDOR deverá informar na forma definida pela ConnectParts (Será gerado um ticket na Sales Force), sem prejuízo de outras informações, em até 12 horas após o recebimento da informação da venda do produto, em dias úteis.

## Integrações / Estoque Dropshipping

---

![](http://developers.connectparts.com.br/imagens/estoqueDropshipping.png)

## Funcionalidade

Nesta tela mostrará os produtos que estão na situação de estoque **menor ou igual a quantidade 5**.

## Processo

**Fornecedor**: Quando o estoque de um determinado produto no **Fornecedor** for menor ou igual a quantidade 5, o sistema marca esse produto como “**_pendência_**” e insere o saldo virtual no ERP como **0** para não vender.

> Existe um serviço que consulta o saldo as **02h00** no fornecedor mostrando nesse sistema para ciência do comprador/vendedor.


