# Demonstração: Busca Vetorial do Oracle AI

## Considerações iniciais

### Visão geral

Nesta demonstração, vamos observar como a busca vetorial encontra produtos com significado semelhante ao de uma consulta, mesmo quando os termos pesquisados não aparecem nas descrições. Também veremos como combinar a busca por similaridade com filtros relacionais em SQL.

---

# Transcrição da aula

## 1. Busca por similaridade sem correspondência exata

Depois que a consulta é convertida em um embedding, a função de distância vetorial do Oracle a compara com os vetores armazenados, ordena os resultados por proximidade e retorna as correspondências mais próximas.

Considere a consulta “equipamento para exercícios em casa”. Nenhuma dessas palavras aparece nas descrições dos produtos do exemplo. Uma busca tradicional por palavras-chave não retornaria resultados, pois depende da correspondência dos termos pesquisados.

A busca vetorial, por outro lado, considera o significado. Ela pode identificar tapetes de ioga e rastreadores de fitness como itens relacionados a exercícios em casa. O tapete de ioga aparece primeiro por estar mais próximo da consulta no espaço vetorial, isto é, por ter a menor distância.

## 2. Combinando busca vetorial com filtros SQL

Também é possível combinar uma consulta semântica com uma cláusula `WHERE`. Por exemplo, podemos buscar produtos relacionados a “proteção para esportes aquáticos” e limitar os resultados a itens que custem menos de US$ 100.

O fluxo continua usando o mesmo modelo para gerar o embedding da consulta. Em seguida, a função de distância vetorial compara a consulta com os vetores dos produtos, e os resultados são ordenados por proximidade.

No exemplo, os produtos que custam mais de US$ 100 — como botas de caminhada, uma raquete de tênis e uma barraca — não atendem ao filtro de preço. Entre os produtos restantes, os óculos de natação, por cerca de US$ 25, aparecem como resultado mais próximo da consulta.

## 3. Busca vetorial e dados relacionais na mesma consulta

Em um banco de dados vetorial separado, talvez fosse necessário consultar os vetores primeiro e aplicar filtros relacionais posteriormente no código da aplicação. No Oracle, a busca por similaridade e os filtros de SQL podem ser combinados em uma única instrução.

Isso permite aplicar critérios relacionais, como preço, aos produtos e, ao mesmo tempo, ordenar os resultados pela similaridade semântica. Assim, itens fora do limite de preço são eliminados, e os demais são classificados de acordo com sua proximidade em relação à consulta.

## 4. Recapitulando os pontos principais

- A busca vetorial pode encontrar itens relacionados mesmo quando as palavras da consulta não aparecem nas descrições.
- A distância entre os vetores permite ordenar os resultados por similaridade.
- Uma cláusula `WHERE` pode combinar critérios relacionais, como limite de preço, com a busca vetorial.
- No Oracle, esses critérios podem ser aplicados em uma única consulta SQL.

## Conclusão

Nesta demonstração, vimos como a Busca Vetorial do Oracle AI identifica produtos semanticamente relacionados e como ela pode ser combinada com filtros relacionais em SQL.

Espero que esta demonstração tenha sido útil. Obrigado pelo seu tempo!
