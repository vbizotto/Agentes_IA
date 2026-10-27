# Demonstração: Criando seu Primeiro Agente

## Considerações iniciais

### Visão geral

Nesta demonstração, vamos acompanhar a criação de um agente simples com LangChain. A proposta é mostrar como o agente usa o padrão ReAct para decidir se responde diretamente ou se precisa acionar uma ferramenta. Também veremos como a função `createAgent` conecta o modelo e as ferramentas, abstraindo o loop de execução.

### Objetivos de aprendizagem

Ao concluir esta demonstração, você será capaz de:

- Reconhecer as etapas principais da criação de um agente com LangChain.
- Entender o papel do modelo e das ferramentas no funcionamento do agente.
- Compreender como o padrão ReAct organiza o ciclo de raciocínio, ação e observação.
- Interpretar o rastreamento de execução de um agente ao responder a consultas.

### Benefícios para você

Esta demonstração conecta os conceitos vistos anteriormente a um exemplo prático. Ao observar o agente em execução, fica mais fácil entender como o framework coordena o modelo e as ferramentas sem exigir que você implemente manualmente o loop de raciocínio.

---

# Transcrição da aula

Boas-vindas a esta demonstração! Vamos retomar o primeiro código de agente que vimos no módulo 1 e revisamos na lição anterior. O exemplo é simples de propósito, para facilitar a compreensão dos conceitos.

## 1. O padrão ReAct e os pré-requisitos

A ideia é mostrar como o agente usa o padrão ReAct — *Reason* (raciocinar), *Act* (agir) e *Observe* (observar) — em um loop. Também veremos como a função `createAgent` do LangChain ajuda a construir o agente.

Para acompanhar a demonstração, é necessário ter os pacotes usados pelo exemplo instalados e uma chave de API da OpenAI configurada. Se você seguiu a demonstração anterior, provavelmente já preparou esses pré-requisitos.

## 2. Carregando as variáveis de ambiente e inicializando o modelo

Primeiro, carregamos as variáveis de ambiente. Essa é uma boa prática: informações sensíveis, como chaves de API, não devem ser armazenadas diretamente nos arquivos de código. Elas devem ficar em um arquivo de ambiente separado, mantendo os segredos fora do código.

Em seguida, inicializamos o modelo. Como vimos no módulo 1, podemos pensar nele como o cérebro do agente: o LLM interpreta a pergunta, decide qual ferramenta usar e, por fim, gera uma resposta.

Na demonstração original, o modelo é inicializado com o modelo da OpenAI indicado durante a aula. Esse é o primeiro passo do processo.

## 3. Definindo as ferramentas

O segundo passo é definir as ferramentas. Podemos pensar nelas como as mãos do agente: elas permitem que ele faça coisas, em vez de apenas raciocinar e responder.

Cada ferramenta deve ter:

- Um nome claro.
- Uma docstring descritiva, que explique o que ela faz e quando deve ser usada.
- Dicas de tipo, que indiquem ao LLM quais entradas são esperadas.

Neste exemplo, são usadas funções de multiplicação, divisão e adição. As descrições ajudam o LLM a entender a finalidade de cada ferramenta e a escolher a mais adequada para cada consulta.

## 4. Criando o agente

O terceiro passo é criar o agente. A função `createAgent` reúne o modelo e as ferramentas e monta a camada de orquestração.

Essa etapa esconde boa parte da complexidade do processo. O agente raciocina sobre o que fazer, chama uma ferramenta quando necessário, observa o resultado e repete o ciclo até concluir a tarefa.

A grande vantagem dos frameworks é que você não precisa escrever esse loop manualmente: o LangChain coordena a execução. Em lições posteriores, esse processo será explorado com mais detalhes, inclusive em outros frameworks.

## 5. Executando o agente e observando o rastreamento

O último passo é executar o agente chamando `agent.invoke` e fornecendo uma consulta. A demonstração começa com uma pergunta simples de adição e depois apresenta outra consulta que exige duas operações.

O rastreamento da execução mostra o percurso do agente. O usuário faz uma pergunta e o LLM decide se consegue respondê-la diretamente ou se precisa de uma ferramenta. Quando uma ferramenta é necessária, o agente a executa, recebe o resultado e o envia de volta ao LLM. Por fim, o modelo produz a resposta.

Ao executar o programa, é possível observar os rastreamentos das diferentes perguntas e acompanhar o agente em ação. Embora o exemplo seja simples, ele mostra como o framework coordena o loop ReAct por trás de uma chamada ao agente.

## 6. Encerramento

Nesta demonstração, vimos como criar um agente, disponibilizar ferramentas e executá-lo com consultas. Também acompanhamos o papel do loop ReAct: o LLM decide se pode responder sozinho ou se precisa solicitar ao framework que execute uma ferramenta e retorne o resultado.

Esse exemplo apresenta um agente básico em funcionamento e consolida os conceitos introduzidos nas lições anteriores. Espero que a demonstração tenha sido útil. Obrigado pelo seu tempo!
