# Guardrails e segurança

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar os *guardrails* (mecanismos de proteção) disponíveis no SDK de Agentes da OpenAI. Como agentes são controlados por grandes modelos de linguagem (LLMs), suas respostas e ações podem ser imprevisíveis. Os *guardrails* ajudam a verificar entradas e saídas e a interromper a execução quando uma regra de segurança é violada.

Também vamos acompanhar um exemplo de proteção de entrada e conhecer o recurso de rastreamento, que permite observar as etapas executadas pelo agente.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Diferenciar *guardrails* de entrada e de saída.
- Identificar exemplos de uso para cada tipo de proteção.
- Explicar como um mecanismo de proteção pode interromper a execução de um agente.
- Descrever, em linhas gerais, como configurar uma verificação de entrada.
- Entender como o rastreamento ajuda a analisar a execução de um agente.

### Benefícios para você

Os *guardrails* ajudam a controlar o que o agente processa e o que apresenta como resposta. O rastreamento complementa essas proteções ao permitir investigar o comportamento do agente, verificar o uso de ferramentas e identificar oportunidades de melhoria.

---

# Transcrição da aula

Bem-vindos a esta lição sobre *guardrails* e segurança. Os mecanismos de proteção funcionam como uma rede de segurança para agentes controlados por LLMs. Eles podem verificar entradas e saídas e, dependendo da configuração, executar em paralelo com o agente principal ou impedir que ele seja iniciado.

## 1. Tipos de guardrails

O SDK de Agentes da OpenAI oferece dois tipos principais de mecanismos de proteção.

### Guardrails de entrada

São executados antes de o agente processar a entrada do usuário. Podem ser usados para:

- Bloquear solicitações fora do tópico esperado.
- Detectar tentativas de injeção de prompt.
- Validar se a entrada está no formato esperado.

### Guardrails de saída

São executados depois que o agente gera uma resposta. Podem ser usados para:

- Verificar possíveis alucinações.
- Aplicar diretrizes de conteúdo ou o tom da marca.
- Evitar a exposição de dados confidenciais.

Os *guardrails* fazem parte de uma abordagem de segurança em profundidade e podem complementar outras medidas de validação e proteção.

## 2. Como os guardrails funcionam

Um mecanismo de proteção pode ser um agente auxiliar ou uma função que verifica a entrada ou a saída. Se a verificação falhar, ele aciona um *tripwire* — um mecanismo de interrupção — que para o agente principal.

Por exemplo, um *guardrail* de entrada pode bloquear uma solicitação que tente fazer o agente ignorar instruções anteriores e revelar informações protegidas.

## 3. Exemplo de proteção de entrada

O exemplo apresentado na aula verifica se uma pergunta está relacionada a História e bloqueia a solicitação caso ela esteja fora desse tema.

### Definindo a saída da verificação

Primeiro, é definido um modelo Pydantic para estruturar o resultado da verificação. A classe `TopicCheck` representa o tópico e um valor booleano que indica se a pergunta está dentro do tema. O Pydantic é uma biblioteca Python usada para definir e validar estruturas de dados.

### Criando o agente verificador

Em seguida, é criado um agente auxiliar com instruções para indicar se a pergunta é sobre História. A saída estruturada permite que o programa consulte essa decisão de forma previsível.

### Aplicando o guardrail

Uma função de proteção é definida com o decorador `@input_guardrail`. Ela executa o agente verificador sobre a entrada do usuário. Se a pergunta não for sobre História — isto é, se `is_on_topic` for falso —, o *tripwire* é acionado e a execução do agente principal é interrompida.

Por fim, o *guardrail* é registrado no agente principal. Assim, uma pergunta de Matemática direcionada ao agente de História é bloqueada antes de ser processada por ele.

## 4. Rastreamento da execução

O rastreamento permite visualizar o que aconteceu durante a execução de um agente. A aula apresenta o painel da OpenAI, em `platform.openai.com`, como um lugar para consultar esses registros. A disponibilidade e a configuração do recurso podem variar; consulte a documentação atual para confirmar como habilitá-lo no seu projeto.

Um rastreamento pode ajudar a identificar:

- Quais agentes foram executados e em que ordem.
- Quais ferramentas foram chamadas, com seus argumentos e resultados.
- Quando ocorreram transferências entre agentes.
- Se os mecanismos de proteção foram aprovados ou acionados.
- Quantos tokens foram consumidos em cada etapa.

Essas informações são úteis para depurar respostas incorretas, analisar custos e avaliar se o agente utilizou as ferramentas e transferências adequadas. Os rastreamentos também podem ser exportados para ferramentas externas.

## 5. Recapitulando

Nesta lição, vimos os *guardrails* de entrada e de saída, que ajudam a verificar o que o agente recebe e o que produz. Também acompanhamos um exemplo de verificação de tópico com Pydantic, um agente auxiliar e um *tripwire* para interromper solicitações fora do tema.

Por fim, conhecemos o rastreamento como recurso para analisar as etapas, as ferramentas e os mecanismos de proteção envolvidos na execução do agente. Consulte sempre a documentação atual para confirmar os detalhes de configuração disponíveis.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
