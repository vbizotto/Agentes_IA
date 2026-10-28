# O que é MCP?

## Considerações iniciais

### Visão geral

Bem-vindos de volta. Nesta lição, vamos construir a base do que é o MCP e por que ele existe.

MCP significa `Model Context Protocol` (Protocolo de Contexto de Modelo). É um padrão aberto que permite que aplicações de IA se conectem a ferramentas externas, fontes de dados e sistemas de forma consistente. A frase mais importante aqui é: "padrão aberto". Ele não está vinculado a um único fornecedor.

O protocolo é baseado em `JSON-RPC 2.0`, uma forma simples e amplamente utilizada de comunicação estruturada por requisição e resposta.

### Entendendo o termo JSON-RPC

`JSON-RPC` significa `JavaScript Object Notation Remote Procedure Call` (Chamada de Procedimento Remoto em Notação de Objeto JavaScript). Em termos práticos, ele é um protocolo de comunicação baseado em JSON para chamadas de procedimento remoto.

Abordaremos os detalhes dessa tecnologia na próxima lição. Por enquanto, pense no MCP como uma "linguagem comum" que ambas as partes concordam em usar: a aplicação de IA e a ferramenta.

Você frequentemente ouvirá a analogia do `USB-C para IA`. Assim como o USB-C permite que qualquer dispositivo se conecte a qualquer porta compatível, o MCP permite que qualquer cliente compatível se conecte a qualquer servidor compatível. Essa é a ideia central por trás da padronização da conectividade.

---

# Transcrição da aula

## 1. O problema que o MCP resolve

Antes do MCP, cada aplicação de IA precisava criar integrações personalizadas com cada ferramenta. Esse era o principal problema.

Imagine um cenário com três aplicações de IA e quatro ferramentas diferentes. Para que todas as combinações funcionassem, seria necessário criar 12 integrações separadas. Isso acontece porque cada aplicação de IA precisa se conectar a cada ferramenta individualmente.

Esse cenário é normalmente chamado de problema de "n vezes m". Ele cresce rapidamente e fica muito difícil de manter. Aqui:

- `n` = número de aplicações de IA
- `m` = número de ferramentas

O resultado é um conjunto de integrações customizadas, com muita infraestrutura e muito trabalho necessário para manter tudo funcionando.

## 2. Como o MCP muda essa realidade

O MCP altera esse cenário completamente. Agora, cada aplicativo de IA cria um cliente MCP, e cada ferramenta expõe um servidor MCP.

Lembre-se do slide anterior: qualquer cliente compatível com MCP pode se comunicar com qualquer servidor compatível com MCP, independentemente de quem o criou.

Em vez de 12 integrações, o cenário passa a exigir apenas 7 conexões: 3 para os aplicativos de IA e 4 para as ferramentas. Isso transforma um problema de complexidade quadrática (`n x m`) em um problema de complexidade linear (`n + m`).

É por isso que o MCP é tão importante.

## 3. Arquitetura do MCP

Agora, vamos dar uma olhada rápida na arquitetura do MCP. É fundamental entender esse modelo, porque neste módulo vamos construir sobre ele.

A arquitetura do MCP tem três participantes principais:

- `Host`
- `Cliente`
- `Servidor`

### Host

O `host` é o aplicativo de IA com o qual o usuário interage. Pode ser o Claude Desktop, o Cursor, o Visual Studio Code ou qualquer outro ambiente de IA compatível com MCP.

Dentro do host, existe um `LLM` (modelo de IA), que realiza o raciocínio e a tomada de decisão. O host também cria um ou mais clientes MCP.

### Cliente MCP

O cliente MCP fica dentro do host e mantém uma conexão dedicada com um servidor MCP específico.

Na arquitetura, você pode visualizar vários clientes, como `Cliente MCP 1`, `Cliente MCP 2` e `Cliente MCP 3`. Cada um deles representa uma conexão individual e separada com um servidor MCP.

### Servidor MCP

Os servidores MCP são programas que fornecem contexto para o cliente. Isso pode incluir:

- ferramentas para executar ações;
- dados para leitura;
- modelos de prompt.

Cada servidor pode se conectar a sistemas externos, como GitHub, Slack, bancos de dados ou até mesmo o sistema de arquivos local.

## 4. Independência entre cliente e servidor

A ideia central aqui é que o cliente e o servidor são independentes. O servidor não se importa com qual aplicação está fazendo a chamada. Enquanto o protocolo for respeitado, qualquer cliente pode se conectar a qualquer servidor.

Isso permite uma interoperabilidade muito maior entre diferentes ferramentas e diferentes aplicações de IA.

## 5. Recapitulando os pontos principais

Vamos recapitular alguns pontos importantes:

- O `host` gerencia a aplicação de IA e cria o cliente;
- cada cliente se conecta a exatamente um servidor;
- os servidores expõem ferramentas, dados e prompts;
- a comunicação é feita por meio de `JSON-RPC 2.0`;
- os servidores podem ser executados localmente ou remotamente.

Uma questão importante que vamos abordar mais adiante neste módulo é como o host gerencia a agregação de contexto entre vários clientes.

Se você tiver três clientes, como o sistema consegue reunir e organizar todas as informações? Esse é um assunto mais avançado, mas vale a pena explorá-lo.

### Clientes especializados

Existe também a possibilidade de usar clientes especializados. Por exemplo, o cliente MCP multi-servidor da LangChain pode carregar ferramentas, prompts e recursos de vários servidores em um único cliente, simplificando o gerenciamento.

É importante deixar claro que cada cliente normalmente se conecta a um único servidor. Mas existem abordagens especializadas para gerenciar múltiplos servidores de forma mais eficiente.

## 6. Transporte e comunicação

Outra parte relevante é que o `JSON-RPC 2.0` suporta dois mecanismos principais de transporte:

- transporte padrão de entrada/saída, usado para servidores locais;
- transporte `HTTP` em fluxo, usado para servidores remotos.

Esses detalhes serão explorados com mais profundidade na próxima lição.

---

## Conclusão

Esta lição foi uma breve introdução ao que é o MCP, ao problema que ele resolve e à arquitetura por trás do protocolo.

Lembrem-se: existe um `host` com um modelo de IA e vários clientes conectados a servidores MCP. O cliente e o servidor são independentes entre si, e essa separação é um dos pontos centrais da proposta do MCP.

A ideia principal por trás do protocolo é padronizar a conectividade entre aplicações de IA e ferramentas externas.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
