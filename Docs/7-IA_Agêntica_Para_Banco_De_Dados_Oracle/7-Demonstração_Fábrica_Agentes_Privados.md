# Demonstração: Oracle AI Database Private Agent Factory

## Considerações iniciais

### Visão geral

Nesta demonstração, vamos explorar os agentes pré-configurados do Private Agent Factory — o Agente de Conhecimento e o Agente de Análise de Dados — e criar um fluxo simples com o Construtor de Agentes. O objetivo é observar como a plataforma permite configurar, testar e publicar agentes sem escrever código.

---

# Transcrição da aula

## 1. Agente de Conhecimento

O Agente de Conhecimento é um sistema de geração aumentada por recuperação (RAG) voltado a perguntas sobre dados não estruturados, como documentos internos, websites e arquivos. Ele retorna respostas sintetizadas com citações que apontam para as seções relevantes das fontes.

Na demonstração, o agente é consultado sobre como configurar o Private Agent Factory. A resposta descreve os modos de Produção e de Início Rápido e inclui links para a documentação relacionada.

As fontes de dados usadas pelo agente são configuradas previamente. Neste exemplo, o agente consulta a documentação do Private Agent Factory. A instalação demonstrada está em uma máquina virtual, acessível por um endereço IP e pela porta `8080`. A documentação do produto descreve os requisitos da máquina virtual e as etapas de instalação pelo OCI Marketplace.

## 2. Agente de Análise de Dados

O Agente de Análise de Dados trabalha com dados estruturados. Ele pode gerar consultas SQL, gráficos, tabelas e resumos em linguagem natural. Também oferece o Modo de Exploração, que examina um conjunto de dados e produz perguntas e respostas de exemplo.

Na demonstração, é criado um agente para o conjunto de dados da Netflix:

1. Seleciona-se o conjunto de dados.
2. Define-se o nome e a descrição do agente.
3. Publica-se o agente.
4. Usa-se o Modo de Exploração para gerar análises do conjunto de dados.

Entre os exemplos de perguntas estão quantos títulos foram adicionados por gênero desde janeiro de 2020 e quais filmes foram lançados antes de 2000, mas adicionados nos últimos cinco anos, junto com suas classificações.

## 3. Construtor de Agentes

Além dos agentes pré-configurados, o Private Agent Factory oferece o Construtor de Agentes, uma interface visual para criar fluxos de trabalho sem código.

Na demonstração, é montado um agente simples com os seguintes componentes:

1. Um campo de entrada de chat.
2. Um agente configurado para usar o LLM Grok.
3. Uma saída de chat conectada à resposta do agente.

Os componentes são conectados visualmente, arrastando a entrada para o prompt do agente e a resposta do agente para a saída de chat. Depois de salvar o fluxo, ele pode ser testado no playground com uma pergunta, como “O que é o Oracle AI Vector Search?”.

Esse exemplo mostra o fluxo básico de entrada, processamento pelo LLM e resposta. O Construtor também oferece componentes adicionais para criar fluxos mais avançados.

## 4. Recapitulando os pontos principais

- O Agente de Conhecimento responde a perguntas sobre dados não estruturados e inclui referências às fontes.
- O Agente de Análise de Dados trabalha com dados estruturados e pode gerar SQL, tabelas, gráficos e análises.
- O Modo de Exploração cria exemplos de perguntas e respostas sobre um conjunto de dados.
- O Construtor de Agentes permite montar fluxos visualmente, conectando entradas, agentes, LLMs e saídas.
- Os agentes e fluxos podem ser testados antes de serem usados.

## Conclusão

Nesta demonstração, exploramos os dois agentes pré-configurados do Private Agent Factory e criamos um fluxo simples no Construtor de Agentes. A plataforma combina agentes prontos para diferentes tipos de dados com a flexibilidade de criar e testar fluxos personalizados sem código.

Espero que esta demonstração tenha sido útil. Obrigado pelo seu tempo!
