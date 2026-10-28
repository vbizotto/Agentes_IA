# Demonstração: servidor MCP com cliente LangChain

## Considerações iniciais

### Visão geral

Nesta demonstração, vamos executar o agente LangChain conectado a um servidor MCP de matemática e, em seguida, conectar esse mesmo servidor ao Codex. O objetivo é observar que as ferramentas deixam de estar acopladas a um agente específico e podem ser descobertas e usadas por diferentes hosts compatíveis com MCP.

---

# Transcrição da aula

## 1. O agente conectado ao servidor MCP

O exemplo parte do agente apresentado nos módulos anteriores, agora adaptado para usar a arquitetura MCP. As ferramentas que antes eram definidas localmente com decoradores estão comentadas. A principal mudança no agente é a conexão com o servidor MCP, que permite ao cliente descobrir as ferramentas disponíveis.

O exemplo se conecta ao servidor matemático, mas poderia incluir servidores de outros serviços, como GitHub ou uma API de previsão do tempo. Fora a conexão e a descoberta das ferramentas, a forma de criar, executar, invocar e testar o agente permanece praticamente igual.

## 2. O servidor matemático

O servidor matemático MCP fornece as ferramentas que antes estavam definidas no arquivo do agente. Agora, elas estão disponíveis em um servidor reutilizável.

Ao iniciar o servidor diretamente, pode parecer que nada acontece. No exemplo, ele usa o transporte de entrada e saída padrão (STDIO) e fica aguardando mensagens MCP na entrada padrão. Sem um cliente enviando solicitações, o servidor permanece ocioso.

Esse comportamento é esperado: um host, como o agente LangChain ou o Codex, inicia o servidor como subprocesso e encaminha as solicitações JSON-RPC. A ausência de saída no terminal, por si só, não significa que o servidor esteja com problema.

## 3. Executando o cliente LangChain

Quando o cliente LangChain é executado, ele inicia o servidor como subprocesso e descobre as ferramentas disponíveis. Elas não são mais locais ao agente: são fornecidas pelo servidor MCP.

Na demonstração, o agente executa quatro casos de teste:

- adição;
- multiplicação;
- raiz quadrada;
- cálculo de área.

Também é testado um caso extremo: a divisão de `100` por `0`.

O código do agente praticamente não muda. A diferença principal é o local onde as ferramentas residem: elas saem dos decoradores locais e passam a ser oferecidas por um servidor MCP compartilhável.

## 4. Conectando o mesmo servidor ao Codex

Em seguida, o mesmo servidor matemático é conectado ao Codex, um host de IA diferente do cliente LangChain. A configuração do servidor é feita no arquivo de configuração do Codex.

Pelo comando de barra relacionado ao MCP, é possível consultar o status do servidor e confirmar que o servidor matemático está disponível. O Codex também pode listar as quatro ferramentas descobertas: adição, multiplicação, divisão e raiz quadrada.

Nenhuma alteração é necessária no código do servidor. O novo host aponta para o mesmo servidor MCP e descobre as ferramentas que ele oferece.

## 5. Executando uma ferramenta pelo Codex

Para demonstrar que a chamada é atendida pelo servidor MCP, solicita-se ao Codex que use especificamente a ferramenta de divisão do servidor matemático para calcular `100 ÷ 0`, sem executar comandos do shell nem escrever código.

É importante indicar a ferramenta e o servidor desejados, pois o host também pode ter outros meios de resolver o cálculo. Quando o Codex solicita a execução, ele apresenta uma tela de aprovação com a ferramenta e os argumentos. Após a aprovação, o resultado retorna como erro: não é possível dividir por zero.

Esse é o mesmo texto retornado pela função Python do servidor. Isso confirma que a solicitação foi encaminhada à ferramenta do servidor, em vez de ser respondida apenas pelo raciocínio do modelo.

## 6. Recapitulando os pontos principais

- O agente LangChain descobre e executa ferramentas fornecidas pelo servidor MCP.
- O servidor pode permanecer aguardando solicitações quando é iniciado sem um cliente.
- O mesmo servidor matemático pode ser conectado a diferentes hosts, como LangChain e Codex.
- A implementação das ferramentas não precisa ser alterada para cada host.
- O host pode solicitar aprovação antes de executar uma ferramenta.

## Conclusão

Nesta demonstração, usamos o mesmo servidor matemático MCP primeiro com o cliente LangChain e depois com o Codex, sem modificar o código do servidor. A ideia central é definir as ferramentas uma vez e disponibilizá-las a diferentes aplicações compatíveis com MCP.

Espero que esta demonstração tenha sido útil. Obrigado pelo seu tempo!
