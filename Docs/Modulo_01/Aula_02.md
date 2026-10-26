# Aula 02 — Componentes fundamentais de um agente de IA

## Considerações iniciais

### Visão geral da aula

Nesta aula, você vai entender que todo agente de IA é formado por três blocos centrais: o LLM, as ferramentas e o loop de execução. O objetivo é conectar esses elementos em uma visão prática de arquitetura, mostrando como um agente transforma um modelo de linguagem em um sistema capaz de perceber, raciocinar, agir e responder com base em observações do mundo real.

### Objetivos de aprendizagem

Ao concluir esta aula, você será capaz de:

- Explicar o papel do LLM em um agente de IA.
- Compreender como as ferramentas ampliam a capacidade de ação do agente.
- Entender a função do loop de execução e da orquestração.
- Identificar trade-offs entre capacidade, custo e latência na escolha de um modelo.

### Recurso complementar

Para aprofundar este tema, revise os exemplos de *tool calling*, orquestração e prompts de sistema aplicados ao longo do curso.

### Benefícios para você

Ao dominar esses conceitos, você conseguirá projetar agentes mais eficientes, seguros e orientados a objetivos. Isso também ajudará você a compreender por que a combinação entre modelo, ferramentas e orquestração é essencial para construir sistemas reais de IA agêntica.

---

# Transcrição da aula

Bem-vindo(a)! Nesta lição, vamos analisar os componentes fundamentais de um agente de IA.

## 1. Os três pilares de um agente

Agora que você entende o que é um agente, vamos dividi-lo em três componentes centrais: o "cérebro" (LLM), as "ferramentas" e a camada de orquestração — o que chamamos de "loop" (ciclo).

Todo sistema de agentes, independentemente de sua complexidade, resume-se a esses três elementos. Vamos começar pelo LLM. Dentro de um agente, o LLM desempenha várias funções: ele compreende a intenção, planeja etapas, seleciona ferramentas, interpreta resultados e gera as respostas finais.

O LLM pode ser composto por um ou mais modelos de qualquer porte e pode ser orientado por estratégias de raciocínio, como *Chain-of-Thought* (cadeia de pensamento) e *ReAct* — tópicos que abordaremos na próxima aula. Além disso, um mesmo LLM pode sustentar diferentes agentes com configurações de ferramentas distintas, sem a necessidade de novo treinamento (*retraining*).

O segundo componente fundamental de qualquer agente são as ferramentas. Elas são o que conferem poder aos agentes: sem elas, um LLM limita-se a gerar texto. Com ferramentas, ele pode consultar bancos de dados, chamar APIs, executar código e realizar ações no mundo real.

O terceiro componente é o que chamamos de *loop*. É nele que tudo se integra: o *loop* executa o ciclo de raciocínio, monitora o estado, gerencia a memória, direciona o uso de ferramentas e aplica regras de segurança. Uma boa forma de visualizar o *loop* é encará-lo como um sistema operacional para o agente; ele decide se o ciclo deve continuar, ser interrompido, sofrer uma nova tentativa ou ser escalado.

É aqui que reside a verdadeira complexidade de engenharia. Portanto, esses são os três componentes centrais. Vamos analisar cada um deles com mais detalhes.

## 2. O LLM como cérebro do agente

O LLM — que podemos considerar como o "cérebro" do agente — atua como o motor de raciocínio no núcleo de todo agente. Na prática, o LLM compreende a intenção do usuário a partir da linguagem natural, planeja os passos necessários para atingir o objetivo, define qual ferramenta deve ser utilizada (e com quais argumentos), interpreta os resultados dessas ferramentas, decide qual será o próximo passo e gera a resposta final para o usuário.

Como se pode notar, o motor de raciocínio — o cérebro do agente — desempenha um papel bastante abrangente. A escolha de um LLM envolve um exercício de equilíbrio (*trade-off*). É preciso ponderar entre capacidade, custo e latência.

Vamos analisar algumas dessas considerações. A primeira é a capacidade de seguir instruções: o modelo deve ser capaz de seguir, de forma confiável, instruções estruturadas. O que seriam essas instruções? Trata-se de *system prompts* (prompts de sistema) que definem o papel do agente, as ferramentas disponíveis e o formato de saída esperado.

É preferível que o modelo possua uma janela de contexto ampla, uma vez que os agentes acumulam contexto rapidamente — cada pensamento, raciocínio, ação e observação é adicionado ao prompt. Portanto, janelas de contexto maiores são, em geral, mais desejáveis.

A capacidade de raciocínio — a qualidade do processo lógico do modelo — impacta diretamente a habilidade do agente de planejar tarefas complexas, compostas por múltiplas etapas. Outro ponto importante diz respeito ao custo: lembre-se de que cada iteração no ciclo de um agente corresponde a uma chamada de API do LLM.

Algumas equipes adotam uma estratégia de dois níveis, utilizando um modelo mais rápido e econômico para decisões simples de roteamento, e um modelo mais robusto para tarefas que exigem um raciocínio complexo. Vale ressaltar também que alguns dos modelos mais recentes, desenvolvidos por empresas como OpenAI e Anthropic, incorporam a técnica de "cadeia de pensamento" (*Chain-of-Thought*) diretamente em seu treinamento.

Isso pode aprimorar o raciocínio do agente, embora resulte em custos mais elevados e maior latência. Em suma, o LLM funciona como o motor ou o núcleo de raciocínio do agente; contudo, a escolha do modelo ideal é uma questão mais complexa do que simplesmente selecionar aquele com a maior pontuação em *benchmarks*.

Trata-se, literalmente, de um exercício de equilíbrio entre capacidade, custo e latência.

## 3. As ferramentas como mãos do agente

O segundo componente fundamental de um agente são as ferramentas. Podemos pensar nelas como as "mãos" do agente; é por meio delas que ele adquire a capacidade de interagir com o mundo real.

Sem ferramentas, um LLM não passa de um gerador de texto; com elas, ele se torna um agente capaz de atuar no mundo real. Mas como funciona, na prática, a chamada de funções (*function calling*) ou de ferramentas (*tool calling*)?

Analisaremos isso com mais detalhes ao longo do curso, mas, por ora, vou listar as etapas: o agente descreve as ferramentas disponíveis na forma de esquemas JSON conceituais e envia essas definições, juntamente com a mensagem do usuário, para o LLM. Assim, o LLM compreende quais ferramentas estão à sua disposição e o que o usuário deseja realizar.

O LLM, basicamente, decide qual será o próximo passo. É como se você enviasse a pergunta e um "conjunto de ferramentas" para o LLM, deixando que ele próprio defina o que fazer a seguir. Nesse momento, o LLM pode optar por responder diretamente ao usuário — caso não precise utilizar nenhuma ferramenta — ou realizar o que chamamos de "chamada de ferramenta estruturada" (*structured tool call*).

Por exemplo, se um usuário solicitar informações sobre o clima ou a temperatura em uma cidade como Paris, o LLM pode gerar uma solicitação estruturada para acionar uma API de meteorologia e obter os dados referentes a essa localidade. É isso que o LLM faz.

Em seguida, após o LLM enviar essa solicitação, o agente a recebe, valida, executa a função correspondente — neste caso, chamando a API de meteorologia — e obtém o resultado. Por fim, o agente envia esse resultado de volta ao LLM na forma de uma "observação", permitindo que o LLM decida, então, como formular a resposta.

## 4. O papel do loop de execução

O terceiro componente central é o *loop*. É nele que tudo se integra: o *loop* executa o ciclo de raciocínio, monitora o estado, gerencia a memória, direciona o uso de ferramentas e aplica regras de segurança.

Uma boa forma de visualizar o *loop* é encará-lo como um sistema operacional para o agente; ele decide se o ciclo deve continuar, ser interrompido, sofrer uma nova tentativa ou ser escalado. É aqui que reside a verdadeira complexidade de engenharia.

Em outras palavras, o *loop* conecta o cérebro e as mãos do agente, transformando um modelo de linguagem em um sistema que consegue agir de forma coordenada, observar os resultados e continuar até atingir o objetivo.

## 5. Conclusão

Os três pilares de um agente de IA — LLM, ferramentas e loop — formam a base da arquitetura agêntica. O LLM fornece raciocínio e interpretação; as ferramentas ampliam a capacidade de ação no mundo real; e o loop orquestra o processo, gerencia o contexto, aplica regras e decide quando parar.

Essa combinação é o que permite que um agente vá além da geração de texto e se torne um sistema capaz de planejar, executar e ajustar sua atuação até alcançar uma meta.
