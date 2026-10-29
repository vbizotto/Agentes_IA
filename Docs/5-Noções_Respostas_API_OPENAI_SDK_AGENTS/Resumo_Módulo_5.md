# Resumo do Módulo 5

## Considerações iniciais

### Visão geral

Neste módulo, conhecemos componentes e padrões usados para criar aplicações com agentes de IA da OpenAI. Vimos como a API de Respostas, o SDK de Agentes, as ferramentas, os sistemas multiagentes e os mecanismos de proteção podem trabalhar em conjunto.

### Objetivos de aprendizagem

Ao concluir este módulo, você será capaz de:

- Explicar o papel da API de Respostas e do SDK de Agentes.
- Entender como ferramentas ampliam as capacidades de um agente.
- Diferenciar padrões de coordenação entre vários agentes.
- Identificar como mecanismos de proteção e rastreamento contribuem para aplicações mais confiáveis.

### Benefícios para você

Compreender esses componentes ajuda a estruturar aplicações de IA com mais clareza: o modelo interpreta e gera respostas, as ferramentas executam tarefas, os agentes coordenam o fluxo, e as proteções e o rastreamento apoiam a segurança e a análise do comportamento.

---

# Principais conceitos

## 1. API de Respostas

A API de Respostas é uma interface para interagir com modelos e combinar respostas, ferramentas e contexto da conversa. Ela permite construir interações em várias etapas, em que o modelo pode continuar o fluxo com base nas informações disponíveis.

## 2. SDK de Agentes

O SDK de Agentes oferece abstrações para definir agentes, instruções, ferramentas e fluxos de execução. Com isso, desenvolvedores podem implementar a lógica da aplicação sem precisar montar manualmente toda a orquestração.

## 3. Ferramentas e chamadas de função

As ferramentas permitem que um agente realize tarefas além de gerar texto, como consultar dados, chamar APIs ou executar cálculos. Uma função Python pode ser disponibilizada como ferramenta para que o agente a selecione quando for apropriado.

## 4. Sistemas multiagentes

Em vez de concentrar todas as responsabilidades em um agente, um sistema pode usar agentes especializados. No padrão de transferência (*handoff*), a solicitação passa para o especialista adequado. No padrão de gerenciador (*manager*), um agente central coordena especialistas e reúne seus resultados.

## 5. Guardrails e rastreamento

Os mecanismos de proteção (*guardrails*) verificam entradas ou saídas de acordo com as regras da aplicação e podem interromper o fluxo quando uma condição de segurança é violada.

O rastreamento registra etapas da execução, como chamadas ao modelo, uso de ferramentas, transferências e verificações de proteção. Essas informações ajudam a depurar o sistema, avaliar seu comportamento e investigar o desempenho.

## 6. Recapitulando

Os componentes estudados cumprem papéis complementares: a API e o SDK apoiam a interação e a orquestração; as ferramentas executam tarefas específicas; os sistemas multiagentes distribuem responsabilidades; e os *guardrails* e o rastreamento apoiam a segurança e a observabilidade.

Em conjunto, esses recursos podem reduzir a complexidade de desenvolvimento e ajudar a criar aplicações de IA mais confiáveis. A escolha de como combiná-los depende das necessidades e dos requisitos de cada projeto.
