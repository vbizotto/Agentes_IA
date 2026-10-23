# Aula 03 — Padrões de raciocínio em agentes de IA

## Considerações iniciais

### Visão geral da aula

Nesta aula, você vai explorar os principais padrões de raciocínio utilizados por agentes de IA. O foco será entender como o agente decide, planeja e atua em cada etapa do problema, avaliando quando deve raciocinar, quando deve usar ferramentas e quando deve apresentar a resposta final.

### Objetivos de aprendizagem

Ao concluir esta aula, você será capaz de:

- Explicar o que é o padrão *Chain of Thought*.
- Compreender o funcionamento do padrão *ReAct*.
- Diferenciar *Chain of Thought*, *ReAct* e *Tree of Thought*.
- Identificar qual padrão é mais adequado para cada tipo de problema.

### Recurso complementar

Para aprofundar estes conceitos, revise os exemplos de raciocínio, busca de informações e uso de ferramentas em contextos reais de agentes.

### Benefícios para você

Ao dominar esses padrões, você será capaz de projetar agentes com decisões mais transparentes, confiáveis e eficientes. Isso ajuda a reduzir erros de raciocínio, melhorar a capacidade de depuração e escolher a arquitetura mais adequada para cada caso de uso.

---

# Transcrição da aula

Bem-vindos de volta! Nesta aula, vamos analisar alguns padrões de raciocínio e examinar como os agentes raciocinam, planejam e decidem qual será o próximo passo.

## 1. Introdução aos padrões de raciocínio

Três dos principais modelos de raciocínio utilizados em agentes de IA são:

- *Chain of Thought* (Cadeia de Pensamento)
- *ReAct* (raciocínio + ação)
- *Tree of Thought* (Árvore de Pensamento)

Cada um desses padrões tem um papel diferente no processo de resolução de problemas. O objetivo central é permitir que o agente não apenas responda, mas também siga uma lógica de decisão que possa ser observada, avaliada e ajustada.

## 2. Chain of Thought

O *Chain of Thought* é uma técnica simples, mas extremamente importante. A ideia central é não pedir ao modelo apenas qual é a resposta, mas pedir que ele mostre seu processo de raciocínio.

Isso funciona muito bem para matemática, lógica, quebra-cabeças e análises estruturadas. Em vez de um modelo gerar apenas uma resposta final, ele é instruído a raciocinar e apresentar os passos intermediários.

### Como funciona

Em vez de perguntar diretamente: "Qual é o resultado?", você pede algo como: "Vamos pensar passo a passo." Isso incentiva o modelo a decompor o problema e apresentar uma sequência lógica antes da resposta final.

### Variações

Existem duas variações muito comuns:

- *Zero-Shot Chain of Thought*: você acrescenta uma instrução simples ao prompt, como "Vamos pensar passo a passo".
- *Few-Shot Chain of Thought*: você fornece alguns exemplos de raciocínio para mostrar o padrão esperado.

### Vantagens

Esse padrão oferece transparência. Você consegue visualizar como a resposta foi obtida e identificar exatamente onde o raciocínio falhou. Isso facilita a depuração e a análise do comportamento do sistema.

### Exemplo prático

Considere o seguinte problema: "Uma loja tem 15 maçãs e vende 3 pacotes de 4 maçãs cada. Quantas restam?"

Sem a técnica de cadeia de pensamento, o modelo pode responder diretamente com um valor, mas sem deixar claro como chegou a ele. Com o *Chain of Thought*, o modelo pode seguir um raciocínio como:

- 3 pacotes de 4 maçãs totalizam 12 maçãs;
- 15 menos 12 resulta em 3;
- resposta final: 3 maçãs restam.

### Limitações

Apesar de útil, o *Chain of Thought* isolado tem limitações importantes. Ele depende exclusivamente do conhecimento interno do modelo e não consegue consultar fontes externas nem verificar a realidade. Se o modelo estiver equivocado, ele pode apresentar um raciocínio convincente, mas incorreto.

Em outras palavras, ele melhora a transparência, mas não resolve a necessidade de confirmar fatos com o mundo exterior.

## 3. ReAct

O segundo padrão de raciocínio, bastante utilizado, chama-se *ReAct*. O termo *ReAct* vem da combinação de *reasoning* (raciocínio) e *acting* (ação).

Esse padrão combina o raciocínio intermediário com a execução de ações. O agente pensa sobre o problema, decide qual ferramenta deve usar, executa a ação e analisa o resultado antes de responder.

### Fluxo típico

Como vimos na aula anterior, um exemplo clássico é a busca de voos:

1. O agente recebe a tarefa: "preciso encontrar voos de Austin para Zurique".
2. Raciocina: "preciso consultar uma ferramenta de busca de voos".
3. Executa a ação: chama a ferramenta com os parâmetros necessários.
4. Observa os resultados: recebe uma lista de voos e preços.
5. Decide: "agora posso apresentar a opção mais barata ou a melhor alternativa".
6. Responde ao usuário com a conclusão.

Esse ciclo de raciocínio, ação e observação é o que caracteriza o padrão *ReAct*.

### Por que ele é tão usado?

O *ReAct* oferece um equilíbrio entre:

- transparência;
- capacidade de execução;
- uso de ferramentas externas;
- custo e eficiência.

Por esse motivo, ele é amplamente adotado em produção.

### Relação com o Chain of Thought

O *ReAct* pode ser visto como uma evolução do *Chain of Thought*. Em vez de apenas mostrar o raciocínio, o agente também usa esse raciocínio para decidir quando e como agir. Isso permite que ele consulte APIs, ferramentas e dados externos antes de responder.

## 4. Tree of Thought

O terceiro padrão é o *Tree of Thought* (Árvore de Pensamento). Ele é mais complexo e mais avançado.

A ideia central é que o agente considera várias abordagens alternativas ao mesmo tempo, em vez de seguir apenas um único caminho de raciocínio. É como um jogador de xadrez que avalia diferentes possíveis jogadas antes de decidir a melhor opção.

### Exemplo de analogia

Imagine que o agente está tentando resolver um problema. Em vez de escolher uma única linha de raciocínio, ele explora várias ramificações:

- "Se eu fizer isso, o que acontece?"
- "Se eu tentar essa alternativa, qual será o resultado?"
- "Qual caminho parece mais promissor?"

Ele então compara os resultados e escolhe o melhor curso de ação.

### Quando usar

Esse padrão é útil em problemas mais complexos, em que há mais de uma possibilidade de abordagem. Ele oferece maior flexibilidade, mas também exige mais processamento e custo computacional.

## 5. Comparando os padrões

Os três padrões têm papéis distintos:

- *Chain of Thought*: melhora a transparência e o raciocínio interno.
- *ReAct*: combina raciocínio com ação e uso de ferramentas.
- *Tree of Thought*: explora múltiplas alternativas antes de decidir.

Na prática, a maioria dos agentes em ambientes de produção usa *ReAct* porque equilibra bem custo, capacidade e observabilidade. Ainda assim, conhecer os outros padrões permite escolher a abordagem mais adequada para cada cenário.

## 6. Conclusão

Os padrões de raciocínio são fundamentais para transformar um LLM em um agente útil e eficaz. O *Chain of Thought* melhora a explicabilidade do raciocínio; o *ReAct* adiciona ação e acesso a ferramentas externas; e o *Tree of Thought* amplia a capacidade de explorar alternativas.

A escolha do padrão correto depende do problema, do custo desejado e do nível de complexidade da tarefa. Entender essas diferenças é essencial para projetar agentes mais inteligentes, confiáveis e prontos para uso real.
