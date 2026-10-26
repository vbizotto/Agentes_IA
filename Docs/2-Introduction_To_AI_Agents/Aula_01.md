# Aula 01 — Fundamentos de IA Agêntica

## Considerações iniciais

### Visão geral do curso

Neste curso, você explorará os fundamentos da IA agêntica e terá contato prático com a criação de agentes de IA. Você aprenderá conceitos essenciais como arquitetura de agentes, ferramentas, loops, padrões de raciocínio, MCP, LangChain e OpenAI Agents SDK, e aplicará esses conhecimentos em cenários corporativos usando a OCI Enterprise AI Platform e o Oracle AI Database.

Esse material oferece uma base sólida para o desenvolvimento e a implementação de soluções de IA agêntica e ajuda você a se preparar para a certificação gratuita Agentic AI Foundations.

### Objetivos de aprendizagem

Ao concluir esta aula e o curso, você será capaz de:

- Explicar os principais conceitos de agentes de IA, incluindo LLM, ferramentas, loops e padrões de raciocínio.
- Projetar agentes de IA usando LangChain e o OpenAI Agents SDK.
- Implementar os conceitos do Model Context Protocol (MCP) em fluxos de trabalho de agentes.
- Criar agentes usando a OCI Enterprise AI Platform.
- Aplicar os recursos do Oracle AI Database para soluções de IA agêntica.

### Recurso complementar

Para baixar os arquivos de código, use o link abaixo:

https://github.com/oracle-university-labs/ou-generativeai-pro/tree/main/agentic-ai-foundations

### Benefícios para você

Ao final do curso, você terá adquirido habilidades para projetar e construir soluções de IA baseadas em agentes, utilizando tecnologias de código aberto e da Oracle. Você desenvolverá experiência prática com agentes de IA, LangChain, MCP, APIs e SDKs da OpenAI, agentes corporativos da OCI e recursos do Oracle AI Database. Isso o ajudará a transitar de conceitos fundamentais para implementações prontas para o ambiente corporativo.

Essas competências são cada vez mais demandadas pelo mercado e fortalecerão sua capacidade de criar soluções de IA inteligentes, escaláveis e inovadoras para uma ampla variedade de casos de uso.

---

# Transcrição da aula

Bem-vindo(a)! Nesta lição, vamos analisar o que é um agente de IA.

## 1. O que é um agente de IA?

A pergunta mais fundamental é:

> O que exatamente é um agente de IA?

Antes de definir esse conceito, vale compará-lo com elementos que você já conhece:

- Um chatbot responde às suas perguntas.
- Um fluxo de trabalho segue uma sequência fixa e predefinida.
- Um agente de IA faz algo diferente: ele pensa e decide dinamicamente o que fazer em seguida.

Essa é a principal diferença.

Na IA clássica, um agente é qualquer sistema que percebe um ambiente e age sobre ele. Neste curso, focamos em agentes baseados em LLMs (Modelos de Linguagem de Grande Escala).

O modelo mental que queremos seguir é este:

- O LLM é o cérebro.
- As ferramentas são as mãos.
- O loop é o sistema nervoso.

Em outras palavras, um agente de IA baseado em LLM é uma combinação de LLM, ferramentas e um loop de execução.

## 2. Propriedades dos agentes

Os agentes são caracterizados por algumas propriedades importantes:

- São orientados a objetivos e trabalham para atingir uma meta.
- São autônomos e escolhem os próximos passos de forma dinâmica.
- Usam ferramentas, não apenas para gerar texto, mas também para interagir com APIs, bancos de dados, códigos, buscas na web e outras capacidades externas.
- São iterativos e refinam continuamente sua abordagem.

### Analogia útil

Imagine um profissional com mestrado em Direito como um LLM: ele é altamente inteligente, mas está em uma sala sem telefone, computador ou livros de referência, apenas com sua própria memória.

Ele consegue responder perguntas com base no conhecimento que possui, mas não consegue:

- pesquisar informações;
- enviar e-mails;
- verificar previsões do tempo;
- consultar dados externos.

Agora, imagine a mesma pessoa em uma mesa com telefone, computador, livros e uma lista de tarefas. Ela passa a agir no mundo real. Isso é a essência de um agente de IA: capacidade de usar ferramentas para executar ações e alcançar objetivos.

## 3. Agente versus chatbot

A principal diferença entre um chatbot e um agente é que o chatbot recebe uma mensagem, gera uma resposta e para.

Já um agente:

1. recebe um objetivo;
2. divide esse objetivo em etapas;
3. usa ferramentas para coletar informações ou agir;
4. avalia os resultados;
5. continua até alcançar a meta.

### Comparação rápida

| Tipo | Comportamento | Capacidade de ação |
|:---|:---|:---|
| Chatbot / LLM isolado | Responde a um prompt | Gera texto, mas não atua no mundo real |
| Agente de IA | Planeja, executa e ajusta | Interage com ferramentas, dados e sistemas externos |

Ambos são baseados em LLM, mas apenas o agente de IA utiliza um loop de decisão e ação.

## 4. O LLM sozinho não basta

O LLM por si só é apátrida e passivo. Você envia um comando, ele gera texto e termina. Ele não mantém memória entre chamadas, normalmente não executa ações no mundo real e, em muitos casos, não verifica suas próprias respostas.

Um agente, por outro lado, envolve o LLM em um loop de execução. Nesse modelo, o sistema:

- mantém o estado entre múltiplas chamadas ao LLM;
- chama ferramentas para coletar informação ou executar ações;
- se autocorrige observando os resultados das ações;
- decide quando terminou ou quando deve pedir ajuda.

> Um agente de IA não é um modelo novo. É um padrão de arquitetura.

Essa frase é fundamental: você não precisa de um modelo novo para construir um agente. Basta levar um LLM e envolvê-lo em um loop de decisão. Esse loop transforma um respondente passivo em um tomador de decisões ativo.

## 5. O ciclo de execução de um agente

Todo agente opera em um ciclo. Os passos principais são:

1. Percepção: o agente recebe informações ou observações.
2. Raciocínio: decide o que fazer.
3. Ação: chama uma ferramenta ou produz uma resposta.
4. Observação: analisa os resultados e repete o ciclo.

Esse processo é muito semelhante ao comportamento humano. Você não resolve um problema em uma etapa única. Em vez disso, pensa, tenta algo, observa o resultado e ajusta a próxima ação.

O loop termina quando o agente decide que já tem informações suficientes para responder ou quando atinge um limite máximo de iterações, conhecido como limite de segurança.

### Riscos do ciclo

Esse ciclo traz poder, mas também riscos:

- cada iteração pode gerar custo de API;
- aumenta a latência e o tempo de resposta;
- pode ocorrer erro em chamadas de ferramenta;
- pode haver alucinações;
- pode ocorrer um ciclo infinito.

Por isso, a orquestração e os mecanismos de proteção são essenciais. Mais adiante, haverá uma aula dedicada a segurança e proteção de agentes.

## 6. Exemplo prático: reservar um voo

Vamos tornar isso mais concreto com um exemplo.

### Situação

Um usuário diz:

"Quero reservar um voo de Austin para Zurique."

### Fluxo do agente

1. O usuário faz uma pergunta específica.
2. O agente raciocina: "Preciso encontrar voos disponíveis."
3. O sistema consulta a caixa de ferramentas.
4. Existe uma ferramenta chamada "Ferramenta de Voos".
5. O agente executa a ação: chama a ferramenta e envia os parâmetros necessários.
6. A busca considera origem, destino, datas e outros filtros relevantes.
7. A ferramenta retorna três opções com preços diferentes.
8. O agente observa os resultados e decide: "Já tenho as informações. Agora posso responder ao usuário."
9. O agente entrega a resposta final: "Aqui estão os voos disponíveis de Austin para Zurique."

### Ponto-chave

A ideia central é perceber como o raciocínio determina quando consultar uma ferramenta e quando parar.

- Na etapa de raciocínio inicial, o agente conclui que precisa de informação externa.
- Na etapa final, como já possui os resultados, ele decide que não precisa mais acionar ferramentas.

Esse comportamento é o que define um agente: a capacidade de decidir quando usar uma ferramenta e quando finalizar a tarefa.

## 7. Conclusão

O principal conceito desta aula é simples, mas essencial:

- um agente de IA não é um modelo isolado;
- ele é um padrão arquitetural que combina LLM, ferramentas e loop de execução;
- sua principal diferença em relação a um chatbot está na capacidade de observar, decidir, agir e iterar até alcançar um objetivo.

Na próxima aula, veremos os diferentes componentes dos agentes que ajudam nessa tomada de decisão específica.

Esperamos que esta aula tenha sido útil. Obrigado pelo seu tempo.

---

## Resumo rápido

- LLM: cérebro do agente.
- Ferramentas: mãos do agente.
- Loop: sistema nervoso do agente.
- Agente: sistema orientado a objetivo, autônomo e iterativo.
- Diferenciação principal: ação e decisão em vez de resposta estática.



