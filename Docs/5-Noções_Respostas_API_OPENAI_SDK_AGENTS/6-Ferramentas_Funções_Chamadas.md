# Ferramentas e chamadas de funções

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar as ferramentas disponíveis no SDK de Agentes da OpenAI e entender como elas permitem que um agente vá além da geração de texto. O SDK oferece ferramentas hospedadas, ferramentas de função personalizadas e a possibilidade de usar agentes como ferramentas.

Também vamos acompanhar o fluxo de chamada de uma ferramenta e comparar, em linhas gerais, a experiência de desenvolvimento com o SDK de Agentes e com o LangChain.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Identificar os três tipos de ferramentas suportados pelo SDK de Agentes.
- Entender como transformar uma função Python em uma ferramenta usando `@function_tool`.
- Reconhecer o papel das dicas de tipo e da docstring na definição de uma ferramenta.
- Descrever como o agente e o executor trabalham juntos para chamar ferramentas.
- Comparar as etapas gerais de desenvolvimento com o SDK de Agentes e o LangChain.

### Benefícios para você

As ferramentas permitem que agentes acessem capacidades externas ou executem lógica personalizada. Ao entender como defini-las e registrá-las, você poderá escolher entre recursos hospedados prontos para uso, funções próprias ou a delegação para agentes especializados.

---

# Transcrição da aula

Bem-vindos de volta. Nesta lição, vamos analisar as ferramentas e as chamadas de funções. As ferramentas tornam os agentes mais capazes: sem elas, um agente se limita a responder como um chatbot.

## 1. Tipos de ferramentas

O SDK de Agentes suporta três tipos de ferramentas.

### Ferramentas hospedadas

São ferramentas fornecidas pela OpenAI e prontas para uso. Entre os exemplos apresentados estão:

- busca na web, para pesquisar na internet;
- interpretador de código, para executar código Python;
- busca de arquivos, para pesquisar documentos enviados.

Essas ferramentas podem ser adicionadas à lista de ferramentas do agente.

### Ferramentas de função

São funções Python personalizadas que o agente pode chamar. O decorador `@function_tool` transforma uma função em uma ferramenta, e o SDK gera o esquema a partir das dicas de tipo.

O modelo recebe informações sobre o nome da função, seus parâmetros e sua docstring. Por isso, as dicas de tipo e uma descrição clara da função são importantes.

### Agentes como ferramentas

Também é possível disponibilizar um agente para outro agente como uma ferramenta, por exemplo, usando `agent.as_tool`. Isso permite que um agente gerenciador delegue tarefas a agentes especializados.

Esta lição não explora essa abordagem em profundidade, mas ela é uma das opções suportadas pelo SDK.

### Qual tipo escolher?

Como regra geral, comece por uma ferramenta hospedada quando ela já oferecer a funcionalidade necessária, como busca na web ou busca de arquivos. Use ferramentas de função quando precisar implementar lógica personalizada.

## 2. Definindo ferramentas de função

Uma ferramenta de função começa como uma função Python comum. Para que o SDK gere o esquema corretamente, a função deve declarar os tipos dos parâmetros e incluir uma docstring que explique seu propósito.

Por exemplo, uma ferramenta matemática pode receber dois números de ponto flutuante. Depois de aplicar `@function_tool`, a função pode ser registrada na lista de ferramentas do agente.

O SDK cuida da integração da chamada de função: o modelo recebe o esquema e pode selecionar a ferramenta adequada quando a solicitação exigir aquela operação.

## 3. Registrando as ferramentas no agente

Ao criar o agente, você fornece seu nome, o modelo, as instruções e as ferramentas que ele poderá utilizar.

As instruções definem o comportamento do agente, enquanto as ferramentas fornecem suas capacidades. Por exemplo, para responder a uma pergunta matemática, o agente pode escolher uma ferramenta de cálculo, receber o resultado e formular uma resposta em linguagem natural.

## 4. Fluxo de chamada de uma ferramenta

O fluxo geral pode ser resumido assim:

1. Definir as ferramentas com `@function_tool`, dicas de tipo e docstrings.
2. Criar o agente com nome, modelo, instruções e lista de ferramentas.
3. Enviar ao agente a pergunta do usuário.
4. O executor encaminha a solicitação ao modelo por meio do SDK.
5. O modelo decide se precisa de uma ferramenta e seleciona a apropriada.
6. O agente executa a ferramenta e devolve o resultado ao modelo.
7. O ciclo pode continuar até que o modelo produza a resposta final.

Por exemplo, diante de uma expressão como “15 vezes 8, dividido por 3”, o modelo pode determinar que uma ferramenta matemática é necessária. Após receber o resultado, ele pode concluir a resposta sem novas chamadas.

Esse processo é semelhante ao fluxo de chamadas de ferramentas visto anteriormente com LangChain: o modelo decide quando usar uma ferramenta, recebe o resultado e continua a interação.

## 5. Comparação geral com LangChain

As duas estruturas permitem configurar modelos, definir ferramentas, criar agentes, executá-los e obter respostas. A aula apresenta as seguintes diferenças gerais:

1. **Configuração do modelo:** no LangChain, o modelo costuma ser inicializado explicitamente. No SDK de Agentes, ele pode ser configurado diretamente na definição do agente.
2. **Definição de ferramentas:** ambos suportam ferramentas. O LangChain usa o decorador `@tool`, enquanto o SDK de Agentes usa `@function_tool`.
3. **Criação do agente:** o LangChain organiza ferramentas, modelos e orquestração em diferentes componentes. O SDK de Agentes reúne esses elementos numa definição de agente mais direta.
4. **Execução:** no LangChain, o agente é invocado por uma interface baseada em mensagens. No SDK de Agentes, o executor oferece métodos como `Runner.run_sync`.
5. **Acesso à resposta:** a forma de processar a resposta depende do formato usado. No SDK de Agentes, a saída final em texto pode ser acessada por `result.final_output`.

A aula considera o SDK de Agentes uma opção mais leve e direta para iniciantes, enquanto o LangChain oferece uma estrutura de orquestração mais ampla. A escolha depende das necessidades e da experiência de cada projeto.

## 6. Recapitulando

Nesta lição, vimos os três tipos de ferramentas do SDK de Agentes: ferramentas hospedadas, ferramentas de função e agentes como ferramentas. Também aprendemos que funções Python podem ser transformadas em ferramentas com `@function_tool`, usando dicas de tipo e docstrings para descrever seus parâmetros e finalidade.

Por fim, acompanhamos o ciclo em que o agente seleciona uma ferramenta, recebe o resultado e continua até produzir uma resposta, além de comparar as etapas gerais de desenvolvimento com LangChain.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
