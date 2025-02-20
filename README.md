# TesteSQL-14022025

Estou fazendo este documento pois não consigo fazer nenhuma movimentação na máquina da empresa além do que é permitido.  
Comecei utilizando o [DB Fiddle](https://www.db-fiddle.com/), pois achei que funcionou melhor.


## 2. Primeira Consulta:

![Primeira consulta]
SELECT ID_VENDEDOR AS id, NOME AS nome, SALARIO AS salario
FROM VENDEDORES
WHERE INATIVO = FALSE
ORDER BY NOME ASC;

---

## 3. Segunda Consulta:

![Segunda consulta]
SELECT
 ID_VENDEDOR AS ID, NOME, SALARIO 
FROM VENDEDORES
WHERE SALARIO > (SELECT AVG(SALARIO) FROM VENDEDORES)
ORDER BY SALARIO DESC;


---

## 4. Terceira Consulta:

![Terceira consulta ]
SELECT c.ID_CLIENTE AS id, c.RAZAO_SOCIAL AS razao_social,
	COALESCE (SUM(p.VALOR_TOTAL), 0) AS total
FROM CLIENTES c
LEFT JOIN PEDIDO p ON c.ID_CLIENTE = p.ID_CLIENTE
GROUP BY c.ID_CLIENTE, c.RAZAO_SOCIAL
ORDER BY total DESC;

## 5. Quarta Consulta:

![Quarta consulta]
SELECT
	ID_PEDIDO AS ID,
	VALOR_TOTAL AS VALOR,
	DATA_EMISSAO AS DATA,
	CASE
		WHEN DATA_CANCELAMENTO IS NOT NULL THEN 'CANCELADO'
		WHEN DATA_FATURAMENTO IS NOT NULL THEN 'FATURADO'
	END AS SITUACAO
FROM PEDIDO;


## 7. Quinta Consulta:
![Quinta consulta]
SELECT ip.ID_PRODUTO AS id_produto,
	SUM(ip.QUANTIDADE) AS quantidade_vendida,
	SUM (ip.QUANTIDADE * ip.PRECO_PRATICADO) AS total vendido,
	COUNT (DISTINCT p.ID_CLIENTE) AS clientes,
	COUNT (DISTINCT ip.ID_PEDIDO) AS pedidos
FROM ITENS_PEDIDO ip
JOIN PEDIDO p ON ip.ID_PRODUTO = p.ID_PEDIDO
GROUP BY ip.ID_PRODUTO
ORDER BY quantidade vendida DESC, total vendido DESC
LIMIT 1;



