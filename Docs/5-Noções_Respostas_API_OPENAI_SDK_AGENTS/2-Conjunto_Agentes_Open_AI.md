# A Pilha de Agentes da OpenAI

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar a pilha de agentes da OpenAI e entender como seus principais componentes se relacionam: modelos, API de Respostas, SDK de Agentes e aplicação.

Também vamos recapitular o conceito de agente de IA e comparar duas formas de construir agentes: usar a API de Respostas diretamente, com mais controle sobre a orquestração, ou usar o SDK de Agentes, que oferece recursos de nível mais alto.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Recapitular os componentes e as propriedades de um agente de IA.
- Identificar as camadas da pilha de agentes da OpenAI.
- Explicar a relação entre os modelos, a API de Respostas e o SDK de Agentes.
- Escolher entre a API de Respostas e o SDK de Agentes de acordo com a complexidade do fluxo de trabalho.
- Comparar como cada opção lida com ferramentas, etapas, orquestração e falhas.

### Benefícios para você

Esta lição oferece um modelo prático para decidir como implementar um agente com as tecnologias da OpenAI. Ao entender o que cada camada oferece, você poderá escolher entre controlar diretamente o loop do agente ou aproveitar a estrutura e a automação do SDK de Agentes.

---

# Transcrição da aula

Bem-vindo(a)! Nesta lição, vamos analisar a pilha de agentes da OpenAI. Antes disso, vamos recapitular o que é um agente de IA, assunto que vimos no módulo 1.

## 1. O que é um agente de IA?

Um agente de IA pode ser entendido como a combinação de um modelo de linguagem de grande porte (LLM), ferramentas e um loop:

- O LLM é o cérebro, responsável por compreender e raciocinar.
- As ferramentas são como as mãos, permitindo que o agente aja no mundo real.
- O loop é como o sistema nervoso, mantendo o processo em andamento.

Os agentes também têm algumas propriedades importantes:

- São orientados a objetivos: trabalham em direção a uma meta.
- São autônomos: escolhem dinamicamente os próximos passos.
- Usam ferramentas: não se limitam a gerar texto.
- São iterativos: continuam refinando sua abordagem.

Essa recapitulação será útil para entendermos o agente sob a perspectiva da plataforma da OpenAI.

## 2. A pilha de agentes da OpenAI

A pilha de agentes da OpenAI é composta por camadas. Na base estão os modelos, que dão suporte ao restante do sistema. Entre as opções, há modelos de raciocínio, como o GPT-5, voltados a tarefas complexas, e modelos rápidos sem raciocínio, como o GPT-4.1, voltados a respostas rápidas.

> Até o momento desta gravação, o modelo mais recente da OpenAI é o GPT-5.5.

Acima dos modelos está a API de Respostas, a principal API da OpenAI para a criação de agentes. Ela é stateful, ou seja, armazena o histórico de conversas. Também oferece suporte a ferramentas integradas, como busca na web, busca em arquivos e interpretador de código, além de lidar com chamadas de função. Esses recursos serão explorados em lições subsequentes.

Acima da API de Respostas está o SDK de Agentes, um framework Python de nível mais alto que facilita:

- definir agentes;
- orquestrar fluxos de trabalho multiagentes;
- adicionar mecanismos de proteção;
- rastrear e depurar sistemas.

No topo da pilha está a aplicação, com sua lógica de negócios, interface do usuário e código personalizado.

Em resumo, os modelos dão suporte à API de Respostas, o SDK de Agentes utiliza essa API e a aplicação se apoia nessas camadas.

## 3. Como escolher entre a API de Respostas e o SDK de Agentes

Uma dúvida frequente é: devo usar a API de Respostas ou o SDK de Agentes? A resposta não é que um seja melhor que o outro: eles atendem a diferentes níveis de complexidade.

### Fluxo simples

Se você não precisa de uma lógica com várias etapas — por exemplo, se quer fazer uma pergunta, chamar uma ferramenta uma vez e receber uma resposta —, a API de Respostas tende a ser a opção mais simples e direta, oferecendo controle total.

### Fluxo com várias etapas

Se a aplicação exige várias etapas, avalie se também precisa de múltiplos agentes, mecanismos de proteção ou orquestração:

- Se não precisar desses recursos, ainda é possível usar a API de Respostas. Nesse caso, você terá de implementar boa parte da lógica por conta própria, incluindo o loop que gerencia o agente.
- Se precisar desses recursos, o SDK de Agentes pode ser a escolha mais adequada. Ele oferece estrutura, automação e funcionalidades integradas.

Uma analogia ajuda a visualizar a diferença: usar a API de Respostas é como construir um motor de carro do zero. Já o SDK de Agentes é como usar um carro que já vem com motor, direção e sistemas de segurança. Você continua decidindo para onde ir, mas não precisa construir tudo sozinho.

## 4. Exemplo: buscar e reservar um voo

Vamos retomar um exemplo do módulo 1. Imagine que o usuário pergunte: “Encontre o voo mais barato de Austin para Zurique e reserve-o.”

No ciclo ReAct, o agente realiza uma ação, chama a ferramenta de voos, observa o resultado, raciocina novamente e então responde. O exemplo pode começar com uma busca de voos e ser ampliado para incluir a reserva.

Com a API de Respostas, você chamaria as ferramentas de busca e de reserva, processaria os resultados, gerenciaria novas tentativas e trataria falhas. Em outras palavras, seria responsável por orquestrar o fluxo manualmente.

Com o SDK de Agentes, loops, lógica de múltiplas etapas, mecanismos de proteção e outros recursos já estão integrados. O agente pode planejar e executar etapas, chamar ferramentas, repetir o ciclo automaticamente e retornar o resultado final.

## 5. Recapitulando

Nesta lição, analisamos a pilha de agentes da OpenAI — modelos, API de Respostas e SDK de Agentes — e vimos que o SDK é construído sobre a API de Respostas.

Também percorremos um fluxo de decisão para escolher entre as duas opções. Com a API de Respostas, você constrói o loop e a camada de orquestração do agente. Com o SDK de Agentes, esse loop já está estruturado, o que simplifica a implementação de fluxos mais complexos.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!