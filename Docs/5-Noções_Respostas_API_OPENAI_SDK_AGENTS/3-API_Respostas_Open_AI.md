# API de Respostas da OpenAI

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar a API de Respostas da OpenAI, a interface principal para interagir com os modelos da plataforma. Ela permite enviar entradas, receber saídas estruturadas, habilitar ferramentas e encadear conversas entre turnos.

A API de Respostas é a API mais recente da OpenAI para esse tipo de interação. Ela foi lançada em março de 2025 e substitui e aprimora duas APIs anteriores: a API de Chat Completions e a API de Assistants. A recomendação apresentada nesta aula é usar a API de Respostas em vez dessas APIs mais antigas.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Reconhecer as principais funcionalidades da API de Respostas.
- Comparar a simplicidade de entrada e saída com a API de Chat Completions.
- Entender como encadear conversas usando o ID da resposta anterior.
- Identificar ferramentas integradas que podem ser habilitadas na chamada à API.
- Compreender como o modelo decide quando usar ferramentas.

### Benefícios para você

Ao conhecer os recursos da API de Respostas, você poderá simplificar a interação com os modelos, manter o contexto de conversas entre turnos e habilitar ferramentas sem precisar implementar toda a integração manualmente.

---

# Transcrição da aula

Bem-vindo(a) de volta. Nesta lição, vamos explorar a API de Respostas da OpenAI.

## 1. Principais funcionalidades

A API de Respostas permite enviar entradas, receber saídas estruturadas, habilitar o uso de ferramentas e encadear conversas entre turnos.

Entre suas funcionalidades mais importantes estão:

- **Entrada simples:** é possível enviar uma string ou uma entrada estruturada e receber um texto como resposta.
- **Encadeamento de conversas:** o ID da resposta anterior permite conectar interações entre turnos.
- **Integração com ferramentas:** ferramentas como busca na web e execução de código podem ser habilitadas na chamada à API.
- **Uso de ferramentas orientado pelo modelo:** o modelo decide quando chamar as ferramentas disponíveis.
- **Execução eficiente:** a API foi projetada para melhorar o desempenho e o armazenamento em cache.

Nesta lição, vamos nos concentrar nas três primeiras funcionalidades.

## 2. Configuração e chamada simples

Para acompanhar os exemplos, instale o pacote Python da OpenAI:

```bash
pip install openai
```

Também é necessário obter uma chave de API na plataforma da OpenAI e configurá-la como variável de ambiente:

```bash
# macOS ou Linux
export OPENAI_API_KEY="sua-chave"
```

```powershell
# Windows PowerShell
$env:OPENAI_API_KEY="sua-chave"
```

O cliente da OpenAI lê a chave do ambiente. Em uma chamada simples, você cria uma resposta com dois parâmetros principais: o modelo a utilizar — no exemplo da aula, GPT-4.1 — e a entrada, que pode ser uma string.

A resposta inclui a propriedade `output_text`, que permite acessar diretamente o texto gerado.

### Comparação com a API de Chat Completions

A API de Chat Completions espera um histórico de conversa estruturado como um array de mensagens. Para acessar o conteúdo gerado, é preciso percorrer a resposta, por exemplo, usando `response.choices[0].message.content`.

Com a API de Respostas, a entrada pode ser fornecida diretamente e o texto pode ser lido por meio de `output_text`. Isso torna a interação mais simples.

## 3. Encadeamento de conversas

Outro recurso importante é o gerenciamento de estado entre turnos. Na API de Chat Completions, era necessário rastrear e enviar manualmente o histórico da conversa a cada solicitação. À medida que a conversa crescia, isso podia exigir o envio de cada vez mais tokens.

Com a API de Respostas, você pode definir o ID da resposta anterior na nova solicitação. A OpenAI mantém o histórico no servidor, e a nova resposta dá continuidade à conversa sem que seja necessário reenviar todas as mensagens anteriores.

### Exemplo de continuidade

No primeiro turno do exemplo, informamos ao modelo que nosso nome é Alice e que gostamos de fazer trilhas. No turno seguinte, perguntamos qual é nosso nome e nosso hobby, passando o ID da resposta anterior.

O modelo recupera o contexto e responde que o nome é Alice e que ela gosta de fazer trilhas. Nos bastidores, cada resposta faz referência à anterior, formando uma cadeia de conversas que permite recuperar o contexto.

Esse recurso pode ser especialmente útil quando as ferramentas retornam grandes volumes de dados, pois evita transferir novamente todo o contexto entre o cliente e o servidor e simplifica o gerenciamento do estado da conversa.

## 4. Ferramentas integradas

A API de Respostas oferece ferramentas integradas que podem ser habilitadas na chamada à API. Entre elas estão:

- **Busca na web:** pesquisa informações atualizadas na internet.
- **Busca em arquivos:** pesquisa documentos carregados na plataforma, como documentos empresariais ou arquivos usados em um sistema de geração aumentada por recuperação (RAG).
- **Interpretador de código:** escreve e executa código Python, útil, por exemplo, para análise de dados.
- **Uso do computador:** permite que o modelo interaja com uma interface, clique em botões e preencha formulários. Na gravação, esse recurso é descrito como experimental ou beta.
- **Geração de imagens:** permite gerar imagens usando o DALL·E.

Para habilitar uma ferramenta, basta adicioná-la ao array `tools` da chamada à API `responses`. O modelo decide quando usar as ferramentas disponíveis e pode incorporar os resultados à resposta.

Por exemplo, diante de uma pergunta sobre os acontecimentos mais recentes em IA naquela semana, o modelo pode usar a busca na web. Já para responder qual é a capital da França, pode responder com base no conhecimento prévio sem fazer uma pesquisa.

## 5. Recapitulando

Nesta lição, vimos três funcionalidades principais da API de Respostas:

1. **Entrada e saída simplificadas:** você pode fornecer uma entrada direta e acessar o texto gerado por `output_text`.
2. **Encadeamento de conversas:** o ID da resposta anterior permite manter o contexto entre turnos.
3. **Ferramentas integradas:** ferramentas podem ser habilitadas na chamada, e o modelo decide quando utilizá-las.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
