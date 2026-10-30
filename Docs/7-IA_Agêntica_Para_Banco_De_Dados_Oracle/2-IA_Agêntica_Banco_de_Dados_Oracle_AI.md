# Ciclo de vida e ambiente de execução de agentes

## Considerações iniciais

### Visão geral

Nesta lição, vamos entender o que acontece depois que escrevemos a lógica de um agente. Vamos explorar a arquitetura de tempo de execução, os componentes necessários para disponibilizar agentes a usuários reais e o papel de serviços gerenciados, como o OCI Enterprise AI Agents Service.

---

# Transcrição da aula

## 1. Da lógica do agente à produção

Se você já escreveu um agente usando LangChain, o SDK de Agentes da OpenAI ou a API de Respostas, talvez tenha se perguntado o que acontece depois que o código está pronto.

Imagine que você seguiu um tutorial, escreveu algumas linhas de código e o agente respondeu corretamente a uma pergunta. Você compartilha uma captura de tela, e alguém pergunta: “Posso usar?”. Então percebe que o agente só funciona no seu laptop. Se você fechar a tampa, ele deixa de estar disponível. É nesse momento que surgem os desafios de produção.

Precisamos responder a perguntas como:

- Onde o agente será executado?
- Como ele poderá escalar?
- Como os usuários poderão acessá-lo?
- Onde ficará armazenada a memória?
- Como investigar uma falha ou reproduzir um problema?

Essas questões não são resolvidas apenas escrevendo uma lógica de agente melhor. Elas fazem parte da arquitetura de tempo de execução.

## 2. A lógica do agente e a arquitetura de tempo de execução

Pense na construção de um carro. Projetar um motor é uma conquista importante, mas um motor sozinho não leva ninguém a lugar algum. Para funcionar, o carro também precisa de combustível, sistema de arrefecimento, freios, direção, estradas e manutenção.

No agente, o motor corresponde à lógica que escrevemos usando, por exemplo, LangChain ou o SDK de Agentes da OpenAI. Essa lógica contém o raciocínio, os prompts e as chamadas de ferramentas.

A arquitetura de tempo de execução é tudo o que envolve essa lógica: onde o agente é executado, como as solicitações chegam até ele, como ele escala e como observamos seu comportamento. A inteligência do agente sem essa arquitetura é como um motor fora do carro: existe, mas não consegue atender usuários no mundo real.

## 3. As camadas de um sistema de agentes

Sistemas de agentes, desde demonstrações até aplicações empresariais, podem ser entendidos em três camadas:

1. **Usuário ou aplicação:** é a forma como uma pessoa ou outro serviço acessa o agente, por exemplo, por uma interface web, um aplicativo móvel ou uma API.
2. **Arquitetura de tempo de execução:** conecta a aplicação à lógica do agente e oferece os recursos necessários para operar.
3. **Lógica do agente:** é o código que implementamos com frameworks e SDKs, responsável pelo raciocínio e pelo uso de ferramentas.

Uma solicitação entra pela camada de usuário ou aplicação, passa pelos componentes de tempo de execução até chegar à lógica do agente e, em seguida, a resposta retorna pelo fluxo.

Ao usar apenas LangChain ou um SDK de agente, construímos principalmente a lógica do agente. Sem um serviço gerenciado, os componentes intermediários da arquitetura continuam sendo responsabilidade de quem desenvolve e opera o sistema.

## 4. Componentes da arquitetura de tempo de execução

A arquitetura de tempo de execução é formada por componentes que exigem código e infraestrutura próprios:

1. **Tratamento de solicitações:** recebe requisições, autentica usuários, limita o tráfego e direciona cada solicitação ao agente correto.
2. **Ambiente de execução:** fornece o processo e a infraestrutura onde o código do agente é executado, como uma máquina virtual, um cluster Kubernetes ou uma função sem servidor.
3. **Orquestração e estado:** coordena execuções com várias etapas, chamadas de ferramentas, novas tentativas e o armazenamento da memória entre solicitações.
4. **Sandbox de ferramentas:** aplica limites e permissões, como limites de CPU e tempo, para proteger o sistema quando o agente executa código ou acessa recursos externos.
5. **Camada de integração:** conecta o agente a bancos de dados, CRMs e sistemas de tickets, gerenciando credenciais, pools de conexão e controle de acesso.
6. **Escalabilidade e confiabilidade:** lida com variações no tráfego e falhas de servidores para manter o serviço disponível.
7. **Observabilidade:** oferece logs, rastreamentos e métricas para investigar o comportamento do agente e reproduzir problemas.

Esses componentes representam trabalho real de engenharia e operação. Eles não são fornecidos automaticamente por uma instalação simples de um framework como o LangChain.

## 5. Construir a infraestrutura ou usar um ambiente gerenciado

Há duas abordagens: criar e manter os componentes por conta própria ou usar um ambiente de execução gerenciado. Ambas podem resultar em um agente funcional, mas o esforço operacional é diferente.

Ao integrar um framework ou SDK diretamente à própria infraestrutura, a equipe é responsável pelos componentes da arquitetura de tempo de execução. Em produção, cada componente pode exigir trabalho significativo de engenharia e suporte contínuo.

Com um ambiente gerenciado, como o OCI Enterprise AI Agents Service, grande parte dessa infraestrutura já está disponível. A equipe fornece a lógica do agente e as chamadas de API, enquanto o serviço gerencia aspectos como o ambiente de execução, o tratamento de solicitações, o estado, o sandbox de ferramentas e a escalabilidade.

Para muitas equipes, especialmente aquelas que estão começando a levar agentes à produção, um serviço gerenciado pode reduzir o tempo e o trabalho necessários. A lógica do agente continua sendo escrita pela equipe; o que muda é que a infraestrutura de execução deixa de ser uma responsabilidade implementada do zero.

## 6. Recapitulando os pontos principais

- Frameworks de agentes fornecem os recursos para implementar a lógica e a inteligência do agente.
- A arquitetura de tempo de execução envolve essa lógica e permite que ela opere no mundo real.
- Um sistema de agentes inclui uma camada de usuário ou aplicação, uma camada de tempo de execução e a lógica do agente.
- A arquitetura de tempo de execução abrange tratamento de solicitações, execução, orquestração e estado, sandbox, integração, escalabilidade, confiabilidade e observabilidade.
- Um ambiente gerenciado oferece esses recursos sem exigir que a equipe construa cada componente do zero.

## Conclusão

Nesta lição, vimos que a lógica do agente é apenas uma parte de uma solução de produção. A arquitetura de tempo de execução é o sistema que a envolve e fornece os recursos para disponibilizar, operar e observar o agente.

O uso de um ambiente gerenciado, como o OCI Enterprise AI Agents Service, permite concentrar o trabalho na lógica do agente sem precisar construir todas as camadas de infraestrutura do zero.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
