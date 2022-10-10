# Descritivo de possíveis melhorias no sistema:

## 1 - Usuário do tipo admin não possui um próprio menu:
### Descrição do problema:
- Por não haver uma condição para o usuário que tem a role admin, ele estava caindo na condição de usuário "cliente".
### Sugestão para solução:
- Adicionar uma condição para usuário admin, e criar um menu próprio para ele, onde se pode visualizar todas as vendas, estoque e informações das empresas cadastradas no sistema.

## 2 - É possível selecionar produtos cadastrados para outras empresas
### Descrição do problema:
- É possível selecionar produtos que estão cadastrado para outras empresas, no momento em que o cliente está efetuado a compra;
- Exemplo: seleciono a empresa de id 1, essa empresa tem os produtos de ids 1, 2 e 3 cadastrados. Se eu selecionar o produto id 4, e esse produto estiver cadastrado para outra empresa, o sistema adicionar esse produto para uma venda da empresa selecionada.
### Sugestão para solução:
- Na linha 149, adicionar nessa condição se o id da empresa cadastrada no produto, é o mesmo id da empresa selecionada.
- Exemplo: (produtoSearch.getId().equals(escolhaProduto) && produtoSearch.getEmpresa().getId().equals(escolhaEmpresa))

## 3 - Após a venda de algum produto, não está sendo subtraido a quantidade no estoque da empresa
### Descrição do problema:
- No momento em que se realiza a venda de qualquer produto, não está sendo subtraido pela quantidade vendida.
### Sugestão para solução:
- Após adicionar a venda no objeto carrinho, setar a quantidade do productSearch;
- Exemplo: produtoSearch.setQuantidade(produtoSearch.getQuantidade() - 1);

## 4 - Verificar estoque antes de efetuar a venda
### Descrição do problema:
- Antes de ser efetuado uma venda, verificar se há disponibilidade do produto no estoque
### Sugestão para solução:
- Antes de adicionar o produto no objeto carrinho, fazer uma condição para verificar a disponibilidade do produto no estoque.

## 5 - O saldo da empresa não está subtraindo as taxas
### Descrição do problema:
- O saldo total que está sendo computado nas empresas, está sendo o saldo bruto e não está subtraindo as taxas.
### Sugestão para solução:
- No momento em que é efetuado uma venda, o saldo que está sendo setado, é a soma do saldo atual + total da venda, e não está sendo subtraido as taxas.
- Apenas subtrair as taxas pelo saldo total, Exemplo: empresa.setSaldo(empresa.getSaldo() + (total - comissaoSistema))(Linha 211);

## 6 - Problema se digitado um id de uma empresa não existente
### Descrição do problema:
- Se digitar um id de uma empresa inexistente, aplicação "quebra" com a exceção `IndexOutOfBoundsException`;
### Sugestão para solução:
- Muito provável que isso aconteça, porque não existe essa posição selecionada no array de objetos empresas/
- Acredito que se tiver um try/catch para tratar essa exceção a aplicação não "quebrará" mais.

## 7 - Problema se digitado uma senha/usuario errados
### Descrição do problema:
- Se digitar a senha e/ou usuario errados, o sistema está aparecendo a ultima compra realizada;
### Sugestão para solução:
- Não consegui identificar o real motivo desse problema;
- Talvez se reiniciar aplicação após a mensagem de "Usuário não encontrado" o problema seja resolvido. Exemplo: executar(usuarios, clientes, empresas, produtos, carrinho, vendas);

## 8 - Menu do cliente para selecionar as empresas não está em ordem:
### Descrição do problema:
- No momento em que se seleciona para realizar compra com usuário "cliente", o menu não está em ordenado conforme o número do id da empresa.
### Sugestão para solução:
- Na linha 134, após o stream, adicionar .sorted() para ordenar em ordem conforme o id das empresas cadastradas. Exemplo: empresas.stream.sorted(Comparator.comparing(Empresa::getId)).forEach(...).