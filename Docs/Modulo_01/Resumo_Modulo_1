# Resumo do Módulo 1 — Fundamentos dos agentes de IA

## Considerações iniciais

### Visão geral

Neste resumo, vamos retomar os principais conceitos do primeiro módulo: o que são agentes de IA baseados em LLMs, como modelos, ferramentas e orquestração trabalham em conjunto, quais são os principais padrões de raciocínio, como construir um agente simples e como protegê-lo.

### Objetivos de aprendizagem

Ao concluir esta revisão, você será capaz de:

- Descrever os componentes fundamentais de um agente de IA baseado em LLM.
- Explicar como modelos, ferramentas e a camada de orquestração se complementam.
- Reconhecer o padrão *ReAct* e seu papel no uso de ferramentas.
- Resumir como um agente pode planejar e executar tarefas em várias etapas.
- Identificar as camadas de uma arquitetura de segurança em profundidade.

### Benefícios para você

Esta recapitulação conecta os conceitos abordados ao longo do módulo e reforça como eles se aplicam à construção de agentes. Ela também prepara você para aprofundar, no próximo módulo, o funcionamento interno dos frameworks e dos loops de agentes.

---

# Transcrição do resumo

Parabéns por concluir o primeiro módulo! Vamos relembrar alguns dos assuntos que estudamos.

## 1. O que é um agente de IA

Na IA clássica, um agente é qualquer sistema que percebe um ambiente e age nele. Neste módulo e neste curso, o foco está nos agentes baseados em LLMs. O modelo mental que quero que você leve é: um agente de IA baseado em LLM é a combinação de um LLM, ferramentas e um loop.

Como vimos na primeira aula, podemos entender esses componentes por meio de uma analogia: o LLM é o cérebro, que compreende e raciocina; as ferramentas são como as mãos, que permitem agir no mundo real; e o loop é o sistema nervoso, que mantém o processo em andamento.

Também vimos que o LLM é o mecanismo de raciocínio do agente, mas escolher o modelo certo exige mais do que selecionar aquele com a maior pontuação em um benchmark.

## 2. Modelos, ferramentas e orquestração

A escolha do LLM envolve equilibrar capacidade, custo e latência.

As ferramentas transformam um LLM — que, sem elas, seria apenas um gerador de texto — em um agente capaz de consultar informações e executar ações.

Por fim, estudamos a camada de orquestração, também chamada de loop. É nela que tudo se conecta: o loop executa o ciclo de raciocínio, acompanha o estado, gerencia a memória, direciona as chamadas às ferramentas e aplica regras de segurança.

Pense nessa camada como o sistema operacional do agente. Ela decide se o agente deve continuar, parar, tentar novamente ou encaminhar a tarefa para outra etapa. É nela que está boa parte da complexidade real de engenharia.

## 3. O padrão ReAct

Na aula 3, estudamos o padrão *ReAct* (*Reasoning and Acting*, ou raciocinar e agir), um dos padrões mais importantes para o projeto de agentes. Ele resolve uma limitação fundamental do padrão *Chain of Thought*: este permite que os modelos raciocinem, mas não lhes dá acesso ao mundo real.

O uso de ferramentas, por outro lado, permite que o modelo execute ações, mas não determina como ou quando deve usá-las. O *ReAct* intercala raciocínio e ação. Por isso, este é um dos princípios e padrões de projeto de agentes mais importantes a serem lembrados.

## 4. Construção de um agente simples

Na aula 4, construímos um agente simples e vimos como criá-lo e invocá-lo. Usamos uma única função chamada `create_agent`, fornecemos um modelo e várias ferramentas e, em seguida, invocamos o agente com `agent.invoke`. Foram apenas duas linhas de código para a criação e a chamada do agente. Também analisamos três exemplos:

1. **Uma adição matemática simples:** o agente resolveu o problema em um único loop.
2. **Um teste com várias etapas:** o agente realizou uma multiplicação e depois uma divisão, encadeando os resultados em dois loops.
3. **Um teste mais complexo:** pedimos ao agente que calculasse a raiz quadrada da área de um retângulo.

No terceiro exemplo, o agente planejou a própria estratégia: primeiro calculou a área e depois extraiu a raiz quadrada. Ele interpretou a pergunta, dividiu a tarefa em etapas, escolheu as ferramentas adequadas e passou o resultado de cada etapa para a seguinte, sem que essa sequência precisasse ser definida previamente.

Em outras palavras, o agente avaliou dinamicamente o que fazer em seguida. Essa capacidade é uma das características que definem um agente.

Por trás daquelas duas linhas de código, o LangChain executa muitas operações que não vemos diretamente. Por isso, frameworks como o LangChain são importantes para quem está começando. Porém, à medida que os agentes se tornam mais complexos, entender esses mecanismos internos se torna essencial — por exemplo, para depurar o sistema ou criar loops personalizados.

Vamos estudar esses detalhes no módulo 2. Nesta aula, construímos um agente e analisamos três testes simples.

## 5. Segurança de agentes

Por fim, estudamos segurança. Os agentes são mais poderosos do que os chatbots e, por isso, podem ser mais perigosos quando algo dá errado. Eles precisam de uma arquitetura de segurança em camadas, baseada no princípio de defesa em profundidade.

As cinco camadas que vimos foram:

1. Validação de entradas.
2. Mecanismos de proteção do LLM.
3. Limites de execução das ferramentas.
4. Filtragem de saídas.
5. Observabilidade e monitoramento.

## 6. Encerramento

Este módulo abordou muitos conceitos. Parabéns novamente por concluí-lo e obrigado pelo seu empenho nos estudos!
