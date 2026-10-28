# Demonstração: API de Respostas e SDK de Agentes

## Considerações iniciais

### Visão geral

Nesta demonstração, vamos colocar em prática os conceitos das aulas anteriores. Primeiro, veremos chamadas simples à API de Respostas da OpenAI. Depois, criaremos e executaremos um agente usando o SDK de Agentes.

Nos dois exemplos, é necessário ter os pacotes correspondentes instalados e uma chave da API da OpenAI configurada no ambiente.

### Objetivos de aprendizagem

Ao concluir esta demonstração, você será capaz de:

- Fazer uma chamada simples à API de Respostas.
- Acessar o texto gerado por meio de `response.output_text`.
- Reconhecer como fornecer mensagens estruturadas à API.
- Criar um agente com modelo, nome e instruções.
- Executar o agente de forma síncrona ou assíncrona.
- Comparar a chamada direta à API com a execução por meio do SDK de Agentes.

### Benefícios para você

Esta demonstração conecta os conceitos teóricos com exemplos de código. Ao comparar as duas abordagens, você poderá observar a diferença entre chamar a API diretamente e delegar ao SDK de Agentes a execução do loop do agente.

---

# Transcrição da demonstração

Bem-vindo(a) de volta. Nesta demonstração, vamos analisar primeiro a API de Respostas e, em seguida, o SDK de Agentes.

## 1. Preparação do ambiente

Para usar a API de Respostas, instale o pacote Python da OpenAI:

```bash
pip install openai
```

O cliente da OpenAI lê a chave de API configurada no ambiente. Essa chave é necessária para executar os exemplos.

## 2. Chamadas à API de Respostas

O exemplo mais simples cria um cliente e chama `client.responses`, informando o modelo — `gpt-5.5` no exemplo da demonstração — e uma entrada em texto.

O texto gerado pode ser acessado diretamente por meio de `response.output_text`. Por exemplo, a demonstração envia uma pergunta sobre o que é um agente de IA.

Também é possível fornecer mensagens estruturadas, como instruções de sistema e conteúdo enviado pelo usuário, de forma semelhante ao formato usado pela antiga API de Chat Completions. Um dos exemplos pede ao modelo que diferencie um chatbot de um agente.

## 3. Instalação do SDK de Agentes

Para acompanhar a parte da demonstração dedicada ao SDK de Agentes, instale o pacote:

```bash
pip install openai-agents
```

Assim como na chamada direta à API, também é necessário ter a chave da API da OpenAI configurada no ambiente.

## 4. Criando e executando um agente

Com o SDK, criamos um agente informando o modelo, um nome e as instruções. Em seguida, executamos o agente com uma pergunta.

Para uma execução síncrona, usamos `Runner.run_sync`. O SDK também oferece a opção assíncrona, `Runner.run`. O executor implementa o loop do agente e coordena as chamadas ao modelo e às ferramentas.

Na demonstração, o agente responde a perguntas diretas, como quem foi o primeiro presidente dos Estados Unidos e o que causou a Primeira Guerra Mundial. Os resultados são exibidos no terminal.

## 5. Comparando as abordagens

No primeiro exemplo, usamos diretamente a API de Respostas. No segundo, usamos o SDK de Agentes para definir e executar um agente.

A diferença principal é que, com a API de Respostas, fazemos a chamada diretamente. Com o SDK de Agentes, criamos um agente e usamos o executor para gerenciar seu loop.

## 6. Recapitulando

Nesta demonstração, vimos a API de Respostas e o SDK de Agentes em ação:

- A API de Respostas recebe uma entrada e permite acessar o texto gerado por `response.output_text`.
- O SDK de Agentes permite definir um agente com modelo, nome e instruções.
- O executor permite executar o agente de forma síncrona ou assíncrona e gerencia o loop de execução.

Espero que a demonstração tenha sido útil. Obrigado pelo seu tempo!
