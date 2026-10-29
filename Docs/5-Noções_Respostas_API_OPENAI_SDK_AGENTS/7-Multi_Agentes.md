# Sistemas multiagentes

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar sistemas multiagentes com transferência de tarefas. Quando uma solicitação é complexa ou envolve diferentes especialidades, vários agentes podem colaborar usando dois padrões: transferências (*handoffs*) e gerenciador (*manager*).

Também vamos acompanhar a configuração de um fluxo com transferências, no qual um agente de triagem encaminha a solicitação para o especialista adequado.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Diferenciar os padrões de transferência (*handoffs*) e gerenciador (*manager*).
- Entender os papéis dos agentes de triagem e dos agentes especialistas.
- Descrever como configurar transferências entre agentes.
- Escolher um padrão de coordenação adequado para diferentes situações.

### Benefícios para você

Sistemas multiagentes permitem dividir tarefas entre agentes especializados. Ao entender os padrões de coordenação, você poderá decidir quando encaminhar uma conversa para um especialista e quando manter um agente central responsável por organizar o trabalho e apresentar a resposta final.

---

# Transcrição da aula

Bem-vindos a esta lição sobre sistemas multiagentes com transferência de tarefas. Quando uma tarefa é muito complexa para um único agente, você pode usar vários agentes no contexto do SDK de Agentes da OpenAI. Existem dois padrões principais.

## 1. Padrões de coordenação

### Transferências (*handoffs*)

O padrão de transferências, também conhecido como modelo descentralizado, começa com um agente de triagem. Ele recebe a pergunta do usuário, decide qual especialista deve lidar com ela e transfere a conversa. Depois da transferência, o especialista assume o atendimento e recebe o histórico da conversa.

Um exemplo é um sistema de suporte ao cliente que encaminha perguntas para agentes especializados em faturamento, envio ou suporte técnico.

### Gerenciador (*manager*)

No padrão de gerenciador, também conhecido como modelo centralizado, um agente central mantém o controle. Ele aciona agentes especializados — disponibilizados como ferramentas — e reúne os resultados em uma resposta unificada. O usuário interage apenas com o gerenciador.

Por exemplo, um agente gerente de projeto pode delegar tarefas a um pesquisador, um redator e um revisor, e depois sintetizar o trabalho.

### Qual padrão escolher?

Use transferências para encaminhar solicitações diretamente a um especialista, especialmente quando o roteamento é simples. Prefira o padrão de gerenciador quando um agente precisar coordenar vários especialistas e combinar seus resultados.

## 2. Configurando um fluxo com transferências

Nesta aula, vamos analisar o padrão de transferências por meio de um exemplo com agentes de Matemática e de História.

### Definindo os agentes especialistas

Primeiro, são definidos os agentes especialistas. Neste exemplo, há um Tutor de Matemática e um agente de História. Cada um tem instruções próprias, que orientam seu comportamento, e uma descrição de transferência, que informa ao agente de triagem em quais situações deve encaminhar uma pergunta para aquele especialista.

### Definindo o agente de triagem

Depois, é criado o agente de triagem. Sua instrução é encaminhar cada pergunta ao especialista adequado. As transferências disponíveis são configuradas com os agentes de Matemática e de História; em um sistema real, a lista pode incluir mais especialistas. Também é especificado o modelo que o agente utilizará.

Cada transferência fica disponível ao agente de triagem como uma ferramenta. Assim, ele pode selecionar o especialista apropriado com base na solicitação do usuário.

### Executando o fluxo

O fluxo pode ser resumido assim:

1. Definir os agentes especialistas e suas instruções.
2. Descrever quando cada especialista deve receber uma transferência.
3. Criar o agente de triagem e configurar as transferências disponíveis.
4. Enviar a pergunta do usuário ao agente de triagem.
5. Encaminhar a conversa ao especialista adequado, que responde à solicitação.

Por exemplo, se o usuário perguntar “quanto é 15% de 240?”, o agente de triagem identifica que é uma questão de Matemática e encaminha a conversa ao Tutor de Matemática, que responde “36”. Se a pergunta for sobre a Grande Muralha da China, a conversa é encaminhada ao agente de História.

## 3. Recapitulando

Nesta lição, vimos dois padrões para coordenar sistemas multiagentes: transferências (*handoffs*), em que um especialista assume a conversa, e gerenciador (*manager*), em que um agente central coordena especialistas e sintetiza os resultados.

Também acompanhamos a configuração de um fluxo de transferências com um agente de triagem e especialistas em Matemática e História. Como modelo mental, comece com transferências para um roteamento mais simples e use o padrão de gerenciador quando precisar coordenar vários especialistas.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
