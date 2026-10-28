# Por Dentro do Agente LangChain — Parte 2

## Considerações iniciais

### Visão geral

Nesta continuação, vamos retomar o ciclo do agente a partir do resultado da primeira ferramenta. O modelo usa o valor calculado para solicitar uma segunda operação, recebe o resultado e, quando já tem informações suficientes, produz uma resposta final. Acompanhar esse fluxo ajuda a entender como o LangChain decide continuar ou encerrar o loop.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Explicar como o modelo reutiliza o resultado de uma ferramenta em uma nova chamada.
- Descrever como o histórico da conversa cresce ao longo do loop do agente.
- Identificar o sinal que indica que o modelo terminou e não precisa de mais ferramentas.
- Resumir as responsabilidades do LangChain durante a execução de um agente.

### Benefícios para você

Entender a continuação do loop facilita a análise de rastreamentos, a depuração de agentes com várias etapas e a avaliação do que acontece nos bastidores de uma chamada aparentemente simples.

---

# Transcrição da aula

Boas-vindas de volta! Na lição anterior, vimos o LangChain enviar ao modelo o resultado da primeira chamada de ferramenta. Agora, vamos continuar a partir desse ponto e acompanhar como o modelo conclui o cálculo.

## 1. O modelo solicita a próxima ferramenta

O modelo recebe a conversa atualizada, que inclui o resultado da multiplicação: `15 × 8 = 120`. Como a pergunta original também pedia para dividir o resultado por 3, o modelo solicita a ferramenta de divisão com os argumentos `a = 120` e `b = 3`.

Observe que o modelo usa o resultado da primeira ferramenta como entrada para a segunda chamada. Esse é um aspecto importante do loop do agente: cada etapa pode se apoiar nos resultados das etapas anteriores.

A nova solicitação tem outro identificador, como `call_002`, para manter cada pedido associado à resposta correspondente. O LangChain repete o processo já visto: interpreta a solicitação, localiza a função de divisão no registro, executa a ferramenta e obtém o resultado `40`.

## 2. O histórico da conversa é atualizado

Depois da segunda execução, o histórico da conversa contém as mensagens necessárias para representar o percurso até aquele momento:

1. A pergunta original do usuário.
2. A solicitação do modelo para multiplicar.
3. O resultado da multiplicação.
4. A solicitação do modelo para dividir.
5. O resultado da divisão.

O LangChain envia esse histórico ao modelo novamente. Assim, o modelo pode consultar a pergunta inicial e os resultados das duas operações antes de decidir o que fazer em seguida.

Como cada mensagem se relaciona com as anteriores, o histórico registra a sequência de raciocínio e execução que levou ao resultado.

## 3. O modelo produz a resposta final

Agora o modelo tem as informações necessárias para responder à pergunta original. Como a multiplicação e a divisão já foram executadas, ele não solicita outra ferramenta. Em vez disso, retorna uma resposta em linguagem natural, com o resultado final: **40**.

O LangChain analisa essa resposta. Ele verifica se há conteúdo de texto e se existe uma nova chamada de ferramenta. Como há conteúdo e nenhuma ferramenta foi solicitada, o framework entende que o loop terminou e retorna a resposta à aplicação.

Nesse exemplo, o ciclo de chamadas de ferramenta acontece duas vezes: primeiro para multiplicar e depois para dividir. Em seguida, o modelo fornece a resposta final. Em tarefas mais complexas, o mesmo padrão pode continuar por mais etapas: o agente age, observa os resultados e raciocina novamente até conseguir concluir a solicitação.

## 4. Retorno à aplicação e rastreamento

Depois de receber a resposta final, o LangChain a retorna ao código Python. A aplicação pode então exibi-la, por exemplo, com uma chamada a `print`.

Se o rastreamento estiver ativado, é possível inspecionar cada etapa, incluindo as chamadas às ferramentas e seus resultados. Sem esse rastreamento, o usuário normalmente vê apenas a resposta final; as chamadas à API, a execução das ferramentas e as mensagens estruturadas ficam nos bastidores.

Essa abstração facilita a construção de agentes, mas compreender o fluxo interno continua sendo importante para depurar problemas e desenvolver sistemas mais complexos.

## 5. O que o LangChain faz nos bastidores

Ao criar um agente com um modelo e ferramentas e, depois, invocá-lo, o LangChain coordena várias tarefas:

- Constrói esquemas estruturados a partir das definições das ferramentas.
- Formata as mensagens para a API do modelo.
- Envia as solicitações e interpreta as respostas.
- Detecta chamadas de ferramentas e localiza as funções correspondentes no registro.
- Executa as funções Python com os argumentos recebidos.
- Anexa os resultados ao histórico da conversa.
- Decide se deve continuar o loop ou retornar a resposta final.

Em um fluxograma, esse processo pode ser visto como uma troca de informações entre a aplicação, o LangChain e o LLM. Quando uma ferramenta é solicitada, o LangChain a localiza e executa, envia o resultado de volta ao modelo com o histórico atualizado e repete o ciclo quando necessário. No exemplo, isso acontece com as funções de multiplicação e divisão.

## 6. Por que entender o fluxo interno

Frameworks como o LangChain tornam mais simples começar a construir agentes, pois automatizam muitos detalhes. Porém, à medida que os sistemas ficam mais complexos, entender esses detalhes é essencial para depurar problemas, criar loops personalizados, otimizar o desempenho e preparar aplicações para produção.

O exemplo matemático é simples, mas ilustra o mesmo padrão usado em tarefas mais elaboradas. Conhecer como as informações circulam entre o framework, o LLM e o código ajuda a compreender o comportamento do agente e a investigar falhas.

## 7. Encerramento

Nesta lição, acompanhamos o restante do loop: o modelo usou o resultado da multiplicação para solicitar a divisão, recebeu o resultado `40` e então respondeu sem chamar outra ferramenta. O LangChain retornou a resposta final à aplicação e, quando habilitado, o rastreamento permite inspecionar todo o percurso.

Esse é o ciclo completo de um agente: o modelo solicita ações, o framework executa as ferramentas, os resultados voltam ao modelo e o processo continua até que uma resposta final possa ser fornecida. Espero que esta explicação tenha ajudado a esclarecer o funcionamento interno do LangChain. Obrigado pelo seu tempo!
