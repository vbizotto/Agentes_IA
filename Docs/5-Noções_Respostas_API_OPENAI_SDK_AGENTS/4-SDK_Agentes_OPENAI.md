# SDK de Agentes da OpenAI

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar o SDK de Agentes da OpenAI, um framework Python que ajuda a definir agentes, gerenciar o uso de ferramentas e construir sistemas multiagentes. Como vimos anteriormente, o SDK é construído sobre a API de Respostas.

Vamos conhecer os conceitos centrais do SDK e acompanhar a criação e a execução de um agente simples. O executor coordena o loop do agente: chama o modelo, executa ferramentas quando necessário e repete o processo até que a execução seja concluída.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Identificar os principais conceitos do SDK de Agentes.
- Explicar como o executor gerencia o loop do agente.
- Criar um agente com nome e instruções.
- Executar um agente de forma síncrona ou assíncrona.
- Acessar a saída final produzida pelo agente.

### Benefícios para você

O SDK de Agentes oferece uma estrutura para construir agentes sem precisar implementar manualmente todo o loop de execução. Além disso, inclui recursos para usar ferramentas, transferir o controle entre agentes, validar entradas e saídas e acompanhar a execução.

---

# Transcrição da aula

Bem-vindos de volta. Nesta lição, vamos explorar o SDK de Agentes da OpenAI. Ele é um framework Python que ajuda a definir agentes, gerenciar o uso de ferramentas e construir sistemas multiagentes.

## 1. Conceitos principais

O SDK de Agentes reúne seis conceitos importantes:

- **Agente:** combina um modelo de linguagem (LLM), instruções, ferramentas e um loop de execução.
- **Executor:** executa o agente e gerencia o loop, chamando o modelo, executando ferramentas quando necessário e repetindo o processo até a conclusão.
- **Ferramentas:** funções que o agente pode chamar. Funções Python podem ser disponibilizadas como ferramentas.
- **Handoffs:** mecanismo para transferir o controle de um agente para outro, útil para criar equipes de agentes especializados.
- **Guardrails:** validações de entrada e saída que ajudam a manter os agentes seguros e focados na tarefa.
- **Rastreamento:** recursos de depuração que permitem inspecionar as etapas executadas pelo agente e as ferramentas que ele utilizou.

## 2. Instalação do SDK

Instale o pacote Python do SDK de Agentes com:

```bash
pip install openai-agents
```

Nas próximas lições, vamos explorar ferramentas, handoffs, guardrails e rastreamento com mais detalhes.

## 3. Criando o primeiro agente

O primeiro passo é definir o agente com um nome e instruções. Também é possível especificar o modelo a ser utilizado.

```python
from agents import Agent, Runner

agent = Agent(
    name="Assistente",
    instructions="Responda de forma clara e objetiva.",
)
```

O nome identifica o agente, enquanto as instruções descrevem como ele deve se comportar.

## 4. Executando o agente

Executar o agente inicia o loop de execução. O modelo recebe a entrada e decide se responde diretamente ou se precisa chamar uma ferramenta. Quando uma ferramenta é chamada, o agente recebe o resultado e continua o processo até produzir a resposta final.

Para executar o agente de forma síncrona, use `Runner.run_sync`:

```python
result = Runner.run_sync(agent, "Olá! Apresente-se.")
```

O SDK também oferece a execução assíncrona com `Runner.run`:

```python
import asyncio

async def main():
    result = await Runner.run(agent, "Olá! Apresente-se.")
    print(result.final_output)

asyncio.run(main())
```

## 5. Obtendo a saída

A propriedade `result.final_output` contém a resposta final em texto:

```python
print(result.final_output)
```

Assim, os passos básicos são definir o agente, executá-lo e acessar o resultado. O executor coordena o loop, as chamadas ao modelo e a execução das ferramentas nos bastidores.

## 6. O fluxo de execução

O processo pode ser resumido da seguinte forma:

1. Importar `Agent` e `Runner`.
2. Definir o agente com um nome e instruções.
3. Executar o agente com `Runner.run_sync` ou `Runner.run`.
4. Obter a resposta final por meio de `result.final_output`.

Durante a execução, o executor chama a API de Respostas, sobre a qual o SDK de Agentes é construído. O modelo decide se deve responder diretamente ou chamar uma ferramenta. Se uma ferramenta for chamada, o resultado volta ao agente e o ciclo pode se repetir até que a resposta final seja produzida.

## 7. Recapitulando

Nesta lição, conhecemos os conceitos centrais do SDK de Agentes: agentes, executor, ferramentas, handoffs, guardrails e rastreamento. Também vimos como definir e executar um agente e acessar sua saída final.

O executor é responsável pelo loop do agente: decide quando chamar o modelo, quando executar ferramentas, quando continuar e quando encerrar. Esse mecanismo simplifica a criação de agentes e permite aproveitar recursos mais avançados nas próximas lições.

Espero que esta lição tenha sido útil!
