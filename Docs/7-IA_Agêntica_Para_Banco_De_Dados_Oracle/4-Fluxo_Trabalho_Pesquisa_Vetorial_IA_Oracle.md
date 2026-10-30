# Fluxo de trabalho da Busca Vetorial do Oracle AI

## Considerações iniciais

### Visão geral

Nesta lição, vamos percorrer as principais etapas da Busca Vetorial do Oracle AI, desde a geração de embeddings até o uso dos resultados em aplicações de geração aumentada por recuperação (RAG). Também veremos opções para gerar embeddings, dividir documentos em partes, armazenar vetores e realizar consultas por similaridade.

---

# Transcrição da aula

## 1. Etapas do fluxo de Busca Vetorial

O fluxo de trabalho da Busca Vetorial do Oracle AI pode ser organizado em cinco etapas:

1. Gerar embeddings, no banco de dados ou por meio de um serviço externo.
2. Armazenar os vetores em tabelas Oracle usando o tipo de dados `VECTOR`, junto aos dados comerciais.
3. Criar índices vetoriais para acelerar as buscas por similaridade.
4. Executar consultas de similaridade com funções de distância vetorial, combinadas com predicados SQL.
5. Usar os resultados relevantes em aplicações de RAG, fornecendo trechos de contexto ao modelo de linguagem (LLM).

## 2. Gerando embeddings

Há duas abordagens principais para gerar embeddings:

- **No banco de dados:** usar modelos ONNX com o ONNX Runtime integrado ao Oracle Database. O modelo é importado para o banco, e os embeddings são gerados sem chamadas de rede ou transferência dos dados para outro serviço.
- **Externamente:** chamar APIs REST de provedores como OpenAI ou Cohere. Essa abordagem dá acesso aos modelos oferecidos por esses provedores.

O pacote `DBMS_VECTOR_CHAIN` fornece funções utilitárias que podem encadear etapas do processamento, como extração de texto, divisão em partes e geração de embeddings.

## 3. Dividindo documentos em partes

Modelos de embeddings conseguem processar apenas uma quantidade limitada de tokens por vez. Por isso, documentos extensos — como um PDF de cem páginas — precisam ser divididos em partes menores e significativas, processo conhecido como *chunking*.

O Oracle fornece funções utilitárias para essas etapas:

- `UTL_TO_TEXT` converte PDFs e documentos do Word em texto simples;
- `UTL_TO_CHUNKS` divide o texto em partes;
- `UTL_TO_EMBEDDINGS` gera vetores para cada parte.

Essas funções podem ser encadeadas em uma única instrução SQL `INSERT`. É possível configurar estratégias de divisão, como por palavra, frase ou parágrafo, além do tamanho e da sobreposição entre as partes. A sobreposição ajuda a preservar o contexto entre trechos consecutivos.

## 4. Criando índices vetoriais

Sem um índice, uma busca por similaridade precisa examinar cada vetor. Isso pode ser adequado para conjuntos pequenos, mas se torna lento e custoso quando há milhões de vetores.

O Oracle oferece diferentes opções de índices vetoriais:

- **HNSW** (*Hierarchical Navigable Small World*): constrói um grafo em camadas para percorrer rapidamente vetores próximos. As camadas superiores facilitam a navegação; as inferiores ajudam a refinar os resultados.
- **IVF** (*Inverted File Index*): agrupa os vetores em partições, normalmente usando *k-means*, e pesquisa as partições mais próximas da consulta.
- **Índices vetoriais híbridos:** combinam busca vetorial e textual.

A escolha do índice depende das características dos dados e das necessidades da aplicação.

## 5. Armazenando vetores no Oracle Database

O Oracle Database oferece o tipo de dados vetorial nativo `VECTOR`, que pode ser declarado como uma coluna de tabela.

Uma declaração flexível permite armazenar vetores com dimensões e formatos variados. Também é possível especificar restrições, por exemplo, `VECTOR(768, INT8)`, para exigir uma quantidade fixa de dimensões e um formato de armazenamento específico.

Os formatos incluem `FLOAT32`, `FLOAT64`, `INT8` e binário. O armazenamento pode ser:

- **Denso:** armazena todas as dimensões.
- **Esparso:** armazena apenas as dimensões diferentes de zero, o que pode ser útil para embeddings esparsos.

Consulte a documentação do Oracle Database para verificar os formatos disponíveis e os detalhes de armazenamento da versão utilizada.

## 6. Consultando vetores por similaridade

A busca por similaridade compara vetores usando uma métrica de distância. Entre as métricas comuns estão:

- **Cosseno:** mede o ângulo entre os vetores e é bastante usado com embeddings de texto.
- **Euclidiana (L2):** mede a distância em linha reta entre os vetores.
- **Produto interno (produto escalar):** considera a direção e a magnitude.
- **Manhattan:** soma as diferenças absolutas entre as dimensões.

A função de distância recebe os vetores e a métrica escolhida. Em geral, resultados com menor distância são mais semelhantes. Uma consulta pode ordenar os resultados pela distância e limitar a saída às primeiras `n` linhas para obter os vizinhos mais próximos.

É importante usar uma métrica compatível com o modelo de embeddings, seguindo as recomendações de sua documentação.

## 7. Combinando busca vetorial e SQL

As consultas por similaridade podem ser combinadas com predicados SQL tradicionais. Por exemplo, é possível buscar casas semelhantes a uma imagem, limitar os resultados a um preço inferior a US$ 500.000 e restringir a busca a Nova York.

Essa combinação permite pesquisar por similaridade sem abrir mão dos filtros relacionais aplicados aos dados comerciais.

## 8. Recapitulando os pontos principais

- O fluxo inclui geração, armazenamento e indexação de embeddings, consultas por similaridade e uso dos resultados em RAG.
- Os embeddings podem ser gerados no banco com modelos ONNX ou por APIs externas.
- O *chunking* divide documentos grandes em partes que os modelos conseguem processar.
- Índices como HNSW e IVF ajudam a acelerar buscas em conjuntos grandes de vetores.
- O tipo `VECTOR` permite armazenar vetores junto aos dados relacionais no Oracle Database.
- Métricas de distância determinam como a similaridade é calculada.
- Consultas vetoriais podem ser combinadas com filtros SQL.

## Conclusão

Nesta lição, percorremos o fluxo de Busca Vetorial do Oracle AI: geração de embeddings, divisão de documentos, armazenamento e indexação de vetores e consultas por similaridade. Também vimos como o Oracle permite combinar essas consultas com SQL e usar os resultados em aplicações de RAG.

Na próxima aula demonstrativa, veremos alguns desses recursos em ação. Espero que esta aula tenha sido útil. Obrigado pelo seu tempo!
