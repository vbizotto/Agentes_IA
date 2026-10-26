# Introdução ao LangChain

## Considerações iniciais

### Visão geral

Nesta lição, vamos conhecer o LangChain, um framework de código aberto para a construção de aplicações baseadas em grandes modelos de linguagem (LLMs). Vamos explorar seus principais recursos, conhecer o ecossistema e estudar três componentes fundamentais: modelos, modelos de prompt e *chains*.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Explicar como o LangChain conecta modelos a sistemas externos e organiza fluxos de trabalho.
- Reconhecer os principais elementos do ecossistema LangChain.
- Descrever o papel dos modelos, dos modelos de prompt e das *chains*.
- Entender como o LCEL conecta etapas de processamento e como uma chamada a `chain.invoke` é executada.

### Benefícios para você

Compreender esses blocos de construção ajuda a ir além de chamadas isoladas a um LLM e a criar aplicações com etapas reutilizáveis. Esses conceitos também preparam você para construir agentes com o LangChain nas próximas lições.

---

# Transcrição da aula

Boas-vindas a esta introdução ao LangChain!

## 1. O que é o LangChain

O LangChain é um framework de código aberto para a construção de aplicações baseadas em grandes modelos de linguagem. Um LLM, por si só, pode gerar textos, responder a perguntas e raciocinar sobre problemas, mas não consegue, por conta própria, chamar APIs, acessar bancos de dados ou executar código.

O LangChain conecta o modelo ao mundo externo. Assim, em vez de apenas gerar texto, uma aplicação pode também executar ações. Seus recursos podem ser agrupados em três áreas:

1. **Conexão:** vincula o modelo a sistemas externos, como APIs, ferramentas e bancos de dados.
2. **Orquestração:** combina várias etapas em fluxos de trabalho, permitindo criar processos com mais de uma etapa.
3. **Construção:** oferece componentes para desenvolver aplicações completas, como agentes, chatbots e sistemas de recuperação de informações.

A principal ideia é que o LangChain não se limita a chamar um modelo: ele ajuda a construir sistemas ao redor dele.

## 2. O ecossistema LangChain

O ecossistema LangChain tem quatro partes principais:

1. **LangChain:** biblioteca central com componentes como cadeias, prompts, ferramentas e memória.
2. **LangGraph:** mecanismo recomendado para criar agentes de produção. Ele representa o comportamento do agente como um grafo de nós e arestas, oferecendo controle sobre loops, ramificações e estado.
3. **LangSmith:** camada de observabilidade que rastreia chamadas a LLMs, invocações de ferramentas e uso de tokens, ajudando a depurar e otimizar aplicações.
4. **Integrações:** conectores para diferentes provedores de LLMs, bancos de dados vetoriais, APIs de busca e outros serviços.

Não é necessário usar todos esses recursos para começar. Neste curso, vamos nos concentrar no framework LangChain; LangGraph, LangSmith e algumas integrações avançadas estão fora do escopo.

## 3. Modelos

O modelo é o mecanismo de raciocínio da aplicação. O LangChain oferece uma interface unificada para trabalhar com diferentes provedores, como OpenAI, Anthropic, Google e modelos de código aberto. Isso permite trocar de modelo com poucas alterações no código.

Ainda assim, modelos diferentes têm capacidades e comportamentos distintos. Alguns são melhores no uso de ferramentas, outros oferecem janelas de contexto maiores ou se comportam de maneira diferente durante o raciocínio. Portanto, uma interface unificada não significa que todos os modelos terão o mesmo desempenho ou comportamento.

Como os modelos disponíveis e suportados mudam com o tempo, consulte a documentação do LangChain para verificar as opções atuais.

## 4. Modelos de prompt

Os modelos de prompt permitem interagir com o modelo de maneira estruturada e reutilizável. Em vez de escrever uma string fixa a cada chamada, você cria um modelo com espaços reservados — por exemplo, para um tópico — e preenche esses valores dinamicamente.

Podemos pensar neles como funções: fornecemos entradas e recebemos prompts formatados. Isso torna a aplicação mais dinâmica e reutilizável.

Há três tipos principais:

1. **Modelo de prompt padrão:** indicado para tarefas simples.
2. **Modelo de prompt de chat:** usado com modelos conversacionais, permite definir mensagens com diferentes papéis:
   - **Sistema:** define o comportamento, o tom e as instruções gerais do modelo.
   - **Humano:** representa a entrada ou as instruções do usuário.
   - **IA:** representa as respostas anteriores do modelo.
3. **Prompt *few-shot* (com poucos exemplos):** inclui exemplos de entradas e saídas para orientar o modelo.

O principal benefício é transformar prompts em componentes reutilizáveis.

## 5. *Chains* e LCEL

As *chains* (cadeias) são sequências de etapas de processamento. Os dados passam de uma etapa para a seguinte. Uma cadeia simples pode conectar um modelo de prompt a um LLM e, depois, a um analisador de saída.

O LangChain usa o operador pipe (`|`) para conectar essas etapas. Essa forma de composição é chamada LCEL (*LangChain Expression Language*). Cada componente transforma os dados e os encaminha para o próximo.

Por exemplo, uma cadeia pode combinar um prompt, um modelo e um analisador de saída de texto. O analisador extrai o texto da resposta do modelo, produzindo uma string simples.

## 6. O que acontece em `chain.invoke`

Considere uma cadeia que recebe um tópico e pede ao modelo que o explique. Quando chamamos `chain.invoke`, o LangChain:

1. Preenche o modelo de prompt com o valor fornecido — por exemplo, “agentes de IA”.
2. Envia o prompt formatado ao LLM.
3. Recebe a resposta do modelo.
4. Usa o analisador de saída para converter a resposta em uma string simples.

O conteúdo da resposta pode variar conforme o modelo escolhido. Com esse fluxo, porém, não estamos apenas chamando um modelo: estamos compondo componentes reutilizáveis.

## 7. Encerramento

Nesta lição, apresentamos o LangChain e seus principais blocos de construção: o modelo, que fornece o mecanismo de raciocínio; o prompt, que orienta o modelo; e a *chain*, que encaminha os dados por uma sequência de etapas.

Ao conectar esses componentes, o LangChain ajuda a criar aplicações mais completas e reutilizáveis. Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
