# Demonstração: servidor MCP em um cenário real

## Considerações iniciais

### Visão geral

Nesta lição, vamos analisar um exemplo de MCP em um cenário real, usando um servidor de terceiros para consultar informações de uso da OCI. Diferentemente do servidor matemático, criado para aprender a mecânica do protocolo, neste exemplo o cliente se conecta a um servidor mantido por outra organização e acessa seus recursos por meio do MCP.

---

# Transcrição da aula

## 1. O MCP em ambientes de produção

O servidor matemático foi útil para aprender porque tínhamos controle sobre o cliente e o servidor. Se algo desse errado, era possível inspecionar os dois lados da conexão e rastrear o problema.

Em produção, porém, o servidor geralmente é fornecido por terceiros, como um fornecedor, um provedor de SaaS ou outra equipe da empresa. Nesse caso, escrevemos o código do cliente, mas não precisamos acessar o código-fonte do servidor nem inserir instruções de depuração nele. A interação acontece por meio do protocolo: consultamos as ferramentas disponíveis e tratamos as respostas e os erros recebidos.

O objetivo do MCP é permitir que os fornecedores disponibilizem suas ferramentas uma vez, para que diferentes aplicações possam usá-las sem criar integrações personalizadas para cada caso.

## 2. O que permanece igual e o que muda

Mesmo quando o servidor é mantido por outra organização, os mecanismos do MCP permanecem os mesmos:

- o cliente se comunica usando JSON-RPC;
- a conexão pode usar entrada e saída padrão (STDIO);
- o cliente lista as ferramentas disponíveis;
- o cliente solicita a execução das ferramentas necessárias.

O que muda é quem mantém o servidor e quais integrações ele encapsula. Em um cenário real, o cliente não implementa diretamente a integração com o serviço externo; ele usa um servidor MCP já publicado.

## 3. Exemplo com OCI

O exemplo desta demonstração usa um servidor MCP para OCI, mantido por terceiros. O cliente se conecta ao servidor, consulta as ferramentas disponíveis e chama a ferramenta apropriada.

O cliente não chama diretamente as APIs REST da OCI. Essa integração é feita pelo servidor MCP, que se comunica com as APIs da OCI por HTTPS. Assim, o cliente interage com o servidor por MCP, enquanto o servidor encapsula o acesso à plataforma.

## 4. Consulta de custos e validação dos resultados

O servidor MCP usado no exemplo encapsula a API de análise de custos que também alimenta a página de faturamento do console da OCI. Essa página permite consultar os custos em diferentes períodos, como o último dia, as últimas 24 horas, os últimos sete dias ou o mês.

Na demonstração, o resultado obtido pelo MCP será comparado ao valor exibido no console. Essa validação ajuda a confirmar que o servidor está funcionando corretamente e que o valor retornado corresponde ao esperado.

O exemplo utiliza uma ferramenta de resumo de uso, que recebe argumentos como o ID do locatário, os horários de início e término e a granularidade da consulta. Embora muitos servidores MCP exponham várias ferramentas, este exemplo se concentra em uma.

## 5. Arquitetura da conexão

A arquitetura pode ser resumida desta forma:

1. O cliente MCP inicia o servidor como um processo local.
2. O cliente e o servidor se comunicam localmente por STDIO.
3. O servidor MCP acessa a API da OCI por HTTPS.
4. O cliente recebe os dados por meio da resposta MCP; ele não acessa a OCI diretamente.

Essa separação é importante: a conexão local entre o cliente e o servidor é diferente da conexão de rede entre o servidor e a API da OCI.

## 6. Executando o servidor com `uvx`

O exemplo usa `uvx`, um utilitário que acompanha o `uv` e executa ferramentas Python sem exigir a instalação prévia do pacote no ambiente do usuário. Ele é semelhante ao `npx` do Node.js.

Ao executar um pacote com `uvx`, os pacotes necessários são baixados para um ambiente isolado e temporário, e o ponto de entrada do pacote é executado. Na primeira execução, o servidor MCP é baixado do PyPI e armazenado em cache; depois, é executado nesse ambiente.

Usar `uvx` evita que os alunos precisem instalar manualmente o servidor com `pip`, gerenciar conflitos entre versões ou configurar um ambiente virtual. O cliente especifica o comando, os argumentos e o ambiente necessários para iniciar o servidor.

## 7. Entendendo o transporte

Embora o servidor seja mantido por um fornecedor externo e acesse um serviço remoto, o processo do servidor MCP é iniciado localmente pelo cliente. Por isso, não há uma conexão HTTPS entre o script do cliente e o servidor MCP: os dois processos se comunicam por pipes locais, usando STDIO.

A conexão HTTPS ocorre entre o processo local do servidor MCP e os servidores em nuvem da OCI. É por essa conexão que o servidor consulta as informações de faturamento. O cliente não se comunica diretamente com a OCI.

Os detalhes de autenticação e segurança dessa conexão não são explorados nesta lição introdutória, mas a distinção entre as duas conexões ajuda a entender o que acontece nos bastidores.

## 8. Recapitulando os pontos principais

- Em produção, o servidor MCP costuma ser fornecido e mantido por terceiros.
- O cliente continua usando o protocolo MCP para descobrir e chamar ferramentas.
- O servidor encapsula a integração com as APIs da OCI.
- `uvx` executa o servidor em um ambiente isolado, sem instalação manual no ambiente do usuário.
- Cliente e servidor MCP se comunicam localmente por STDIO; o servidor acessa a OCI por HTTPS.
- Os resultados podem ser comparados com os valores exibidos no console para validar a consulta.

## Conclusão

Nesta demonstração, vimos como o MCP pode ser usado com um servidor de terceiros para obter dados de faturamento da OCI. O cliente usa o protocolo MCP, enquanto o servidor encapsula a integração com a API externa e faz a conexão HTTPS necessária.

O MCP mostra seu valor quando podemos reutilizar um servidor já disponível, sem precisar escrever sua implementação. Na demonstração, veremos esse código em ação.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
