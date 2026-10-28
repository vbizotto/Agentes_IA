# Adicionando um servidor MCP ao agente

## Considerações iniciais

### Visão geral

Nesta lição, vamos adicionar um servidor MCP ao agente matemático criado nos módulos anteriores. Ao comparar a arquitetura antes e depois dessa mudança, veremos como separar as ferramentas do código do agente, configurar a comunicação entre cliente e servidor e reaproveitar as ferramentas em diferentes aplicações.

---

# Transcrição da aula

## 1. Antes do MCP

No exemplo original, o agente é simples: usa um modelo de IA, um loop ReAct e quatro funções matemáticas — adição, multiplicação, divisão e raiz quadrada. As funções são definidas diretamente no arquivo Python do agente, usando o decorador `tool`.

Essa abordagem funciona, mas mantém as ferramentas presas ao programa. Apenas aquele agente pode usá-las; para compartilhá-las com outra aplicação, seria necessário copiar o código. Além disso, qualquer alteração exige atualizar o próprio agente. Não há compartilhamento nem reutilização independente.

## 2. Separando as ferramentas em um servidor MCP

Com o MCP, as ferramentas são separadas em um arquivo de servidor, enquanto o agente mantém apenas a configuração necessária para se conectar a ele. As ferramentas passam a residir independentemente no servidor MCP.

O cliente e o servidor se comunicam pelo protocolo padrão JSON-RPC, usando entrada e saída padrão (STDIO), como vimos na lição anterior.

### Criando ferramentas com FastMCP

O FastMCP é uma estrutura para construir, testar e implantar servidores MCP. Ele facilita transformar funções Python em ferramentas que modelos de IA podem utilizar.

Assim como o decorador `tool` registra ferramentas no agente, o FastMCP permite registrá-las com `mcp.tool`. Um servidor simples realiza três etapas:

1. Cria um servidor MCP, por exemplo, chamado `math`.
2. Registra funções como ferramentas usando o decorador `mcp.tool`.
3. Inicia o servidor para aguardar mensagens JSON-RPC pela entrada e saída padrão.

O FastMCP cuida do protocolo JSON-RPC, sem exigir que as mensagens sejam escritas manualmente. Ele também usa as anotações de tipo das funções para criar o esquema de entrada e a *docstring* para gerar a descrição da ferramenta. Essas informações são retornadas ao cliente durante a descoberta de ferramentas, por meio de `tools/list`.

O servidor não é executado por conta própria nesse exemplo: outro processo, como o agente, precisa iniciá-lo como subprocesso.

## 3. Conectando o agente ao servidor

Como o MCP segue uma arquitetura cliente-servidor, depois de criar o servidor é necessário configurar um cliente. No exemplo, o agente fornece o caminho do servidor e as informações para iniciá-lo localmente.

O caminho pode ser construído a partir de `__file__`, variável especial do Python que indica o caminho do arquivo em execução. Isso permite localizar o servidor sem depender do diretório de onde o agente foi iniciado.

A configuração do cliente inclui:

- um nome legível para identificar a conexão, especialmente útil nos logs quando há vários servidores;
- o comando `python`, que inicia o servidor como um subprocesso;
- o caminho do script do servidor;
- o transporte STDIO, que informa ao cliente como trocar mensagens com o processo filho.

Nesse transporte, o cliente envia mensagens JSON-RPC pela entrada padrão do servidor e lê as respostas pela saída padrão. Não há rede, portas ou HTTP envolvidos. Essa é uma opção simples e rápida, mas exige que o servidor esteja instalado e seja executado na mesma máquina.

## 4. Conectando-se a vários servidores

O exemplo utiliza um cliente MCP multi-servidor. Isso permite adicionar configurações de outros servidores, como GitHub, ao mesmo conjunto.

Mesmo nesse caso, cada conexão continua sendo entre um cliente e um servidor. O cliente multi-servidor gerencia internamente as conexões individuais, uma para cada servidor configurado.

Quando o agente solicita as ferramentas, o cliente se conecta aos servidores configurados, descobre as ferramentas de cada um e pode reuni-las em uma única lista. No exemplo, essa lista contém as quatro ferramentas do servidor matemático.

## 5. Como o fluxo muda com o MCP

Antes do MCP, o fluxo é direto: o modelo solicita uma ferramenta, o código do agente chama uma função Python local, obtém o resultado e o envia de volta ao modelo.

Depois da adoção do MCP, o fluxo passa pelo cliente e pelo servidor:

1. O modelo solicita uma ferramenta.
2. O agente usa o cliente MCP para encaminhar a solicitação ao servidor.
3. O servidor executa a ferramenta e retorna o resultado ao cliente.
4. O cliente devolve o resultado ao agente, que o encaminha ao modelo.

O MCP adiciona uma camada padronizada para a execução de ferramentas. Ele não substitui o modelo nem o loop de raciocínio do agente.

## 6. Responsabilidades do agente e do servidor

Sem o MCP, a aplicação precisa definir os esquemas das ferramentas, registrá-las localmente, associar seus nomes às funções Python, executar as funções e tratar erros.

Com o MCP, parte dessas responsabilidades passa para o servidor e para a estrutura usada para criá-lo. O servidor expõe as ferramentas, fornece seus esquemas e executa as chamadas. O aplicativo do agente pode se concentrar mais na orquestração.

Para o modelo, a origem da ferramenta não muda o fluxo de raciocínio: ele continua recebendo os nomes das ferramentas disponíveis, escolhendo qual chamar, fornecendo os argumentos e recebendo os resultados.

## 7. Benefícios do MCP

Ao manter as ferramentas em um servidor independente, é possível:

- **Reutilizá-las:** diferentes aplicações compatíveis podem descobrir e utilizar o mesmo servidor.
- **Atualizá-las em um só lugar:** uma correção no servidor pode beneficiar todos os agentes conectados.
- **Combinar servidores:** o agente pode se conectar, por exemplo, a servidores de GitHub, Slack e ferramentas matemáticas.
- **Manter o agente organizado:** a lógica das ferramentas fica separada, facilitando testes e manutenção.

Assim, as ferramentas são escritas uma vez e podem ser usadas em diferentes aplicações, sem copiar sua implementação para cada agente.

## 8. Quando usar MCP

Para operações simples, como multiplicação e divisão no exemplo, uma função Python local pode ser mais simples e rápida. O MCP tende a ser mais útil quando as ferramentas são externas ou reutilizáveis, como:

- acesso a serviços e recursos externos;
- consulta a bancos de dados sem incorporar seus drivers ao agente;
- integração com ferramentas de desenvolvimento, como GitHub e Jira;
- comunicação com serviços como Slack e e-mail;
- operações com arquivos em máquinas remotas.

Nesses cenários, a separação entre agente e ferramentas pode simplificar a reutilização e a manutenção.

## Conclusão

Nesta lição, adicionamos um servidor MCP ao agente matemático e vimos como a arquitetura passa de funções locais para uma separação entre cliente e servidor. O agente continua responsável pelo raciocínio e pela orquestração, enquanto o servidor expõe e executa as ferramentas.

Na próxima lição, veremos uma implementação do MCP em uma demonstração passo a passo.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
