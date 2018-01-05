# Pedidos

Os pedidos serão apresentados da seguinte forma:

**Vtex:** 123456 

**Ábacos:**  
* 123456 –“fornecedor”
* 123456 – “connect”

Na Vtex será apenas um único pedido contendo todos os produtos.Já no ábacos haverá um pedido para determinado fornecedor.

![](http://developers.connectparts.com.br/imagens/atendimentoPedidos16.png)

Assim que o cliente **finalizar a compra**, e seu **pagamento for aprovado**, ele recebe um e-mail de confirmação de compra, caso esse pedido contenha um item DropShipping, haverá a informação sobre entregas em dias diferentes. 


![](http://developers.connectparts.com.br/imagens/atendimentoPedidos02.png) 


![](http://developers.connectparts.com.br/imagens/atendimentoPedidos03.png)


O pedido entrará com o **status pré analise**, onde será analisado pela equipe de Análise de risco de acordo com a política da empresa e assim que for **liberado** seguirão seus status.]]

## Regras

* Iremos notificar o fornecedor (**DTS**) antes de enviar a nota fiscal de venda, verificaremos se há um pedido de compra do mesmo pedido de venda.

    **Envio de email**
    Nos e-mails transacionais de ‘Confirmação de compra’ haverá a seguinte descrição no corpo dos e-mails
    **E-mail contendo produto na modalidade DropShipping**: _Por questões operacionais relativas à logística é possível que a postagem e entrega dos produtos ocorram em dias diferentes._
    **E-mail não contendo produto na modalidade DropShipping** :_Adicione o e-mail vendas@connectparts.com.br como confiável e confira sempre sua caixa de spam e lixo eletrônico para não perder nenhuma informação sobre seu pedido ou acesse seu cadastro no www.connectparts.com.br_

* Afim de não gerar uma demanda extra criando coleções para esses produtos criei à regra com base na informação oriunda do campo ‘modal’.

* É imprescindível que, em caso de novos produtos nessa modalidade e que o campo modal seja vazio ou diferente de ‘Colchões’, que me informem de imediato para alterações no template de e-mail.



## Tempo Processos

|Responsável.|	Ação|
|---|---|
|**ConnectParts**|ConnectParts deverá comunicar a DTS em até** 12 minutos** após  o pedido integrar na plataforma.|
|**Fornecedor**|Fornecedor enviará  NF de compra para ConnectParts às** 12hs e 16hs.**|
|**Fornecedor**|Fornecedor não tem produto, deverá informar ConnectParts com as informações já definidas em até **12 hs úteis**.|
|**ConnectParts**|ConnectParts fará o faturamento  das notas de compras recebidas do fornecedor às **13hs e 18hs**, exceto quando pedido cair na análise de risco.|
|**Fornecedor**|Fornecedor deverá enviar Nota de Remessa para ConnectParts em até **2h** após receber NF de faturamento,considerando que o horário máximo de recebimento da informação pela ConnectParts é até as **15h**, após este horário considerar até **1ª hora** do dia seguinte.|
