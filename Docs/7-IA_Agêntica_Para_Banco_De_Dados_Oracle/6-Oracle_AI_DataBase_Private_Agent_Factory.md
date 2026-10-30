# Oracle AI Database Private Agent Factory

## Considerações iniciais

### Visão geral

Nesta lição, vamos conhecer o Oracle AI Database Private Agent Factory, uma plataforma sem código para criar, testar e implantar agentes de IA corporativos. Veremos seus agentes pré-configurados, as opções de integração com dados e serviços, os modos de implantação e o construtor visual de fluxos de trabalho.

---

# Transcrição da aula

## 1. O que é o Agent Factory

O Agent Factory permite que usuários de negócios e engenheiros criem agentes inteligentes sem escrever código. A plataforma foi projetada para trabalhar com fontes de dados aprovadas e recursos do Oracle Database, mantendo os controles de segurança e governança esperados em ambientes corporativos.

A criação de agentes envolve mais do que desenhar um fluxo: também é necessário conectar dados confiáveis, escolher e configurar um modelo de linguagem (LLM), aplicar controles de acesso e publicar o agente de forma controlada.

## 2. Recursos e integrações

O Agent Factory inclui dois agentes pré-configurados — o Agente de Conhecimento e o Agente de Análise de Dados —, além de um Construtor de Agentes visual e modelos para fluxos de trabalho personalizados.

A plataforma oferece suporte a integrações e controles como:

- fontes de dados de banco de dados;
- fontes de API REST;
- servidores MCP;
- logon único e gerenciamento de funções;
- diretrizes de prompts;
- respostas vinculadas às fontes.

## 3. Fluxo de uma solicitação

Um usuário de negócios faz uma pergunta em linguagem natural. O Agent Factory encaminha a solicitação pela lógica ou pelo fluxo de trabalho do agente, que pode:

- chamar um LLM configurado;
- recuperar conteúdo aprovado;
- consultar dados estruturados;
- chamar uma ferramenta.

Depois de processar a solicitação, o agente retorna uma resposta ao usuário.

## 4. Opções de implantação

O Agent Factory pode ser implantado como um aplicativo conteinerizado, executado com Podman e Podman Compose. O aplicativo requer acesso ao Oracle AI Database 26ai e a um endpoint de LLM configurado.

A aula apresenta dois modos de instalação:

- **Modo de produção:** utiliza o banco de dados e os endpoints de modelo fornecidos pelo usuário.
- **Modo de Início Rápido:** utiliza contêineres locais, incluindo o contêiner gratuito do Oracle AI Database 26ai, para uma avaliação rápida.

O serviço pode ser executado localmente, na OCI ou em ambientes multicloud, como AWS, Azure e Google Cloud, desde que o Oracle AI Database esteja disponível.

## 5. Agente de Conhecimento

O Agente de Conhecimento é voltado à busca corporativa e a perguntas sobre conteúdo não estruturado aprovado pela organização. Ele combina a Busca Vetorial do Oracle AI com os recursos de um LLM e fontes de dados autorizadas.

Entre as fontes citadas estão SharePoint, Google Drive, websites, arquivos carregados e sistemas de arquivos. Depois que uma fonte é configurada, o processamento pode ser automatizado: o conteúdo é recuperado, analisado, armazenado, dividido em partes, convertido em embeddings e preparado para recuperação.

Quando o usuário faz uma pergunta, o agente recupera o contexto aprovado mais relevante e gera uma resposta fundamentada. A rastreabilidade permite consultar as fontes usadas para apoiar a resposta.

## 6. Agente de Análise de Dados

O Agente de Análise de Dados trabalha com dados estruturados diretamente no banco de dados corporativo. Ele interpreta esquemas e usa recursos de LLM para gerar consultas SQL, explicações, tabelas e visualizações.

O agente pode se conectar ao Oracle Database 19c ou superior, incluindo o Oracle AI Database 26ai e o Autonomous Database, além de instâncias autogerenciadas ou em nuvem configuradas como fontes de dados.

A interação é conversacional: o usuário faz uma pergunta de negócio, o agente a converte em SQL, executa a consulta com segurança e apresenta os resultados como dados estruturados, visualizações, consultas SQL e explicações. O agente também pode sugerir perguntas de acompanhamento com base na análise dos resultados.

## 7. Construtor de Agentes

O Construtor de Agentes é uma interface visual de arrastar e soltar para projetar, prototipar e implantar agentes sem programação. Os fluxos de trabalho são montados com nós, incluindo:

- nós de LLM e de agentes;
- nós de ferramentas e integrações, como APIs REST, servidores MCP, Select AI e busca na Wikipédia;
- nós de saída, como respostas de chat ou e-mails.

Um fluxo simples pode encaminhar uma pergunta a um LLM e retornar a resposta. Fluxos com ferramentas podem chamar APIs, servidores MCP ou outros serviços configurados. Fluxos avançados podem incluir componentes personalizados em Python e orquestração multiagente, com um agente gerenciador delegando tarefas a subagentes especializados.

Depois de construir o fluxo, é possível testá-lo e aprimorá-lo no ambiente de testes. Quando estiver pronto, o agente pode ser publicado, expondo um endpoint de API que aplicações podem invocar por requisições `POST`.

## 8. Recapitulando os pontos principais

- O Agent Factory oferece uma abordagem sem código para criar e implantar agentes corporativos.
- A plataforma inclui o Agente de Conhecimento, o Agente de Análise de Dados e um construtor visual.
- As integrações incluem bancos de dados, APIs REST e servidores MCP, com controles de acesso e governança.
- O Agente de Conhecimento recupera conteúdo não estruturado aprovado e fornece respostas com fontes rastreáveis.
- O Agente de Análise de Dados consulta dados estruturados e apresenta resultados em diferentes formatos.
- Fluxos criados no Construtor de Agentes podem ser testados e publicados como endpoints de API.

## Conclusão

Nesta lição, vimos como o Oracle AI Database Private Agent Factory ajuda a criar, integrar, testar e implantar agentes corporativos sem código. A plataforma combina agentes pré-configurados e fluxos personalizados, conectando dados e ferramentas sob controles de segurança e governança.

Espero que esta lição tenha sido útil.
