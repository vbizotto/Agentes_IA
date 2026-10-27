# Construindo o Primeiro Agente com LangChain

## Considerações iniciais

### Visão geral

Nesta lição, vamos revisar e consolidar os conceitos essenciais para construir o primeiro agente com LangChain. Já vimos alguns desses blocos no módulo anterior; portanto, o foco aqui é reforçar a mentalidade de agente: como ele decide usar ferramentas, como o modelo participa do processo e como tudo se conecta para formar um comportamento funcional e reutilizável.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Explicar a diferença entre uma chamada simples a um LLM e um agente.
- Reconhecer como as ferramentas transformam um modelo em um sistema capaz de executar ações.
- Entender a anatomia de uma ferramenta no LangChain, incluindo decorador, dicas de tipo, docstring e retorno.
- Compreender o padrão ReAct e como ele orienta o ciclo de raciocínio e ação.
- Construir um agente simples com LangChain usando um modelo e ferramentas básicas.

### Benefícios para você

Compreender esses fundamentos ajuda a criar agentes mais confiáveis e consistentes. Em vez de apenas emitir texto, você passa a escrever sistemas que podem consultar fontes, inspecionar resultados, escolher ferramentas e iterar até encontrar uma resposta adequada.

---

# Transcrição da aula

Boas-vindas de volta! Nesta lição, construiremos nosso primeiro agente usando LangChain. Vocês já viram esse código no módulo anterior, então vamos passar por ele de forma rápida e focada. Algumas partes serão familiares, e vamos revisar os conceitos mais importantes sem perder o contexto.

## 1. O que define um agente

A diferença fundamental entre um LLM simples e um agente está no comportamento do sistema. Uma chamada básica ao modelo recebe uma entrada, gera texto e encerra. Não há uso de ferramentas, raciocínio dinâmico nem memória persistente.

Um agente é diferente. Ele usa o modelo como mecanismo de raciocínio capaz de decidir, em tempo real, o que fazer em seguida. O agente pode acionar ferramentas, inspecionar resultados, decidir se precisa de informações adicionais e iterar até chegar a uma resposta satisfatória. Isso foi visto no módulo anterior, quando discutimos o papel do LLM como parte de um sistema mais amplo.

A definição mais comum é a de um agente como um sistema no qual o modelo define o fluxo de controle da aplicação. Em vez de você, como desenvolvedor, definir cada etapa manualmente, o próprio LLM decide qual ferramenta usar, em que ordem e quando parar. É isso que torna os agentes tão poderosos e os diferencia de cadeias simples.

## 2. Ferramentas e a transformação do modelo

Já analisamos ferramentas no módulo 1. Agora, vamos recapitular o ponto central: são elas que transformam um LLM básico em algo que consegue realizar tarefas concretas. Sem ferramentas, um modelo só consegue gerar texto com base em seu treinamento. Com ferramentas, ele pode pesquisar informações atualizadas na web, consultar bancos de dados, executar código, chamar APIs e muito mais.

Em LangChain, as ferramentas são definidas como funções Python com nome, descrição e dicas de tipo. O LLM lê a descrição da ferramenta para decidir quando e como usá-la. Você pode usar ferramentas integradas do LangChain ou criar suas próprias ferramentas personalizadas usando o decorador `@tool`.

A principal vantagem dessa abordagem é que o modelo não executa a ferramenta diretamente. Em vez disso, ele gera uma solicitação de chamada de ferramenta, e o ambiente de execução do LangChain executa a ação. Essa separação é importante porque torna o processo mais seguro, mais controlável e previsível.

## 3. Anatomia de uma ferramenta

Vamos analisar a estrutura de uma ferramenta de agente. Neste exemplo, você vê algo como `@tool`. Isso é chamado de decorador. Ele registra a função específica como uma ferramenta que o agente pode descobrir e chamar. Sem esse registro, o agente não saberia para que serve a função.

Dentro da definição da função, você vê a dica de tipo. Ela informa ao LLM quais tipos de dados devem ser passados. No caso de uma função de adição, estamos dizendo que ela recebe dois valores de ponto flutuante. Também há um tipo de retorno, que informa ao agente qual tipo de dado a ferramenta envia de volta. Como a operação é matemática, a saída também é um valor numérico.

Em seguida, há a docstring. O modelo lê essa descrição para decidir quando usar a ferramenta. Quanto mais clara e específica for a documentação, mais precisa será a seleção da ferramenta. Nesse caso, a docstring descreve exatamente que a função soma dois números e é adequada para operações de adição.

Essas partes não existem apenas para documentar o código. Elas também orientam o LLM na hora de decidir se deve ou não chamar uma ferramenta. Por isso, a dica de tipo, a docstring e o tipo de retorno são tão importantes: eles ajudam o agente a interagir com o mundo externo de forma adequada.

## 4. A estrutura JSON por trás da chamada

O framework LangChain pega uma função Python e a transforma em um esquema JSON que é enviado ao modelo junto com a mensagem do usuário. Isso não significa que o LLM não entenda código Python. Ele entende. O que fazemos aqui é transformar a função em uma interface estruturada, assim o modelo pode decidir de forma mais robusta se deve ou não invocar a ferramenta.

Esse esquema JSON é a representação da funcionalidade da ferramenta. O modelo decide chamar a ferramenta com base nessa definição. O LLM não precisa “ver” o corpo da função em Python; ele lida com uma descrição estruturada que explica seu objetivo e os parâmetros esperados.

É por isso que dicas de tipo e docstrings são tão importantes. Elas funcionam como instruções para a IA: não são apenas documentação para humanos, mas também informações que o modelo usa para decidir a melhor ação.

## 5. O padrão ReAct

Como já vimos anteriormente, o padrão mais comum em agentes de IA é o ReAct, que significa “raciocínio + ação”. Ele segue um ciclo simples:

1. O agente raciocina sobre a tarefa.
2. Decide se precisa agir.
3. Chama uma ferramenta ou responde ao usuário.
4. Observa o resultado.
5. Retorna ao início do ciclo, se ainda for necessário.

Esse processo continua até que o agente tenha informações suficientes para responder. Em perguntas simples, pode haver apenas um passo. Em tarefas mais complexas, o agente pode fazer várias iterações: pesquisar, calcular, consultar e comparar informações antes de entregar a resposta final.

Quando o usuário pergunta sobre o clima em Seattle, por exemplo, o agente percebe que precisa consultar uma ferramenta de previsão do tempo. Ele chama a ferramenta, analisa o resultado e decide se já tem base suficiente para responder. Esse é o ciclo básico do ReAct e é a base por trás da maioria dos agentes do LangChain.

## 6. Construindo o primeiro agente

Agora, vamos construir nosso primeiro agente de forma prática. O primeiro passo é configurar o ambiente. Normalmente, criamos um ambiente virtual Python para isolar as dependências do projeto. Em seguida, instalamos os pacotes principais: LangChain, a integração com o provedor de modelos e, em muitos casos, LangGraph para o ambiente de execução do agente.

Também precisamos de uma chave de API do provedor escolhido, como OpenAI. A recomendação é armazená-la em um arquivo de ambiente para evitar expô-la diretamente no código.

### Instalando os pacotes

`pip install langchain langchain-openai langgraph python-dotenv`

Em seguida, configuramos as variáveis de ambiente:

```python
import os
from dotenv import load_dotenv

load_dotenv()
os.environ["OPENAI_API_KEY"] = os.getenv("OPENAI_API_KEY")
```

### Inicializando o modelo

O próximo passo é inicializar o modelo. Normalmente, fazemos isso em um objeto de chat, passando o nome do modelo que desejamos usar.

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o-mini")
```

### Definindo as ferramentas

Depois, definimos as ferramentas que o agente pode usar. Neste exemplo, usamos duas ferramentas simples: multiplicação e divisão. Cada uma recebe argumentos tipados e possui docstrings claras, o que ajuda o modelo a decidir quando usar cada uma.

```python
from langchain_core.tools import tool

@tool
def multiply(a: float, b: float) -> float:
    """Multiplica dois números e retorna o produto."""
    return a * b

@tool
def divide(a: float, b: float) -> float:
    """Divide um número por outro e retorna o resultado."""
    return a / b
```

### Criando o agente

O terceiro passo é criar o agente. Esse é o ponto central da demonstração: com poucas linhas, o LangChain monta um agente ReAct completo. Basta passar o modelo e a lista de ferramentas disponíveis.

```python
from langchain.agents import create_tool_calling_agent

agent = create_tool_calling_agent(llm, [multiply, divide])
```

### Executando o agente

Por fim, executamos o agente com uma pergunta simples. Por exemplo:

```python
from langchain.agents import AgentExecutor

executor = AgentExecutor(agent=agent, tools=[multiply, divide])
result = executor.invoke({"input": "Quanto é 15 multiplicado por 8 e dividido por 3?"})
print(result["output"])
```

O agente usa as ferramentas e retorna a resposta final. Nesse caso, o resultado é 40. Isso mostra como, com poucas linhas de código, o LangChain consegue construir um agente funcional que integra raciocínio, seleção de ferramenta e execução de ação.

## 7. Encerramento

Nesta lição, revisamos os fundamentos de um agente no LangChain e vimos como ele se diferencia de uma chamada simples a um LLM. A principal ideia é que ferramentas, descrição estruturada e padrão ReAct permitem que o modelo não apenas gere texto, mas também tome decisões e execute ações.

Relembramos a anatomia de uma ferramenta, a importância de dicas de tipo e docstrings e como o LangChain transforma uma função Python em uma ação utilizável pelo agente. Também vimos a estrutura mínima para criar um primeiro agente com apenas algumas linhas de código.

Espero que essa revisão tenha sido útil para consolidar a ideia de como os agentes funcionam na prática. Obrigado pelo seu tempo!
