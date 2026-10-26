# Aula 04 — Construindo seu primeiro agente de IA

## Considerações iniciais

### Visão geral da aula

Nesta aula, você vai conhecer frameworks para desenvolvimento de agentes e acompanhar a construção de um agente simples com ferramentas matemáticas. O exemplo apresenta as etapas fundamentais: escolher um modelo de linguagem, definir ferramentas, criar o agente e invocá-lo para resolver tarefas de complexidade crescente.

### Objetivos de aprendizagem

Ao concluir esta aula, você será capaz de:

- Comparar os principais frameworks para construção de agentes.
- Explicar como funções são registradas como ferramentas.
- Entender o papel de descrições, *docstrings* e dicas de tipo (*type hints*).
- Criar e invocar um agente que usa ferramentas.
- Descrever como o agente escolhe e encadeia ferramentas em um loop *ReAct*.

### Recurso complementar

Para aprofundar o conteúdo, consulte a documentação oficial dos frameworks mencionados na aula: LangChain, LangGraph, OpenAI Agents SDK, CrewAI e Hugging Face SmolAgents.

### Benefícios para você

Ao acompanhar a construção do agente, você verá como conceitos de modelos, ferramentas e loops de raciocínio se conectam em uma implementação prática. O exemplo também ajuda a entender como um agente pode selecionar ferramentas e combinar resultados sem depender de uma sequência fixa programada para cada pergunta.

---

# Transcrição da aula

Bem-vindos de volta! Nesta aula, vamos construir nosso primeiro agente de IA. Para começar, vamos conhecer alguns frameworks usados no desenvolvimento de agentes.

## 1. Frameworks para agentes de IA

O ecossistema de frameworks para agentes está evoluindo rapidamente. Nesta aula, vamos nos concentrar em LangChain, LangGraph e OpenAI Agents SDK.

### LangChain e LangGraph

O LangChain é amplamente adotado e oferece recursos para encadear chamadas a LLMs, além de um ecossistema extenso de integrações e documentação. Suas abstrações podem, porém, adicionar complexidade a tarefas simples.

O LangGraph amplia esse conjunto com fluxos de trabalho baseados em grafos e com estado. LangChain e LangGraph podem ser boas opções para equipes que precisam de orquestração, gerenciamento de estado, *middleware*, testes e integrações em produção.

### OpenAI Agents SDK

O OpenAI Agents SDK oferece uma abordagem estruturada para criar agentes, com integração à Responses API e orquestração nativa de ferramentas. Entre seus pontos fortes estão a integração com modelos da OpenAI, a observabilidade e os mecanismos de proteção (*guardrails*), além de exigir menos código de suporte do que montar todos esses recursos manualmente.

Por outro lado, seu design é mais opinativo e pode ser menos flexível do que o LangGraph para orquestrações altamente personalizadas. Seu ecossistema também continua evoluindo.

### Outros frameworks

Esta aula não abordará CrewAI nem Hugging Face SmolAgents. O CrewAI é conhecido por fluxos de trabalho que representam equipes; o SmolAgents é uma alternativa compacta, adequada a contextos de aprendizado e educação.

### Orientação prática

Para aprender, comece com um exemplo simples que ajude a compreender os componentes internos. Em produção, LangChain, LangGraph e OpenAI Agents SDK oferecem flexibilidade e suporte de ecossistema. Frameworks tendem a ser especialmente úteis conforme a complexidade do sistema aumenta.

## 2. Etapas para construir o agente

O exemplo desta aula começa com um agente pequeno, mas inspirado em situações do mundo real. A construção segue quatro etapas:

1. Escolher o modelo que funcionará como o cérebro do agente.
2. Definir as ferramentas que ele poderá usar.
3. Criar o agente com o modelo e as ferramentas.
4. Invocar o agente com perguntas e analisar os resultados.

## 3. Escolha do modelo e definição das ferramentas

### Escolher o modelo

O primeiro passo é selecionar o LLM. O exemplo apresentado usa um modelo da OpenAI por meio do LangChain, mas é possível escolher outro modelo compatível, inclusive de outro provedor.

### Definir as ferramentas

Ferramentas representam ações que o agente pode executar. Para manter o exemplo simples, são definidas quatro funções matemáticas:

- adição;
- multiplicação;
- divisão;
- raiz quadrada.

Em aplicações reais, uma ferramenta poderia chamar uma API ou consultar um banco de dados, inclusive por meio de MCP.

### Registrar funções como ferramentas

No exemplo em Python, um decorador de ferramenta registra cada função para que o agente possa descobri-la e chamá-la. Outros elementos também ajudam o LLM a usar as ferramentas corretamente:

- **Dicas de tipo (*type hints*):** indicam os tipos dos parâmetros de entrada e do valor retornado. Por exemplo, dois parâmetros do tipo `float` e um retorno do tipo `float`.
- **Docstring:** descreve o que a função faz e orienta o LLM sobre quando utilizá-la. Quanto mais clara for a descrição, mais precisa tende a ser a seleção da ferramenta.
- **Esquema JSON:** o framework converte a definição da função em um esquema estruturado, enviado ao LLM junto com a mensagem do usuário.

O LLM não recebe o código Python da função. Ele recebe a descrição estruturada da ferramenta. Por isso, nomes, descrições, *docstrings* e tipos funcionam também como instruções para o modelo, não apenas como documentação para quem lê o código.

## 4. Como o agente seleciona uma ferramenta

O agente usa as descrições das ferramentas para decidir qual delas atende à solicitação. Se o usuário pedir uma adição, por exemplo, o LLM pode identificar a ferramenta de adição pelo nome e pela descrição, preencher os parâmetros e solicitar sua execução.

Por isso, é importante definir corretamente os nomes, as descrições, os tipos de entrada e os tipos de retorno das ferramentas.

## 5. Criação e invocação do agente

Depois de definir as ferramentas, o próximo passo é criar o agente. No exemplo, isso é feito com uma chamada à função `create_agent`, fornecendo o modelo e as ferramentas definidas anteriormente.

O framework configura o loop *ReAct* nos bastidores: o agente raciocina sobre a tarefa, escolhe uma ferramenta, observa o resultado e decide se precisa continuar ou se já pode responder.

Para executar o agente, usa-se a função `invoke`, passando a pergunta do usuário. A aula apresenta três exemplos, em ordem crescente de complexidade.

## 6. Exemplos de execução

### Exemplo 1: adição

Para responder a `42 + 58`, o agente precisa de apenas uma chamada à ferramenta de adição:

1. O agente identifica que a pergunta exige uma adição.
2. Seleciona a ferramenta correspondente e fornece os valores.
3. Recebe o resultado e conclui que não precisa chamar outra ferramenta.
4. Responde ao usuário.

### Exemplo 2: multiplicação seguida de divisão

Na expressão `15 × 8 ÷ 3`, o agente precisa encadear duas ferramentas:

1. Primeiro, chama a ferramenta de multiplicação com `15` e `8`, obtendo `120`.
2. Usa o resultado da primeira chamada como entrada da ferramenta de divisão, junto com `3`.
3. Obtém `40` e responde ao usuário.

O agente determina essa ordem a partir da solicitação; ela não foi programada como uma sequência fixa específica para essa pergunta.

### Exemplo 3: área de um retângulo e raiz quadrada

No último exemplo, o usuário informa as dimensões de um retângulo e pede a raiz quadrada de sua área. O agente precisa decompor a tarefa:

1. Calcula a área multiplicando largura por altura.
2. Usa o resultado como entrada da ferramenta de raiz quadrada.
3. Observa o resultado e responde ao usuário.

Assim como no exemplo anterior, a sequência não foi definida previamente como um fluxo fixo. O agente interpreta a solicitação, seleciona as ferramentas e encadeia os resultados para concluir a tarefa.

## 7. Conclusão

Este exemplo mostra que é possível construir um agente simples em poucas etapas: escolher um modelo, definir ferramentas, criar o agente e invocá-lo. Mesmo nesse exemplo reduzido, o framework configura um loop de raciocínio e ação que permite ao agente selecionar ferramentas e combinar resultados.

Em cenários reais, agentes podem exigir mais ferramentas, integrações e mecanismos de proteção. Ainda assim, entender este exemplo básico ajuda a compreender como os componentes fundamentais se conectam e por que agentes podem resolver tarefas sem depender de uma sequência fixa definida para cada caso.
