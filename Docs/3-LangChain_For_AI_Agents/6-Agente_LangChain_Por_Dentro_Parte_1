# Por Dentro do Agente LangChain

## Considerações iniciais

### Visão geral

Nesta lição, vamos examinar o que acontece nos bastidores quando um agente LangChain é executado. Embora uma chamada como `agent.invoke` pareça simples, o framework coordena uma sequência de mensagens entre a aplicação, o modelo e as ferramentas. Usando um exemplo matemático, vamos acompanhar esse fluxo passo a passo.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Descrever o fluxo de controle entre a aplicação, o LangChain e o modelo.
- Entender como as ferramentas são descritas para o LLM por meio de esquemas estruturados.
- Explicar como uma solicitação de chamada de ferramenta é interpretada e executada.
- Compreender como os resultados das ferramentas são vinculados às solicitações correspondentes e enviados de volta ao modelo.

### Benefícios para você

Entender o que ocorre por trás de `agent.invoke` facilita a depuração e ajuda a identificar o papel de cada componente. Também mostra quais tarefas o framework executa automaticamente e quais ações continuam sob o controle da sua aplicação.

---

# Transcrição da aula

Boas-vindas a esta lição sobre os bastidores do agente LangChain! Quando você chama `agent.invoke`, como vimos na aula anterior, pode parecer que está executando apenas uma linha de código. Internamente, porém, há um loop completo. Vamos usar o exemplo matemático anterior, que exigia mais de uma chamada de ferramenta, para entender esse processo.

Nesta aula, analisaremos as camadas envolvidas e as mensagens estruturadas que circulam entre o código LangChain e o modelo. Ao final, você entenderá melhor o que acontece durante essa chamada. Como o conteúdo é extenso, ele foi dividido em duas lições.

## 1. O fluxo começa na aplicação

Tudo começa quando o usuário executa o script Python. O script chama a função `runAgent` com uma pergunta matemática, por exemplo: “Quanto é 15 multiplicado por 8 e dividido por 3?”. Embora o cálculo seja simples, ele ajuda a ilustrar a comunicação entre o código, o LangChain e o LLM.

Dentro de `runAgent`, o código chama `agent.invoke`. Esse é o ponto de entrada no loop do agente LangChain. É importante entender a cadeia de controle:

1. O usuário interage com a aplicação.
2. A aplicação interage com o LangChain.
3. O LangChain interage com a API do modelo.

O usuário não se comunica diretamente com o LLM. Essa separação mantém a aplicação no controle: ela decide quais ferramentas estão disponíveis, como os resultados são formatados e o que o modelo pode ou não fazer.

## 2. O LangChain envia mensagens e ferramentas ao modelo

Na primeira chamada à API do modelo, o LangChain envia dois elementos:

- Um array de mensagens que representa a conversa até aquele momento — inicialmente, apenas a pergunta do usuário.
- Um array com as ferramentas disponíveis para o modelo.

Cada definição de ferramenta inclui seu nome, sua descrição e o esquema dos parâmetros, como os nomes dos argumentos, seus tipos e quais são obrigatórios.

O LangChain gera esses esquemas inspecionando as funções Python registradas como ferramentas. Ele usa a assinatura da função, as dicas de tipo e a docstring para construir uma descrição estruturada em JSON. Assim, o modelo recebe uma representação das ferramentas disponíveis antes de decidir como responder.

## 3. O modelo solicita uma chamada de ferramenta

O modelo analisa a pergunta e as ferramentas disponíveis. Para calcular 15 multiplicado por 8 e depois dividido por 3, por exemplo, ele pode decidir começar pela multiplicação.

O modelo não executa o código Python. Em vez disso, retorna uma solicitação estruturada para chamar a ferramenta de multiplicação, informando os argumentos `a = 15` e `b = 8`. Nesse momento, o campo de conteúdo da resposta pode estar vazio: o modelo ainda não está apresentando uma resposta final, mas solicitando uma ação.

A solicitação também inclui um identificador de chamada, como `call_001`. Esse identificador será usado para associar o resultado à solicitação original. Os argumentos são representados em formato JSON, que a aplicação precisa interpretar.

Esse formato estruturado segue o padrão de chamadas de ferramentas aceito pela API do modelo. O modelo envia a solicitação de volta ao LangChain, em vez de executar a função diretamente.

## 4. O LangChain interpreta a resposta

Quando recebe a resposta do modelo, o LangChain verifica se há conteúdo de texto e se existe uma solicitação de chamada de ferramenta. Se o conteúdo estiver vazio e a chamada estiver presente, o framework entende que o modelo ainda não terminou.

O LangChain extrai as informações necessárias para executar a ação:

- O nome da ferramenta, como `multiply`.
- Os argumentos, neste caso `a = 15` e `b = 8`.
- O identificador da chamada, como `call_001`.

Essa análise é gerenciada automaticamente pelo framework. Sem o LangChain, a aplicação teria que implementar manualmente a interpretação da resposta e a lógica de chamada das ferramentas.

## 5. Do nome da ferramenta à função Python

O modelo conhece o nome da ferramenta como uma string, mas uma string não executa código. Para conectar esse nome à função Python correspondente, o LangChain mantém um registro interno que associa os nomes das ferramentas às referências das funções reais.

Quando o agente é criado com o modelo e a lista de ferramentas, o LangChain monta esse registro. Ao receber o nome `multiply`, ele consulta o registro e encontra a função Python que deve executar.

Essa associação conecta dois mundos: o modelo trabalha com texto e JSON, enquanto o código Python executa as operações. Quando o LangChain identifica a função solicitada, o fluxo passa do raciocínio do modelo à execução efetiva do código.

## 6. Execução e retorno do resultado

O LangChain executa a função Python com os argumentos recebidos. No exemplo, a multiplicação de 15 por 8 retorna `120`. Essa etapa é uma execução normal de Python; não há inteligência artificial envolvida no cálculo.

Em aplicações reais, uma ferramenta poderia consultar um banco de dados, chamar uma API, enviar um e-mail, criar um chamado, ler arquivos ou provisionar recursos na nuvem. O padrão de interação permanece o mesmo, embora a ação seja mais complexa.

Depois de executar a ferramenta, o LangChain envia o resultado de volta ao modelo junto com o histórico da conversa. Esse histórico inclui:

1. A mensagem original do usuário.
2. A solicitação de chamada da ferramenta feita pelo modelo.
3. A resposta da ferramenta.

A resposta da ferramenta é identificada como uma mensagem de ferramenta, e não como uma mensagem do usuário ou do assistente. Ela também inclui o identificador da chamada, como `call_001`, vinculando o resultado `120` à solicitação de multiplicação correspondente.

Esse contexto permite que o modelo continue o raciocínio: ele solicitou a multiplicação, o LangChain a executou e agora o resultado está disponível. Como os LLMs não mantêm estado entre chamadas, cada nova solicitação precisa incluir o histórico necessário para continuar a conversa.

## 7. Continuação do ciclo

Com o resultado da multiplicação disponível, o modelo pode continuar o raciocínio e solicitar a próxima ferramenta — neste exemplo, a divisão. A aula interrompe o acompanhamento nesse ponto para continuar o fluxo na lição seguinte.

## 8. Encerramento

Nesta primeira parte, acompanhamos o caminho de uma chamada a `agent.invoke`: a aplicação envia a pergunta, o LangChain compartilha as mensagens e as ferramentas com o modelo, o modelo solicita uma ação, e o framework identifica e executa a função Python correspondente. Em seguida, o resultado é associado à chamada original e enviado de volta ao modelo com o histórico da conversa.

Esse fluxo mostra como o LangChain coordena o raciocínio do modelo e a execução de ferramentas sem que a aplicação precise implementar manualmente cada etapa. Na próxima lição, o exemplo continuará a partir do resultado da primeira operação.
