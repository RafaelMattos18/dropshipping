# Compra recebida com produto errado (físico diferente da nota)


Cliente entra em contato com atendimento ConnectParts e comunica que o 
Produto recebido está diferente da nota fiscal. Atendimento trata com clientes os prazos.

Atendimento gera uma NF de “acompanhamento de devolução”, entra em contato com a transportadora, encaminha a NF e solicita a coleta. Nessa solicitação de coleta deverá enviar o motivo pela devolução para que a transportadora imprima e entregue junto com a NF para o fornecedor.


A transportadora coleta a mercadoria no cliente e, chegando o produto no fornecedor, ele deverá nos comunicar que recebeu o produto, para então a Connect gerar uma NF de devolução de mercadoria que “anulará” a NF de venda, e então esse saldo de estoque no sistema deverá ser alimentado no estoque troca devolução fornecedor (para que a equipe de cobrança consiga emitir uma NF de devolução ao fornecedor quando financeiro solicitar) , gerando saldo no sistema e crédito ao cliente e então atendimento faz um novo pedido, de acordo com o que cliente solicitar.

**O fluxo de venda recomeça**.[^1]

---

[^1]: [Tratamento Ábacos Pedido](/chapter1/integracoes.md)