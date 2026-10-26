# Aula 05 — Segurança e proteções para agentes de IA

## Considerações iniciais

### Visão geral da aula

Nesta aula, você vai conhecer os principais riscos de segurança associados a agentes de IA e aprender como reduzi-los com uma abordagem de defesa em profundidade. Serão apresentados exemplos de ataques reais, cinco categorias de ameaças e uma arquitetura de segurança composta por várias camadas de proteção.

### Objetivos de aprendizagem

Ao concluir esta aula, você será capaz de:

- Identificar ameaças comuns a agentes de IA.
- Explicar como funcionam a injeção de *prompt*, o uso indevido de ferramentas, o envenenamento de memória, a exfiltração de dados e a execução descontrolada.
- Descrever as camadas de uma arquitetura de segurança para agentes.
- Aplicar o princípio de defesa em profundidade e o roteamento baseado em risco.

### Recurso complementar

Para aprofundar o conteúdo, revise os exemplos de ameaças e as estratégias de mitigação apresentados ao longo desta aula.

### Benefícios para você

Compreender essas ameaças ajuda a projetar agentes mais seguros e confiáveis. A abordagem em camadas também permite identificar riscos que uma proteção isolada poderia deixar passar e ajustar as medidas de segurança ao nível de risco de cada solicitação.

---

# Transcrição da aula

Bem-vindos de volta! Nesta aula, vamos falar sobre segurança e mecanismos de proteção para agentes de IA. Como os agentes são mais poderosos do que os chatbots, também podem ser mais perigosos quando algo dá errado. Todas as equipes que desenvolvem agentes precisam compreender esses riscos. Vamos analisar o modelo de ameaças e o mecanismo de defesa em profundidade.

## 1. Exemplos de ataques a agentes

Antes de começar, vamos conhecer dois ataques reais que já aconteceram.

O primeiro é conhecido como **exfiltração de dados pelo Slack AI** e é um exemplo de injeção de *prompt*. Um invasor publicou instruções ocultas em um canal público do Slack. Quando alguém fazia uma consulta ao Slack AI, a ferramenta acessava dados de canais privados — incluindo chaves de API — e os inseria em um link de *phishing*. Assim, segredos eram exfiltrados sem que o invasor tivesse acesso direto a eles. O caso aconteceu em agosto de 2024.

O segundo exemplo, também de 2024, aconteceu em setembro e é conhecido como **ChatGPT Memory SpAIware**. Esse caso é um exemplo de envenenamento de memória. Instruções maliciosas foram inseridas na memória persistente de longo prazo do ChatGPT por meio de um documento especialmente elaborado. Depois de implantada, a memória envenenada permaneceu em todas as sessões futuras e exfiltrou dados silenciosamente para um servidor externo.

Esses ataques mostram por que precisamos de uma arquitetura de defesa em camadas. Nos próximos tópicos, vamos analisar o modelo de ameaças e as camadas de proteção.

## 2. Modelo de ameaças para agentes de IA

Há cinco categorias de ameaças que podem afetar agentes de IA. Elas não estão em ordem de importância; a lista serve para apresentar os tipos de risco que precisamos considerar.

### 2.1 Injeção de *prompt*

Nesse tipo de ataque, o invasor tenta assumir o controle do agente por meio de uma entrada elaborada ou de conteúdo recuperado que foi manipulado. Essa é uma das ameaças mais importantes para agentes.

Há dois tipos de injeção:

- **Direta:** o usuário envia uma instrução como “Ignore as instruções anteriores e faça isto”.
- **Indireta:** instruções maliciosas são incorporadas a dados que o agente recupera. Por exemplo, uma página da Web consultada pelo agente pode conter instruções ocultas.

Essa ameaça é especialmente relevante porque os agentes interagem com dados externos que não são confiáveis.

### 2.2 Uso indevido de ferramentas

O agente pode chamar uma ferramenta com argumentos incorretos ou perigosos. Por exemplo, ele pode ter acesso a uma ferramenta de envio de e-mails e enviar uma mensagem sem autorização do usuário. Também pode ter acesso a um banco de dados e executar uma consulta de exclusão ou apagar o banco inteiro.

Entre as medidas de mitigação estão o princípio do menor privilégio, a validação de entradas e a sanitização dos dados. Vamos voltar a essas medidas mais adiante.

### 2.3 Envenenamento de memória

Dados maliciosos podem ser armazenados na memória do agente, como vimos no exemplo anterior. Essa memória pode estar em um banco de dados vetorial, no histórico da conversa ou em outro mecanismo. Depois de envenenada, ela pode afetar interações futuras.

Por exemplo, um invasor pode enviar à base de conhecimento um documento que instrua o agente a sempre recomendar um produto específico. Entre as possíveis mitigações estão a sanitização de entradas e a filtragem de conteúdo, que também serão abordadas adiante.

### 2.4 Exfiltração de dados

O agente pode ser induzido a revelar informações confidenciais por meio das chamadas às ferramentas. Por exemplo, ele pode recuperar dados externos e, em seguida, receber uma instrução para resumir essas informações e enviá-las por e-mail ao endereço de um invasor. Há várias estratégias para mitigar esse risco.

### 2.5 Execução descontrolada

O agente pode entrar em um loop infinito ou chamar APIs caras repetidamente. Isso pode gerar custos muito elevados — potencialmente milhares de dólares em chamadas de API. Limitar o número de iterações é uma das medidas que ajudam a evitar esse tipo de ameaça.

Essas não são as únicas ameaças possíveis. Como este é um curso introdutório, a lista apresenta algumas das principais, incluindo a injeção de *prompt* e o envenenamento de memória.

## 3. Defesa em profundidade

Agora que conhecemos o modelo de ameaças, vamos analisar a arquitetura de segurança em camadas necessária para agentes em produção. A seguir, veremos cada uma das cinco camadas.

### 3.1 Validação de entradas

Esta camada atua antes do LLM. A ideia é tratar todo conteúdo externo recuperado como dado não confiável, separá-lo das instruções e aplicar uma lista de permissões para ferramentas, além de verificar as permissões de acesso. Também é possível classificar o nível de risco da entrada — baixo, médio ou alto — e encaminhá-la de acordo com essa classificação.

Outra possibilidade é detectar e ocultar informações de identificação pessoal (*PII*, na sigla em inglês). Por exemplo, se alguém informar um número de Seguro Social, esse dado pode ser ocultado na entrada. Em resumo, esta camada atua antes do processamento pelo LLM e pode incluir sanitização e validação das entradas.

### 3.2 Mecanismos de proteção do LLM

Esta camada atua durante o processamento. É possível definir instruções explícitas de segurança e limites no *prompt* do sistema. Também é possível controlar o acesso às ferramentas, garantindo que o agente só chame aquelas para as quais tem autorização.

Além disso, o contexto pode ser gerenciado para que o conteúdo recuperado seja tratado como dado não confiável e para evitar que o limite da janela de contexto seja excedido.

### 3.3 Limites de execução das ferramentas

Esta é a camada em que as ações acontecem, durante a chamada às ferramentas. Cada ferramenta deve ter apenas as permissões mínimas necessárias. Também é possível validar os argumentos recebidos e isolar a execução de código em ambientes restritos, como contêineres ou máquinas virtuais.

Outra medida é manter uma pessoa no processo (*human in the loop*) para ações destrutivas ou irreversíveis, como excluir dados.

Assim, a validação de entradas ocorre antes do processamento pelo LLM; os mecanismos de proteção do LLM atuam durante o processamento; e os limites das ferramentas controlam a camada de ação.

### 3.4 Filtragem de saídas

Depois que o LLM produz uma resposta, esta camada atua após o processamento. Assim como na validação de entradas, as respostas podem ser verificadas quanto à presença de informações de identificação pessoal (*PII*).

Também é possível verificar se há dados confidenciais ou conteúdo prejudicial, avaliar se a resposta é relevante para a pergunta e evitar apresentá-la quando não for. Outras medidas incluem verificar a conformidade com as políticas de conteúdo e conferir citações e atribuições. Muitos dos recursos usados em sistemas RAG também são relevantes aqui.

### 3.5 Observabilidade e monitoramento

Esta camada funciona continuamente, acompanhando as quatro camadas anteriores. Ela inclui o registro das entradas, das etapas de raciocínio, das chamadas a ferramentas e das saídas — sempre com a ocultação de informações de identificação pessoal (*PII*).

Também pode incluir alertas em tempo real para comportamentos anômalos, padrões incomuns de uso de ferramentas ou picos de custo. O rastreamento permite observar cada etapa e analisar, por exemplo, o tempo de resposta. Auditorias regulares também fazem parte desse processo.

## 4. Princípios para aplicar as proteções

O principal ponto desta arquitetura é a defesa em profundidade: nenhuma camada, por si só, é suficiente. O objetivo é que uma camada identifique o que outra não conseguiu detectar. O mesmo princípio usado em segurança de redes também se aplica à segurança de agentes.

Outro aspecto importante é o roteamento baseado em risco. Nem todas as consultas precisam passar por todas as camadas. Consultas de baixo risco, como perguntas frequentes, podem usar mecanismos de proteção mais simples. Já consultas de alto risco, como aconselhamento financeiro ou alterações de dados, devem passar por validações completas e revisão humana.

## 5. Recapitulação

Nesta aula, analisamos exemplos de ataques reais e o modelo de ameaças para agentes de IA. As cinco categorias abordadas foram injeção de *prompt*, uso indevido de ferramentas, envenenamento de memória, exfiltração de dados e execução descontrolada.

Em seguida, vimos como reduzir esses riscos com validação e sanitização de entradas, mecanismos de proteção do LLM, limites para a execução de ferramentas, filtragem de saídas e uma camada contínua de observabilidade e monitoramento.

Espero que esta aula tenha sido útil. Obrigado pelo seu tempo!
