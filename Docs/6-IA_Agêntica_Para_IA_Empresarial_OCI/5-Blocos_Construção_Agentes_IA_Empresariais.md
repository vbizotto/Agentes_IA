# Blocos de construção de agentes de IA empresariais

## Considerações iniciais

### Visão geral

Nesta lição, vamos conhecer os principais blocos de construção do serviço OCI Enterprise AI Agents: a API de Respostas, as ferramentas, a memória e algumas APIs de nível inferior.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Descrever os recursos apresentados da API de Respostas da OCI.
- Identificar as quatro categorias de ferramentas integradas mencionadas na aula.
- Diferenciar os tipos de memória oferecidos pelo serviço.
- Reconhecer quando APIs de nível inferior podem ser úteis.

### Benefícios para você

Conhecer esses componentes ajuda a escolher os recursos adequados para cada aplicação, desde ferramentas gerenciadas e memória de conversa até fluxos personalizados de recuperação, armazenamento e execução.

---

# Transcrição da aula

Bem-vindos a esta lição sobre os blocos de construção de agentes de IA empresariais da OCI. Vamos analisar a API de Respostas, as ferramentas, a memória e algumas APIs de nível inferior.

## 1. API de Respostas da OCI

A API de Respostas da OCI é apresentada como a principal API para criar agentes. Segundo a aula, ela é compatível com OpenAI e está em conformidade com a especificação Open Responses.

A API oferece suporte a raciocínio em várias etapas e chamadas de ferramentas. O modelo pode solicitar ferramentas — como um interpretador de código, busca de arquivos, funções personalizadas ou servidores MCP — durante o fluxo da solicitação.

A aula também apresenta o roteamento multimodelo, que permite usar modelos diferentes para tarefas distintas. Entre os provedores e modelos citados estão OpenAI, Grok, Gemini, Llama e Cohere; a disponibilidade pode variar.

O estado da conversa pode ser gerenciado com recursos como a API OCI Conversations, memória de longo prazo e compactação de contexto. Assim, é possível manter informações relevantes entre interações sem precisar montar manualmente toda a infraestrutura de conversa. Consulte a documentação atual para verificar os recursos e requisitos disponíveis.

## 2. Ferramentas do agente

As ferramentas ampliam o que um agente pode fazer além de gerar texto. Com elas, o agente pode pesquisar documentos, executar código, chamar APIs da empresa e conectar-se a servidores MCP.

A aula destaca quatro categorias de ferramentas integradas:

1. **Busca de arquivos:** recupera informações de documentos carregados usando busca semântica.
2. **Interpretador de código:** executa código Python em um ambiente isolado para análise e computação de dados.
3. **Chamada de funções:** permite definir funções Python personalizadas que o agente pode invocar, por exemplo, para consultar dados ou acionar um fluxo de trabalho.
4. **Chamada MCP:** conecta o agente a servidores MCP remotos para integrar ferramentas de maneira padronizada.

Uma forma simples de pensar nessa relação é: o modelo interpreta e decide; as ferramentas permitem que o agente interaja com dados e sistemas externos.

## 3. Memória

O serviço OCI Enterprise AI Agents apresenta três tipos de memória:

### Memória de curto prazo

A API de Conversas gerencia o histórico de uma conversa durante uma sessão. Isso permite que o agente use informações mencionadas anteriormente na mesma interação.

### Memória de longo prazo

A memória de longo prazo pode reter informações entre sessões, como preferências do usuário, decisões anteriores ou conhecimento acumulado, conforme a configuração da aplicação.

### Otimização ou compactação de contexto

A compactação de contexto resume conversas longas para ajudar a mantê-las dentro da janela de contexto do modelo, preservando as informações consideradas relevantes.

Como analogia, a memória de curto prazo é como anotações feitas durante uma reunião; a memória de longo prazo, como um diário; e a compactação de contexto, como resumir uma reunião extensa em seus principais pontos.

## 4. APIs de nível inferior

Além dos recursos de alto nível, a OCI oferece APIs de nível inferior para criar fluxos personalizados de recuperação, armazenamento e execução. A aula cita:

- **API Vector Stores:** gerencia armazenamentos vetoriais usados em busca semântica. Documentos podem ser enviados, divididos em partes e convertidos em vetores para recuperação.
- **API de Arquivos:** permite enviar e gerenciar arquivos que o agente precisa processar.
- **API de Contêineres:** permite executar contêineres personalizados para processamento especializado.

Esses recursos podem ser úteis em casos como pipelines RAG personalizados, processamento especializado de dados e execução de ferramentas em ambientes isolados. Nem toda aplicação precisa chamá-los diretamente: muitos casos podem ser atendidos pela API de Respostas e pelas ferramentas de alto nível.

A aula também observa que há outras APIs e que algumas são compatíveis com o estilo OpenAI. Consulte a documentação atual para confirmar compatibilidade e disponibilidade.

## 5. Recapitulando

Nesta lição, conhecemos quatro blocos de construção do serviço OCI Enterprise AI Agents: a API de Respostas, as ferramentas, os tipos de memória e as APIs de nível inferior.

A API de Respostas coordena interações com o modelo e ferramentas; as ferramentas permitem executar tarefas; a memória ajuda a manter contexto; e as APIs de nível inferior oferecem mais controle sobre arquivos, armazenamento vetorial e contêineres.

Os recursos e as ferramentas disponíveis podem mudar. Consulte a documentação atual da OCI ao definir a arquitetura da sua aplicação.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
