# Necessidade de ciclo de vida e ambiente de execução

## Considerações iniciais

### Visão geral

Nesta lição, vamos entender o que acontece depois que a lógica de um agente é escrita. Frameworks como LangChain, o SDK de Agentes da OpenAI e a API de Respostas ajudam a construir essa lógica, mas não resolvem, por si só, todos os requisitos para disponibilizar um agente a usuários reais.

Vamos explorar o conceito de arquitetura de ambiente de execução, seus principais componentes e a diferença entre montar essa infraestrutura por conta própria e usar um serviço gerenciado, como o OCI Enterprise AI Agents Service.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Diferenciar a lógica do agente da arquitetura de ambiente de execução.
- Identificar as camadas de uma aplicação com agentes.
- Reconhecer os principais componentes necessários para executar um agente em produção.
- Comparar uma infraestrutura autogerenciada com um ambiente de execução gerenciado.

### Benefícios para você

Entender o ambiente de execução ajuda a planejar como disponibilizar um agente além do computador de desenvolvimento: atendendo solicitações, mantendo estado, acessando sistemas externos, lidando com falhas e permitindo a observabilidade do sistema.

---

# Transcrição da aula

Bem-vindos a esta lição sobre o ciclo de vida e o ambiente de execução de agentes. Se você já escreveu código de agente usando LangChain, o SDK de Agentes da OpenAI ou a API de Respostas, talvez se pergunte o que acontece depois. Nesta aula, vamos esclarecer o papel da arquitetura de ambiente de execução e por que ela é importante para levar um agente ao uso real.

## 1. Da lógica do agente à produção

Imagine que você criou um agente seguindo um tutorial. Ele funciona no seu computador, mas isso não significa que outras pessoas já possam acessá-lo como um serviço. Ainda é necessário responder a perguntas como:

- Onde o agente será executado?
- Como ele atenderá aos usuários e escalará com o aumento da demanda?
- Onde serão armazenados o estado e a memória da conversa?
- Como o sistema lidará com falhas e permitirá investigar problemas?

Essas questões tratam da arquitetura de ambiente de execução, não apenas da escrita de uma lógica de agente melhor.

Uma analogia é a construção de um carro: projetar um motor é essencial, mas o motor sozinho não permite que o carro circule. Também são necessários outros sistemas e uma infraestrutura que o apoiem. Da mesma forma, a lógica do agente precisa de um ambiente que permita executá-la e conectá-la aos usuários e aos serviços necessários.

## 2. As três camadas de um sistema de agentes

Um sistema de agentes pode ser entendido por meio de três camadas:

1. **Usuário ou aplicação:** é a interface pela qual uma pessoa ou outro serviço acessa o agente, como um site, um aplicativo móvel ou uma API.
2. **Arquitetura de ambiente de execução:** recebe e encaminha solicitações, coordena a execução e oferece serviços de suporte ao agente.
3. **Lógica do agente:** é o código desenvolvido com um framework ou SDK, incluindo instruções, raciocínio e chamadas de ferramentas.

Ao escrever somente a lógica com um framework, você ainda precisa decidir como fornecer as outras camadas ou escolher um serviço que ofereça parte dessa infraestrutura de forma gerenciada.

## 3. Componentes do ambiente de execução

O ambiente de execução pode incluir vários componentes. A aula destaca:

1. **Tratamento de solicitações:** recebe requisições, pode autenticar usuários, limitar o uso e encaminhar cada solicitação ao agente apropriado.
2. **Ambiente de execução:** fornece os recursos computacionais necessários para executar o código, por exemplo, em uma máquina virtual, um cluster Kubernetes ou uma função sem servidor.
3. **Orquestração e estado:** coordena etapas, chamadas de ferramentas, retomadas após falhas e armazenamento do estado da conversa entre solicitações.
4. **Sandbox de ferramentas:** aplica limites e permissões ao executar ferramentas, como limites de CPU e de tempo.
5. **Camada de integração:** conecta o agente a bancos de dados, CRMs e sistemas de chamados, considerando credenciais e controle de acesso.
6. **Escalabilidade e confiabilidade:** ajuda o sistema a lidar com variações de tráfego e falhas de componentes.
7. **Observabilidade:** reúne logs, rastreamentos e métricas para investigar a execução e diagnosticar problemas.

Esses componentes representam responsabilidades de software e infraestrutura que precisam ser consideradas ao preparar um agente para produção.

## 4. Infraestrutura própria ou serviço gerenciado

Uma opção é montar e operar a infraestrutura por conta própria. Nesse caso, a equipe é responsável pelos componentes necessários, pelas atualizações e pela manutenção contínua.

Outra opção é usar um ambiente de execução gerenciado, como o serviço de agentes de IA empresarial da OCI apresentado neste curso. O serviço fornece recursos de execução e orquestração gerenciados, reduzindo a quantidade de infraestrutura que a equipe precisa implementar e manter. A lógica do agente continua sendo desenvolvida pela equipe, e os recursos disponíveis dependem do serviço e de sua configuração.

Um serviço gerenciado pode reduzir o trabalho operacional, mas não elimina a necessidade de projetar, configurar e acompanhar a aplicação.

## 5. Recapitulando

Nesta lição, vimos que frameworks e SDKs ajudam a construir a lógica do agente, enquanto a arquitetura de ambiente de execução dá suporte à sua operação no mundo real.

Também conhecemos as três camadas de um sistema de agentes — usuário ou aplicação, ambiente de execução e lógica do agente — e os componentes que podem fazer parte do ambiente: tratamento de solicitações, computação, orquestração e estado, sandbox, integrações, escalabilidade, confiabilidade e observabilidade.

Por fim, comparamos a operação de uma infraestrutura própria com o uso de um serviço gerenciado. A escolha depende das necessidades, dos recursos e das responsabilidades operacionais de cada projeto.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
