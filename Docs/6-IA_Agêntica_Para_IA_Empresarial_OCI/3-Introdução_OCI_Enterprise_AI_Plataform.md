# Introdução à plataforma OCI Enterprise AI

## Considerações iniciais

### Visão geral

Nesta lição, vamos conhecer a plataforma OCI Enterprise AI, voltada à criação, implantação e governança de aplicações de inteligência artificial em escala. A plataforma é apresentada em três camadas: modelos de IA empresarial, serviço de agentes de IA empresarial e governança de IA empresarial.

Como o curso tem foco em agentes, veremos os modelos e a governança em nível introdutório. O serviço de agentes será explorado com mais profundidade nas próximas lições.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Identificar as três camadas principais da plataforma OCI Enterprise AI.
- Diferenciar modelos de chat, incorporação e reclassificação.
- Comparar os modos de serviço sob demanda e clusters de IA dedicados.
- Reconhecer as principais camadas de governança de IA empresarial.

### Benefícios para você

Conhecer a plataforma e seus componentes ajuda a compreender como modelos, agentes e controles de governança se complementam na construção e operação de aplicações de IA empresariais.

---

# Transcrição da aula

Bem-vindos de volta. Nesta lição, vamos analisar a plataforma OCI Enterprise AI, que pode ser usada para criar, implantar e governar aplicações de IA em escala.

## 1. Camadas da plataforma

A plataforma é apresentada em três camadas principais:

1. **Modelos de IA empresarial:** dão acesso a diferentes modelos por meio de uma API consistente. Essa é a camada de inteligência.
2. **Serviço de agentes de IA empresarial:** permite criar, orquestrar e executar cargas de trabalho baseadas em agentes, com ferramentas gerenciadas, protocolos padrão — como MCP e comunicação entre agentes — e frameworks de código aberto. Essa é a camada de ação.
3. **Governança de IA empresarial:** reúne recursos de segurança, conformidade e controle de acesso. Essa é a camada de confiança.

Em conjunto, essas camadas oferecem recursos de inteligência, ação e controle. A disponibilidade de modelos, serviços e recursos depende da configuração e da oferta atual da OCI.

## 2. Tipos de modelos de IA empresarial

A lição apresenta três tipos de modelos: chat, incorporação e reclassificação.

### Modelos de chat

Modelos de chat recebem entradas como perguntas, instruções e conversas e geram respostas em linguagem natural. Por padrão, uma chamada não mantém o estado da conversa por conta própria; recursos como a API OCI Conversations podem ser usados para manter o histórico entre turnos.

Esses modelos também podem oferecer suporte a chamadas de ferramentas, permitindo que o modelo solicite uma função, receba o resultado e o use na resposta. A temperatura é um parâmetro que influencia a variabilidade da geração: valores menores tendem a produzir respostas mais previsíveis, enquanto valores maiores podem gerar respostas mais variadas.

### Modelos de incorporação

Modelos de incorporação transformam conteúdo, como texto, em vetores numéricos. Conteúdos com significados semelhantes tendem a gerar vetores próximos, o que permite comparar semanticamente consultas e documentos.

Em uma busca semântica, a consulta do usuário e os documentos são convertidos em vetores. O sistema recupera documentos cujos vetores são mais próximos do vetor da consulta. A lição cita o Cohere Embed 4 como exemplo de modelo multimodal que pode representar texto e imagens; consulte a oferta atual da OCI para confirmar os modelos disponíveis.

### Modelos de reclassificação

Modelos de reclassificação (*reranking*) ajudam a ordenar documentos recuperados de acordo com sua relevância para uma consulta. Em um fluxo de geração aumentada por recuperação (RAG), uma busca inicial pode retornar vários documentos candidatos; um modelo de reclassificação pode então priorizar os mais relevantes antes que sejam enviados ao modelo de chat.

O fluxo geral descrito na aula é:

1. O modelo de incorporação representa a consulta e os documentos em vetores.
2. A busca recupera documentos candidatos com base na proximidade semântica.
3. O modelo de reclassificação ordena os candidatos por relevância.
4. O modelo de chat usa os documentos selecionados para elaborar a resposta.

A reclassificação pode melhorar a seleção do contexto em determinados fluxos RAG, mas sua necessidade depende dos dados, da busca e dos requisitos da aplicação.

## 3. Modos de serviço dos modelos

O modo de serviço influencia fatores como cobrança, latência, isolamento e suporte a modelos personalizados. A aula compara duas opções.

### Sob demanda

O modo sob demanda é apresentado como uma opção para começar, experimentar e validar uma escolha de modelo, sem assumir previamente horas de cluster. O uso é cobrado com base nas chamadas, conforme as condições do serviço.

Como a infraestrutura é compartilhada, podem existir limites de taxa e variações de disponibilidade. A aula também observa que esse modo pode não estar disponível para determinados modelos personalizados ou importados. Consulte a documentação e as cotas atuais da OCI antes de planejar a implantação.

### Clusters de IA dedicados

Nos clusters de IA dedicados (DAC), a cobrança é baseada no tempo de uso do cluster, e os recursos de GPU são dedicados à instância. A aula apresenta essa opção para cenários que exigem maior previsibilidade de latência, isolamento ou implantação de modelos personalizados.

Como a cobrança pode ocorrer enquanto o cluster está ativo, mesmo sem chamadas de inferência, é importante avaliar o padrão de uso e os custos. As condições, os modelos disponíveis e as garantias dependem da oferta vigente.

### Como escolher

Como orientação geral apresentada na aula, o modo sob demanda pode ser adequado para exploração e prototipagem. Clusters dedicados podem ser considerados quando requisitos de produção, previsibilidade, isolamento ou uso de modelos personalizados justificarem essa escolha.

## 4. Serviço de agentes de IA empresarial

O serviço de agentes de IA empresarial corresponde à camada de ação da plataforma. Ele fornece recursos gerenciados para desenvolvimento, orquestração e execução de agentes.

Como este curso se concentra em aplicações com agentes, o serviço será explorado em mais detalhes na próxima lição.

## 5. Governança de IA empresarial

A governança é apresentada em três camadas, como parte de uma abordagem de defesa em profundidade.

### Segurança de rede

Controla o caminho de rede até os modelos. A aula cita endpoints privados e recursos de comunicação baseados em identidade como exemplos de controles que podem ajudar a limitar o acesso.

### Controle de identidade

O serviço de Gerenciamento de Identidade e Acesso (IAM) permite definir quem pode acessar, usar ou administrar recursos de IA. As políticas podem aplicar permissões a recursos e escopos específicos, conforme a configuração da tenancy.

### Proteções de comportamento

Mecanismos de proteção (*guardrails*) podem verificar entradas e saídas do modelo. A aula cita moderação de conteúdo, detecção de injeção de prompt e identificação de informações pessoais como exemplos de controles de comportamento.

As camadas se complementam: os controles de rede restringem o acesso, o IAM define quais identidades podem usar os recursos e os *guardrails* ajudam a controlar o comportamento da aplicação.

## 6. Recapitulando

Nesta lição, conhecemos as três camadas da plataforma OCI Enterprise AI: modelos de IA empresarial, serviço de agentes de IA empresarial e governança de IA empresarial.

Também vimos os modelos de chat, incorporação e reclassificação; comparamos os modos sob demanda e de clusters dedicados; e exploramos as camadas de governança de rede, identidade e comportamento.

Os recursos e as condições de serviço podem mudar. Consulte a documentação atual da OCI ao escolher modelos, modos de serviço e controles para uma aplicação.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
