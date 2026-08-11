# Instruções: campo payment_received (PIX / Dinheiro)

Este pequeno trecho adiciona no formulário de venda a informação de como o pagamento foi recebido — apenas para registro administrativo.

O que foi adicionado
- snippets/payment-received.html: fragmento HTML + pequeno helper JS.

Como usar
1) Inserção direta no formulário:
   - Abra o arquivo HTML que contém o formulário de venda (ex.: templates/sale.html, checkout.html, etc.).
   - Cole o conteúdo de `snippets/payment-received.html` dentro do elemento `<form>...</form>` no local desejado.
   - Se o formulário for enviado normalmente (submit nativo), o campo `payment_received` será incluído no payload HTTP com o valor "pix" ou "dinheiro".

2) Se o formulário for enviado via JavaScript (fetch/XHR):
   - Use a função `getPaymentReceived(formElement)` (já incluída no snippet) para obter o valor selecionado e anexá-lo ao payload JSON antes de enviar.

Backend (o que esperar)
- Campo no corpo da requisição:
  - Envio com formulário tradicional (application/x-www-form-urlencoded ou multipart/form-data): `payment_received=pix` ou `payment_received=dinheiro`.
  - Envio via JSON (AJAX): inclua `payment_received: 'pix'` no objeto enviado.
- Grave este valor no banco como `payment_received` (string) para fins de relatórios/registro.

Boas práticas
- Se cada venda tem exatamente UMA forma de recebimento, prefira radios (como feito aqui) para evitar valores conflitantes.
- Se aceitar múltiplas formas por alguma razão, substitua por checkboxes e trate um array no backend.
- Valide no backend que o valor recebido pertence ao conjunto permitido: ["pix", "dinheiro"].

Commit nesta branch
- Esta modificação foi adicionada na branch `add-payment-received-field` como snippets para você integrar no arquivo de vendas existente.

Próximos passos que eu posso executar por você
- Se indicar o caminho para o arquivo do formulário de venda (ex.: `src/pages/checkout.html` ou `templates/sale.html`), eu posso aplicar o trecho diretamente nesse arquivo e abrir um PR.
- Se preferir, aplique o snippet manualmente e eu reviso o PR/commit.
