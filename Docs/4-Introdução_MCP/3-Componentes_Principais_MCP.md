# Componentes principais do MCP

## Considerações iniciais

### Visão geral

Nesta lição, vamos conhecer os componentes principais do MCP: ferramentas, recursos e prompts. Também vamos explorar o ciclo de vida de uma conexão MCP, o formato de mensagens JSON-RPC 2.0 e os mecanismos de transporte usados por servidores locais e remotos.

---

# Transcrição da aula

## 1. Primitivas do MCP

Os servidores MCP expõem três tipos de primitivas:

- **Ferramentas:** ações que o modelo pode executar, como funções que realizam uma tarefa.
- **Recursos:** fontes de dados que o modelo pode consultar sem causar efeitos colaterais.
- **Prompts:** modelos que estruturam interações e podem ser usados como atalhos na interface.

Uma forma simples de lembrar a diferença é pensar em ferramentas como ações, recursos como leituras e prompts como estruturas. Por exemplo, um comando de barra, como `/review`, pode carregar um prompt predefinido sem que o usuário precise digitar todo o seu conteúdo.

Embora o MCP ofereça as três primitivas, as ferramentas costumam ser o foco quando se fala sobre o protocolo.

## 2. Ciclo de vida de uma conexão MCP

O MCP segue uma arquitetura cliente-servidor. O ciclo de vida de uma conexão tem quatro fases:

1. **Inicialização:** o cliente envia uma solicitação com a versão do protocolo e os recursos que suporta. O servidor responde com sua própria versão e seus recursos. Em seguida, o cliente informa que está pronto para trocar mensagens.
2. **Descoberta:** o cliente consulta o servidor para saber quais ferramentas, recursos ou prompts estão disponíveis. O servidor responde com as descrições e os esquemas correspondentes.
3. **Operação:** o cliente recebe as solicitações do usuário e as encaminha ao modelo junto com as ferramentas disponíveis. Quando o modelo escolhe uma ferramenta, o cliente solicita sua execução ao servidor e devolve o resultado ao modelo.
4. **Encerramento:** quando a interação termina, o cliente fecha a conexão de transporte.

## 3. Comunicação com JSON-RPC 2.0

As mensagens do MCP usam o formato `JSON-RPC 2.0`, que organiza a comunicação em solicitações e respostas. Diferentemente do REST, projetado principalmente para requisições de cliente para servidor, o JSON-RPC também permite comunicação bidirecional.

Uma mensagem pode incluir a chave `jsonrpc`, um identificador (`id`), o nome do método e seus parâmetros. A resposta contém um resultado ou um erro. Por exemplo, o cliente pode usar `tools/call` para pedir ao servidor que execute uma ferramenta de multiplicação. O servidor executa a operação e retorna o resultado — por exemplo, `15 × 8 = 120`.

Na prática, frameworks como FastMCP e LangChain cuidam da criação dessas mensagens. Ainda assim, conhecer sua estrutura ajuda a entender e depurar a comunicação.

## 4. Descoberta de ferramentas

O método `tools/list` solicita ao servidor a lista de ferramentas disponíveis e seus respectivos esquemas, incluindo nomes, descrições e parâmetros de entrada. Em geral, essa consulta acontece quando o cliente se conecta.

Por exemplo, o servidor pode informar que oferece ferramentas de multiplicação, adição, divisão e raiz quadrada. Assim, o cliente descobre dinamicamente o que está disponível, sem que as ferramentas precisem ser definidas diretamente no código da aplicação.

## 5. Chamada de ferramentas

O método `tools/call` é usado quando o modelo decide executar uma ferramenta:

1. O modelo escolhe a ferramenta e define seus argumentos.
2. O cliente envia a solicitação ao servidor.
3. O servidor executa a ferramenta e retorna o resultado.
4. O cliente encaminha o resultado de volta ao modelo.

Por exemplo, o modelo pode solicitar a ferramenta de multiplicação com os valores `15` e `8`. O servidor calcula o resultado e o devolve ao cliente, que o retorna ao modelo.

Em resumo, `tools/list` permite descobrir as ferramentas disponíveis, enquanto `tools/call` solicita a execução de uma ferramenta específica.

## 6. Mecanismos de transporte

O JSON-RPC define o formato das mensagens, mas não exige um mecanismo de transporte específico. Por isso, o MCP pode usar diferentes transportes sem alterar o formato das mensagens.

### Transporte padrão de entrada e saída

O transporte de entrada e saída padrão (STDIO) é indicado para servidores locais. O aplicativo host inicia o servidor MCP como um processo filho na mesma máquina, e a comunicação acontece pela entrada padrão (`stdin`) e pela saída padrão (`stdout`).

Essa opção evita a sobrecarga de rede e é simples e rápida. Em contrapartida, o servidor precisa ser instalado e executado localmente.

### Transporte HTTP em fluxo

O transporte HTTP em fluxo (*Streamable HTTP*) é indicado para servidores remotos. O cliente envia mensagens por meio de requisições HTTP `POST`, e o servidor pode transmitir respostas usando eventos enviados pelo servidor (SSE).

Esse transporte permite implantações em nuvem, conexões de vários clientes e o uso de mecanismos padrão de autenticação HTTP. Um transporte anterior, baseado apenas em SSE, foi substituído pelo *Streamable HTTP*.

Independentemente do transporte escolhido, as mensagens continuam usando JSON-RPC 2.0. Assim, o formato do protocolo permanece consistente tanto em conexões locais quanto remotas.

## 7. Recapitulando os pontos principais

- O MCP oferece três primitivas: ferramentas, recursos e prompts.
- O ciclo de vida de uma conexão tem quatro fases: inicialização, descoberta, operação e encerramento.
- O JSON-RPC 2.0 define o formato das mensagens.
- `tools/list` lista as ferramentas disponíveis; `tools/call` solicita a execução de uma ferramenta.
- O MCP pode usar STDIO para servidores locais e *Streamable HTTP* para servidores remotos.

## Conclusão

Nesta lição, analisamos as primitivas do MCP, o ciclo de vida de uma conexão, a comunicação com JSON-RPC 2.0 e os mecanismos de transporte para servidores locais e remotos.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
