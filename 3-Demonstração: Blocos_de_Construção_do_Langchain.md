# Demonstração: blocos de construção do LangChain

## Considerações iniciais

### Visão geral

Nesta demonstração, vamos colocar em prática os conceitos apresentados na aula teórica. Vamos configurar um modelo de chat, enviar uma pergunta, criar modelos de prompt e compor uma cadeia com o operador pipe. Ao final, veremos como fornecer mensagens anteriores ao modelo para dar contexto à conversa.

### Objetivos de aprendizagem

Ao concluir esta demonstração, você será capaz de:

- Identificar os pré-requisitos para executar os exemplos com LangChain e OpenAI.
- Inicializar um modelo de chat e invocá-lo com `.invoke`.
- Criar modelos de prompt padrão e de chat com valores reutilizáveis.
- Conectar um prompt, um modelo e um analisador de saída em uma cadeia.
- Usar mensagens anteriores como contexto para uma chamada ao modelo.

### Benefícios para você

Os exemplos mostram como os componentes do LangChain se conectam em um fluxo prático. Você verá como transformar uma chamada simples a um LLM em uma cadeia reutilizável e como incluir contexto para que o modelo responda considerando mensagens anteriores.

---

# Transcrição da demonstração

Boas-vindas a este passo a passo do código do LangChain! Já abordamos alguns desses conceitos na aula teórica; agora, vamos vê-los em ação.

## 1. Pré-requisitos

Para executar a demonstração, você precisa instalar o LangChain e os outros pacotes usados pelo exemplo. O comando apresentado na aula para instalar o LangChain é:

```bash
pip install langchain
```

Você também precisa de uma chave de API da OpenAI, pois o exemplo usa um modelo desse provedor. Crie a chave no painel da OpenAI e configure-a no ambiente utilizado pelo código. Mantenha a chave em segurança e não a inclua no código-fonte nem em arquivos versionados.

Com os pacotes instalados e a chave configurada, podemos prosseguir com os exemplos.

## 2. Inicialização e chamada do modelo

O primeiro passo é carregar a chave de API e inicializar o modelo de chat. A função `init_chat_model` oferece uma interface para configurar modelos de diferentes provedores. Embora a demonstração use um modelo da OpenAI, também seria possível utilizar modelos de outros provedores compatíveis, como Anthropic ou Google.

Depois de inicializar o modelo, podemos chamá-lo com `.invoke`. Esse método recebe uma entrada — por exemplo, uma pergunta — e retorna um objeto de resposta. Para obter apenas o texto gerado, acessamos `response.content`, em vez de exibir todos os metadados da resposta.

No exemplo da aula, uma pergunta simples sobre o LangChain é enviada ao modelo, que retorna uma explicação. Essa é a forma mais direta de interagir com o LLM.

## 3. Modelos de prompt

Um modelo de prompt é um modelo reutilizável que pode ser preenchido com valores diferentes. Em vez de escrever um texto novo para cada solicitação, definimos o prompt uma vez com um espaço reservado e fornecemos o valor quando o utilizamos.

Também podemos usar um modelo de prompt de chat, composto por mensagens com papéis diferentes:

- **Sistema:** define instruções e o comportamento esperado do modelo.
- **Humano:** representa a solicitação do usuário.

No exemplo, uma mensagem de sistema define a orientação da resposta e a mensagem humana pede que o modelo explique um conceito, usando um marcador de posição para o tópico.

## 4. Cadeias e operador pipe

As cadeias (*chains*) conectam componentes reutilizáveis em um fluxo. O operador pipe (`|`) permite encadear as etapas da esquerda para a direita. No exemplo, a cadeia tem três componentes:

1. **Prompt:** preenche os espaços reservados com os valores fornecidos.
2. **Modelo:** recebe o prompt e gera uma resposta.
3. **Analisador de saída:** extrai o texto da resposta do modelo.

O analisador de saída de string converte a resposta em texto simples, evitando que seja necessário extrair manualmente o conteúdo do objeto retornado pelo modelo.

## 5. Execução de uma cadeia

Depois de montar a cadeia, podemos executá-la com `chain.invoke`. A chamada recebe os valores necessários para preencher o modelo de prompt. Por exemplo, podemos pedir uma explicação sobre loops `for` com um exemplo em Python; para reutilizar a cadeia, basta fornecer outro tópico.

Durante a execução, o LangChain preenche o prompt, envia-o ao modelo e encaminha a resposta ao analisador de saída. O analisador extrai o texto final. Assim, cada etapa transforma e repassa os dados para a seguinte.

## 6. Uso de mensagens anteriores como contexto

Na parte final da demonstração, veremos como fornecer contexto de conversas anteriores. Por padrão, chamadas independentes ao modelo não mantêm automaticamente o histórico entre si. Para que o modelo considere mensagens anteriores, precisamos armazená-las e incluí-las no prompt da chamada.

O exemplo usa um armazenamento simples em memória com mensagens humanas e respostas da IA. Em seguida, essas mensagens são inseridas no prompt de chat antes de invocar o modelo. Depois de informar o nome “Alex” em uma mensagem anterior, podemos perguntar qual era o nome: como o histórico foi incluído, o modelo tem contexto para responder.

Sem fornecer as mensagens anteriores, o modelo não teria esse contexto. A memória, nesse exemplo, consiste em armazenar e reutilizar o histórico como parte da entrada do modelo.

## 7. Encerramento

Nesta demonstração, vimos como inicializar e invocar um modelo, criar modelos de prompt, conectar componentes com o operador pipe e fornecer mensagens anteriores como contexto.

Esses exemplos mostram como os blocos de construção do LangChain podem ser combinados para criar fluxos reutilizáveis. Espero que a demonstração tenha sido útil. Obrigado pelo seu tempo!
