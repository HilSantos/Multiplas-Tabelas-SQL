# Multiplas-Tabelas SQL
Criação de tabelas usando MySql do ambiente PHP.

1. Liste todos os pedidos, incluindo o nome do cliente.
SELECT pedido_id, cliente_nome
FROM tb_pedidos
-------------------------------------------------------------------------------------------------------------------------------

2. Mostre todos os produtos vendidos, incluindo a quantidade total de cada.
SELECT produto_id, quantidade
FROM tb_itens_pedido
-------------------------------------------------------------------------------------------------------------------------------

3. Exiba os clientes que já realizaram um pedido.
SELECT cliente_nome, pedido_data
FROM tb_clientes
JOIN tb_pedidos
ON tb_pedidos.cliente_id = tb_clientes.cliente_id
-------------------------------------------------------------------------------------------------------------------------------

4. Mostre os clientes que ainda não fizeram pedidos.
SELECT cliente_nome, pedido_data
FROM tb_pedidos
JOIN tb_clientes
ON tb_clientes.cliente_id = tb_pedidos.pedido_data
WHERE pedido_data IS NULL
-------------------------------------------------------------------------------------------------------------------------------

5. Liste os pedidos que ainda não possuem pagamentos.
SELECT pedido_data, pagamento_valor
FROM tb_pedidos
JOIN tb_pagamentos
ON tb_pagamentos.pagamento_id = tb_pedidos.pedido_id
-------------------------------------------------------------------------------------------------------------------------------

6. Exiba o nome dos clientes e o total gasto em seus pedidos pagos.
SELECT cliente_nome, pagamento_valor
FROM tb_pagamentos
JOIN tb_clientes
ON tb_clientes.cliente_id = tb_pagamentos.pagamento_id
-------------------------------------------------------------------------------------------------------------------------------

7. Liste os pedidos e seus produtos correspondentes.
SELECT pedido_data, produto_nome
FROM tb_pedidos
JOIN tb_produtos
ON tb_produtos.produto_id = tb_pedidos.pedido_id
-------------------------------------------------------------------------------------------------------------------------------

8. Exiba os pedidos e a data do pagamento correspondente (se houver).
SELECT pedido_data, pagamento_data
FROM tb_pedidos
JOIN tb_pagamentos
ON tb_pagamentos.pagamento_id = tb_pedidos.pedido_id
-------------------------------------------------------------------------------------------------------------------------------

9. Exiba os clientes que compraram um determinado produto (por exemplo, "Notebook").
SELECT cliente_nome, produto_nome
FROM tb_clientes
JOIN tb_produtos
ON tb_produtos.produto_id = tb_clientes.cliente_id
-------------------------------------------------------------------------------------------------------------------------------

10. Mostre os clientes que já fizeram mais de um pedido.
SELECT cliente_nome, pedido_data
FROM tb_clientes
JOIN tb_pedidos
ON tb_pedidos.pedido_id = tb_clientes.cliente_id
GROUP BY cliente_nome
HAVING COUNT(pedido_data) > 1
------------------------------------------------------------------------------------------------------------------------------

11. Exiba os pedidos que contêm mais de um item.
SELECT pedido_data
FROM tb_pedidos
JOIN tb_itens_pedido
ON tb_itens_pedido.pedido_id = tb_pedidos.pedido_id
GROUP BY pedido_data
HAVING COUNT(item_id) > 1
-------------------------------------------------------------------------------------------------------------------------------

12. Exiba os produtos com preço maior que R$ 100,00. = 
SELECT produto_id, produto_preco 
FROM tb_produtos JOIN tb_pedidos_produtos
ON tb_produtos.produto_id = tb_pedidos_produtos.pedido_produto_preco_unitario
WHERE (pedido_produto_preco_unitario) > 100;
-------------------------------------------------------------------------------------------------------------------------------

13. Mostre os pedidos com status ‘Entregue’. =
SELECT pedido_id, pedido_status FROM tb_pedidos WHERE pedido_status = 'Entregue';
-------------------------------------------------------------------------------------------------------------------------------

14. Liste os pagamentos realizados via ‘Pix’. =
SELECT pagamento_id, pagamento_tipo FROM tb_pagamentos WHERE pagamento_tipo = 'Pix';
-------------------------------------------------------------------------------------------------------------------------------

15. Exiba as avaliações que receberam nota maior ou igual a 4. =
SELECT avaliacao_nota FROM tb_avaliacoes WHERE avaliacao_nota >= 4;
-------------------------------------------------------------------------------------------------------------------------------

16. Liste os pedidos e os nomes dos usuários que realizaram esses pedidos. =
SELECT pedido_id, usuario_nome 
FROM tb_pedidos
JOIN tb_usuarios
ON tb_usuarios.usuario_id = tb_pedidos.usuario_id
JOIN tb_avaliacoes
ON tb_usuarios.usuario_id = tb_avaliacoes.usuario_id
WHERE avaliacao_nota >= 4;
-------------------------------------------------------------------------------------------------------------------------------

17. Exiba os produtos e suas respectivas categorias. =
SELECT produto_nome, categoria_nome
FROM tb_produtos
JOIN tb_produtos_categorias
ON tb_produtos.produto_id = tb_produtos_categorias.produto_id
JOIN tb_categorias
ON tb_categorias.categoria_id = tb_produtos_categorias.categoria_id;
-------------------------------------------------------------------------------------------------------------------------------

18. Mostre os pedidos com os produtos comprados e suas respectivas quantidades. =
SELECT pagamento_status, pedido_produto_quantidade
FROM tb_pedidos
JOIN tb_pagamentos
ON tb_pagamentos.pedido_id = tb_pedidos.pedido_id
JOIN tb_pedidos_produtos
ON tb_pedidos_produtos.pedido_id = tb_pedidos.pedido_id;
-------------------------------------------------------------------------------------------------------------------------------

19. Exiba os pagamentos realizados e os respectivos pedidos com status de pagamento ‘Aprovado’. =
SELECT pagamento_status, tb_pedidos.pedido_id
FROM tb_pagamentos
JOIN tb_pedidos
ON tb_pedidos.pedido_id = tb_pagamentos.pedido_id
WHERE pagamento_status = 'Aprovado';
-------------------------------------------------------------------------------------------------------------------------------

20. Liste as avaliações feitas por cada usuário, incluindo o nome do usuário e o nome do produto avaliado. =
SELECT avaliacao_nota, usuario_nome, produto_nome
FROM tb_avaliacoes
JOIN tb_usuarios
ON tb_usuarios.usuario_id = tb_avaliacoes.usuario_id
JOIN tb_produtos
ON tb_produtos.produto_id = tb_avaliacoes.produto_id;
-------------------------------------------------------------------------------------------------------------------------------

21. Liste todos os usuários e, se existirem, os endereços cadastrados. (Inclua usuários sem endereço) =
SELECT usuario_nome, endereco_id
FROM tb_usuarios
JOIN tb_enderecos
ON tb_enderecos.usuario_id = tb_usuarios.usuario_id;
-------------------------------------------------------------------------------------------------------------------------------

22. Mostre todos os produtos e, se houver, as avaliações recebidas. (Inclua produtos sem avaliação) =
SELECT produto_nome, avaliacao_comentario
FROM tb_produtos
JOIN tb_avaliacoes
ON tb_avaliacoes.produto_id = tb_produtos.produto_id;
-------------------------------------------------------------------------------------------------------------------------------

23. Mostre todos os produtos e, se houver, as avaliações recebidas. (Inclua produtos sem avaliação) =
SELECT produto_nome, avaliacao_comentario
FROM tb_produtos
JOIN tb_avaliacoes
ON tb_avaliacoes.produto_id = tb_produtos.produto_id;
-------------------------------------------------------------------------------------------------------------------------------

24. Exiba todos os pedidos e, se houver, os pagamentos correspondentes. (Inclua pedidos sem pagamento) =
SELECT tb_pedidos.pedido_id, pagamento_id
FROM tb_pedidos
JOIN tb_pagamentos
ON tb_pagamentos.pedido_id = tb_pedidos.pedido_id;
-------------------------------------------------------------------------------------------------------------------------------

25. Exiba todos os usuários e seus pedidos, mesmo que alguns usuários ainda não tenham feito pedidos. =
SELECT usuario_nome, pedido_id
FROM tb_usuarios
LEFT JOIN tb_pedidos
ON tb_pedidos.usuario_id = tb_usuarios.usuario_id;
-------------------------------------------------------------------------------------------------------------------------------

26. Liste todos os produtos e as avaliações feitas, incluindo avaliações que não correspondem a um produto cadastrado. =
SELECT produto_nome, avaliacao_comentario
FROM tb_produtos
LEFT JOIN tb_avaliacoes
ON tb_avaliacoes.produto_id = tb_produtos.produto_id;
-------------------------------------------------------------------------------------------------------------------------------

27. Exiba todas as categorias e seus produtos, garantindo que todas as categorias apareçam mesmo que ainda não tenham produtos. =
SELECT categoria_nome, produto_nome
FROM tb_categorias
LEFT JOIN tb_produtos_categorias
ON tb_produtos_categorias.categoria_id = tb_categorias.categoria_id
LEFT JOIN tb_produtos
ON tb_produtos.produto_id = tb_produtos_categorias.produto_id;
-------------------------------------------------------------------------------------------------------------------------------

28. Liste todos os produtos e todas as avaliações, garantindo que produtos sem avaliação e avaliações sem produto cadastrado apareçam. =
SELECT produto_nome, avaliacao_comentario
FROM tb_produtos
LEFT JOIN tb_avaliacoes
ON tb_avaliacoes.produto_id = tb_produtos.produto_id;
-------------------------------------------------------------------------------------------------------------------------------

29. Exiba todos os usuários e seus pedidos, garantindo que usuários sem pedidos e pedidos sem usuário válido apareçam. =
SELECT usuario_nome, pedido_id
FROM tb_usuarios
LEFT JOIN tb_pedidos
ON tb_pedidos.usuario_id = tb_usuarios.usuario_id;
-------------------------------------------------------------------------------------------------------------------------------
