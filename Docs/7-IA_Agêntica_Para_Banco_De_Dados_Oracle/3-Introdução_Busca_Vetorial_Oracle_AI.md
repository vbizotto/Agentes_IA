# Introdução à Busca Vetorial do Oracle AI

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar embeddings, vetores e os conceitos básicos da Busca Vetorial do Oracle AI. Vamos entender como representações matemáticas capturam o significado dos dados e como o Oracle Database permite armazenar e pesquisar esses vetores junto aos dados tradicionais.

---

# Transcrição da aula

## 1. Da busca por palavras-chave à busca semântica

As buscas tradicionais em bancos de dados dependem da correspondência exata de palavras-chave. Por exemplo, uma pesquisa por “canino” pode não encontrar documentos que falem sobre “cachorros”.

Isso pode ser frustrante, porque as pessoas geralmente procuram um significado, não apenas uma palavra exata. A busca semântica baseada em vetores ajuda a resolver esse problema: ela converte o texto em representações matemáticas que capturam seu significado. Assim, termos como “canino” e “cachorro” podem ficar próximos no espaço vetorial e ser encontrados por uma busca por similaridade.

## 2. Vetores e embeddings

Um vetor é uma lista de números. Uma forma de imaginá-lo é como coordenadas de GPS, mas em centenas ou milhares de dimensões, em vez de apenas duas.

Um modelo de embeddings é uma rede neural que converte dados — como texto, imagens ou áudio — em vetores. A ideia é que conteúdos semelhantes gerem vetores próximos uns dos outros.

Imagine um mapa em que cada palavra, frase ou documento ocupa uma posição. Termos como “cachorro”, “filhote” e “canino” ficariam agrupados por terem significados semelhantes. O mesmo aconteceria com “gato”, “gatinho” e “felino”. Já “carro” ficaria distante, por representar um conceito diferente.

## 3. Modelos de embeddings

Existem muitos modelos de embeddings. Entre os exemplos citados na aula estão:

- modelos disponíveis no Hugging Face;
- `all-MiniLM`, com 384 dimensões, como opção introdutória;
- modelos da OpenAI, como o Text Embedding Large Model, mencionado na aula com 3.072 dimensões.

No Oracle AI Vector Search, também é possível executar modelos de incorporação ONNX diretamente no banco de dados. ONNX significa *Open Neural Network Exchange* (Intercâmbio Aberto de Redes Neurais). Nesse caso, a criação dos embeddings acontece dentro do próprio banco.

## 4. Como os embeddings são criados

O fluxo de criação de embeddings pode ser entendido em três etapas:

1. **Entrada dos dados:** texto, imagens, áudio ou outros dados são fornecidos ao fluxo.
2. **Tokenização:** um tokenizador divide a entrada em tokens, que podem ser entendidos como fragmentos de palavras.
3. **Geração do vetor:** uma rede neural, normalmente baseada em uma arquitetura Transformer, processa os tokens e produz um vetor que representa o significado semântico da entrada.

Por exemplo, um tokenizador BERT pode dividir uma frase em vários tokens. O símbolo `##` pode indicar que um fragmento continua um token anterior, em vez de representar uma palavra independente. Outros modelos podem usar tokenizadores diferentes, portanto, é importante consultar a documentação do modelo escolhido.

## 5. Limites de tokens e *chunking*

Os tokenizadores têm um limite para a quantidade de tokens que conseguem processar de uma só vez. Esse limite costuma ser de 512 tokens ou um pouco mais, embora varie conforme o modelo.

Por isso, documentos extensos podem precisar ser divididos em partes menores, um processo chamado *chunking*. Essa técnica será explorada em uma lição posterior.

## 6. Busca Vetorial do Oracle AI

A Busca Vetorial do Oracle AI não é um produto separado: é um recurso integrado ao Oracle Database. Ela permite armazenar, indexar e pesquisar vetores de embeddings junto com dados empresariais tradicionais, usando SQL.

Como os vetores permanecem no mesmo banco que os registros de clientes, pedidos e produtos, não é necessário configurar e manter um banco vetorial separado para esses dados. A integração também permite aproveitar recursos do banco, como segurança, transações, backup e escalabilidade.

## 7. Consultas por similaridade com SQL

A função `VECTOR_DISTANCE` permite encontrar itens semelhantes. Ela também pode ser combinada com cláusulas `WHERE` comuns para aplicar filtros relacionais na mesma consulta.

Por exemplo, seria possível buscar casas semelhantes a uma imagem, limitar o preço a menos de US$ 500.000 e restringir os resultados à cidade de Nova York. A combinação de busca vetorial e filtros SQL permite expressar esses critérios em uma única consulta.

## 8. Recapitulando os pontos principais

- Buscas semânticas com vetores consideram a similaridade de significado, não apenas a correspondência exata de palavras.
- Modelos de embeddings convertem dados em vetores que representam seu conteúdo.
- O fluxo de criação envolve entrada de dados, tokenização e geração do vetor por uma rede neural.
- Limites de tokens podem exigir a divisão de documentos em partes menores (*chunking*).
- A Busca Vetorial do Oracle AI é integrada ao Oracle Database e permite consultar vetores e dados relacionais juntos.
- `VECTOR_DISTANCE` pode ser combinada com filtros SQL, como condições `WHERE`.

## Conclusão

Nesta lição, vimos como vetores e embeddings permitem representar significado e realizar buscas semânticas. Também conhecemos a Busca Vetorial do Oracle AI, integrada ao Oracle Database, e como ela combina busca por similaridade com consultas SQL.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
