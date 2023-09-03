# Palatadorma Dio - Projeto de Banco de Dados

Este é um projeto de banco de dados para o cenário de um e-commerce chamado "Palatadorma Dio". O objetivo deste projeto é modelar e implementar o esquema do banco de dados para atender às necessidades do e-commerce, considerando as seguintes diretrizes:

- Clientes podem ser Pessoa Jurídica (PJ) ou Pessoa Física (PF), mas não ambas.
- Os clientes podem ter várias formas de pagamento cadastradas.
- As entregas possuem status e códigos de rastreio.

## Estrutura do Banco de Dados

O esquema do banco de dados consiste nas seguintes tabelas:

- `Cliente`: Armazena informações dos clientes, incluindo nome e tipo (PJ ou PF).
- `Conta`: Armazena informações das contas dos clientes, incluindo saldo.
- `FormaPagamento`: Contém os tipos de formas de pagamento disponíveis.
- `ClienteFormaPagamento`: Relaciona clientes com suas formas de pagamento.
- `Pedido`: Registra informações sobre os pedidos, incluindo a data e o cliente.
- `Produto`: Armazena informações dos produtos disponíveis.
- `ItemPedido`: Relaciona pedidos com os produtos e inclui a quantidade de cada item.
- `Entrega`: Registra informações sobre as entregas, incluindo status e código de rastreio.

## Exemplos de Consultas SQL

Aqui estão alguns exemplos de consultas SQL que podem ser executadas neste banco de dados:

- Recuperação simples de clientes Pessoa Física:
  ```sql
  SELECT * FROM Cliente WHERE Tipo = 'PF';


- Recuperação simples de clientes Pessoa Jurídica:
    ```sql
    SELECT Pedido.*
    FROM Pedido
    INNER JOIN Cliente ON Pedido.ClienteID = Cliente.ClienteID
    WHERE Cliente.Tipo = 'PJ';

- Criação de um atributo derivado para o valor total de um pedido:
    ```sql
    SELECT Pedido.PedidoID, SUM(Produto.Preco * ItemPedido.Quantidade) AS ValorTotal
    FROM Pedido
    INNER JOIN ItemPedido ON Pedido.PedidoID = ItemPedido.PedidoID
    INNER JOIN Produto ON ItemPedido.ProdutoID = Produto.ProdutoID
    GROUP BY Pedido.PedidoID;

- Ordenação de produtos por nome:
  ```sql
  SELECT * FROM Produto ORDER BY Nome ASC;

- Condição de filtro aos grupos para encontrar clientes com mais de 3 pedidos:
  ```sql
  SELECT Cliente.ClienteID, COUNT(Pedido.PedidoID) AS NumPedidos
  FROM Cliente
  LEFT JOIN Pedido ON Cliente.ClienteID = Pedido.ClienteID
  GROUP BY Cliente.ClienteID
  HAVING COUNT(Pedido.PedidoID) > 3;

- Junção entre tabelas para obter informações detalhadas de um pedido:
   ```sql
    SELECT Pedido.PedidoID, Cliente.Nome AS NomeCliente, Produto.Nome AS NomeProduto
    FROM Pedido
    INNER JOIN Cliente ON Pedido.ClienteID = Cliente.ClienteID
    INNER JOIN ItemPedido ON Pedido.PedidoID = ItemPedido.PedidoID
    INNER JOIN Produto ON ItemPedido.ProdutoID = Produto.ProdutoID;

## Como Usar
Você pode usar este projeto de banco de dados para implementar um sistema de gerenciamento de e-commerce. Para começar, você precisará criar um banco de dados e executar o script SQL fornecido neste projeto para criar as tabelas e os relacionamentos.

Certifique-se de personalizar a estrutura do banco de dados e as consultas SQL de acordo com as necessidades específicas do seu projeto.

## Contribuições
Contribuições são bem-vindas! Se você tiver sugestões de melhorias para o esquema do banco de dados ou exemplos de consultas SQL adicionais, sinta-se à vontade para abrir uma issue ou enviar um pull request.

## Licença

Este projeto é distribuído sob a licença MIT. Consulte o arquivo [LICENSE](https://github.com/iaguy/iaguy-Dio_projeto_modelo_logico_oficina/blob/main/LICENSE) para obter mais informações.