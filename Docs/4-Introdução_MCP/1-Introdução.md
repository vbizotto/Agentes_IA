# Introdução ao Módulo — Model Context Protocol (MCP)

## Considerações iniciais

### Visão geral

Neste módulo, vamos explorar o Model Context Protocol (MCP), um padrão aberto introduzido pela Anthropic em novembro de 2024 para padronizar a conexão entre modelos de IA e ferramentas externas, fontes de dados e sistemas de execução.

A proposta central do MCP é simplificar a integração entre agentes e recursos externos, reduzindo a necessidade de adapters personalizados e criando uma interface comum para comunicação entre componentes.

### Objetivos de aprendizagem

Ao concluir esta introdução, você será capaz de:

- Explicar o que é o MCP e por que ele foi criado.
- Entender a arquitetura básica do protocolo, incluindo hosts, clientes, servidores e primitivas.
- Reconhecer como o MCP altera a forma como um agente acessa ferramentas e dados.
- Comparar a arquitetura antes e depois da adoção do MCP.
- Identificar os pontos em que o MCP se encaixa em sistemas reais de produção.

### Benefícios para você

Este módulo conecta os conceitos estudados nos módulos anteriores com uma nova camada de integração: a forma como agentes de IA se conectam com o mundo externo de maneira padronizada. Ao compreender o MCP, você passa a enxergar melhor como ferramentas, memória, contexto e execução podem ser organizados em sistemas mais robustos e escaláveis.

---

# Transcrição da introdução

Bem-vindo(a) a este módulo sobre Model Context Protocol (MCP).

## 1. O que é o MCP?

O MCP significa Model Context Protocol, ou Protocolo de Contexto de Modelo. Ele é um padrão aberto criado para padronizar a comunicação entre modelos de IA e recursos externos.

Em vez de cada modelo ou agente precisar implementar integrações específicas para cada ferramenta, banco de dados, API ou serviço, o MCP oferece uma interface comum. Isso reduz complexidade, melhora reutilização e torna a arquitetura mais previsível.

## 2. Por que o MCP existe?

Conforme os agentes de IA evoluem, eles precisam acessar cada vez mais ferramentas externas e fontes de dados. No entanto, essa integração não é trivial.

Cada sistema externo possui:

- uma API específica;
- um contrato de autenticação diferente;
- formatos de entrada e saída distintos;
- regras de segurança e limitações próprias.

O MCP nasce para padronizar esse processo. Em vez de cada aplicação construir suas próprias integrações, o padrão define uma forma comum de conectar o modelo ao ambiente externo.

## 3. Estrutura do protocolo

Neste módulo, vamos explorar os principais componentes da arquitetura do MCP:

- host: a aplicação que executa o agente ou o ambiente do usuário;
- cliente: o componente que se conecta ao servidor MCP;
- servidor: o serviço que expõe ferramentas e recursos;
- primitivas: operações padronizadas para troca de contexto, execução e comunicação.

Esses elementos formam a base da arquitetura. Entender cada um deles é essencial para ver como o MCP funciona na prática.

## 4. O mesmo exemplo de agente em outro contexto

Como no módulo anterior, usaremos um exemplo de agente que resolve uma questão matemática simples, mas que exige a chamada de várias ferramentas.

Esse é um exemplo útil porque permite comparar a arquitetura antes e depois do MCP sem perder o foco no comportamento do agente.

## 5. Arquitetura antes e depois do MCP

Uma das partes mais valiosas deste módulo será observar como a arquitetura muda quando o agente passa a interagir com um servidor MCP.

Antes do MCP, a arquitetura costuma ser mais acoplada. O agente, ou a aplicação, precisa conhecer diretamente as ferramentas que vai chamar e implementar a lógica de integração manualmente.

Com o MCP, a complexidade é encapsulada em um servidor padronizado. O cliente continua sendo responsável por orquestrar o agente, mas a conexão com as ferramentas é tratada de forma mais modular e consistente.

## 6. Aprendizado prático

Neste módulo, criaremos um novo servidor matemático MCP. Essa escolha é intencional: ela permite ver, de forma didática, como a arquitetura é montada e como o agente passa a se comunicar com as ferramentas por meio do protocolo.

Ao comparar a solução antes e depois da implementação, você vai perceber com clareza como o MCP transforma a arquitetura e o código.

## 7. O que você verá no restante do módulo

Ao longo das lições, vamos:

1. construir a base conceitual do MCP;
2. explicar como ele funciona na prática;
3. analisar os componentes essenciais da arquitetura;
4. observar um agente em execução integrado ao MCP;
5. ver um exemplo real de uso em contexto de ferramenta matemática;
6. refletir sobre o que muda e o que permanece igual no código quando você adota o padrão.

## 8. Conclusão

O objetivo deste módulo é simples, mas importante: além de entender o MCP conceitualmente, você precisa perceber exatamente onde ele se encaixa em sistemas reais de IA e em agentes autônomos.

Ao final, você não apenas saberá o que é o MCP, mas também compreenderá como ele impacta arquitetura, integração e evolução de sistemas de IA.

Vamos começar!