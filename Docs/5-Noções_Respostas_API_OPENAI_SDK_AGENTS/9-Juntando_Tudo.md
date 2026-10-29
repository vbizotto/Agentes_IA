# Juntando tudo

## Considerações iniciais

### Visão geral

Nesta lição, vamos reunir os conceitos apresentados ao longo do módulo em um exemplo de sistema fictício de suporte ao cliente. A arquitetura combina um agente de triagem, agentes especialistas, transferências (*handoffs*), ferramentas personalizadas, busca na web, *guardrails* de entrada e rastreamento.

Também vamos acompanhar o rastreamento de uma solicitação sobre o status de um pedido para entender como essas partes colaboram durante a execução.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Reconhecer como os principais componentes do SDK de Agentes se integram em um projeto.
- Descrever a função do agente de triagem e dos agentes especialistas.
- Acompanhar o fluxo de uma solicitação protegida por um *guardrail*.
- Entender como uma ferramenta personalizada fornece dados ao agente.
- Usar o rastreamento para analisar etapas e identificar possíveis gargalos.

### Benefícios para você

Um exemplo integrado ajuda a visualizar como agentes, ferramentas e mecanismos de proteção trabalham em conjunto. O rastreamento complementa essa visão ao mostrar onde o tempo foi gasto e como o agente chegou à resposta, apoiando a depuração e a otimização.

---

# Transcrição da aula

Bem-vindos à última aula deste módulo, em que vamos reunir os conceitos vistos anteriormente: a pilha de agentes da OpenAI, a API de Respostas, o SDK de Agentes, as ferramentas e chamadas de função, os sistemas multiagentes e os mecanismos de proteção.

## 1. Arquitetura do exemplo

Vamos criar um sistema fictício de suporte ao cliente. Um agente de triagem recebe as mensagens e as encaminha, por meio de transferências, a um de três agentes especialistas:

- **Status do Pedido:** consulta os detalhes do pedido usando uma função personalizada escrita em Python.
- **Reembolso:** trata solicitações de reembolso usando uma função personalizada.
- **Perguntas Frequentes:** responde a perguntas gerais usando uma ferramenta hospedada de busca na web.

Além dos agentes e das ferramentas, o sistema usa um *guardrail* de entrada para bloquear perguntas fora do escopo do suporte. Assim, o exemplo combina transferências, funções personalizadas, uma ferramenta hospedada e proteção de entrada.

## 2. O papel do rastreamento

O rastreamento permite acompanhar as etapas executadas pelo sistema. Na demonstração da aula, a execução levou aproximadamente 11,4 segundos e envolveu quatro chamadas à API de Respostas. A maior parte do tempo observado foi gasto nessas chamadas ao modelo, enquanto a lógica do *guardrail*, as transferências e a função de consulta do pedido levaram apenas alguns milissegundos.

Esses valores descrevem aquela execução específica. Os tempos podem variar conforme o modelo, a rede, a configuração e as condições de execução.

O rastreamento é útil para entender o fluxo, depurar problemas e identificar oportunidades de otimização. Neste exemplo, ele sugere que reduzir o número ou o tamanho das chamadas ao modelo poderia ter mais impacto no tempo total do que otimizar a função local de consulta do pedido.

## 3. Exemplo: consulta do status de um pedido

Considere a pergunta: “Onde está meu pedido?”. O cliente informa o número `ORD-001`. O fluxo acontece em duas fases.

### Fase 1: proteção e triagem

Antes de o agente principal processar a solicitação, o *guardrail* verifica se ela é relacionada ao suporte ao cliente. Na demonstração, essa verificação usa um agente auxiliar e uma chamada ao modelo. Como a pergunta é sobre um pedido, a proteção é aprovada e a solicitação pode prosseguir.

Em seguida, o agente de triagem analisa a pergunta e suas instruções. Como se trata do status de um pedido, ele transfere o controle para o agente **Status do Pedido**. A transferência muda qual agente está conduzindo a conversa; no exemplo, ela não exige uma chamada adicional ao modelo.

### Fase 2: consulta e resposta

O agente **Status do Pedido** recebe a conversa e disponibiliza ao modelo o esquema da ferramenta `Lookup Order`. O modelo decide chamá-la, e a função Python local consulta os dados do pedido — armazenados, no exemplo, em um dicionário — e retorna o resultado.

O modelo recebe esses dados e faz outra chamada para redigir uma resposta clara e amigável ao cliente. Em uma aplicação real, a função poderia consultar um banco de dados ou um serviço remoto; nesse caso, o tempo de resposta dependeria também desse serviço e da rede.

## 4. Analisando o fluxo e o desempenho

O rastreamento reúne as etapas da execução: a verificação de entrada, as chamadas ao modelo, a transferência para o especialista e a chamada da ferramenta. Na demonstração, a verificação inicial levou pouco mais de cinco segundos, e a etapa do agente de status levou cerca de quatro segundos. Esses tempos são observações do exemplo, não garantias de desempenho.

Essa visão ajuda a investigar questões como:

- O *guardrail* permitiu ou bloqueou a solicitação?
- O agente de triagem escolheu o especialista adequado?
- A ferramenta recebeu os dados esperados e retornou o resultado correto?
- Qual etapa concentrou a maior parte do tempo ou das chamadas ao modelo?

A partir dessas informações, é possível decidir onde concentrar esforços de depuração ou otimização. No exemplo apresentado, as chamadas ao modelo foram o principal componente do tempo total.

## 5. Recapitulando

Nesta lição, reunimos os conceitos do módulo em um sistema de suporte ao cliente com agente de triagem, especialistas, transferências, funções personalizadas, busca na web e um *guardrail* de entrada.

Também acompanhamos uma consulta de pedido do início ao fim e vimos como o rastreamento mostra as etapas executadas e ajuda a analisar o desempenho. Os tempos observados pertencem à demonstração e podem mudar em outras condições.

Espero que esta aula tenha sido útil. Obrigado pelo seu tempo!
