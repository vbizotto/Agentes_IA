# Guia prático do MCP

## Considerações iniciais

### Visão geral

Nesta lição, vamos analisar um exemplo prático de MCP em um cenário real. O servidor matemático foi útil para aprender a mecânica do protocolo, mas a utilização real do MCP normalmente acontece em um ambiente em que o servidor é fornecido por terceiros, como uma empresa, um provedor de SaaS ou outra equipe interna.

Nesse contexto, o cliente normalmente apenas conecta e usa as ferramentas disponíveis. O objetivo é permitir que provedores exponham suas ferramentas uma vez e que diferentes aplicações consigam reutilizá-las sem implementar integrações personalizadas.

---

# Transcrição da aula

## 1. O que muda em produção

No exemplo matemático, nós escrevemos tanto o servidor quanto o cliente. Isso foi ideal para aprender o funcionamento do protocolo, porque tínhamos controle total sobre as duas extremidades da conexão.

Na prática, porém, o uso real do MCP quase nunca é assim. Em produção, o servidor costuma ser fornecido por terceiros. Por exemplo, ele pode ser mantido pela Oracle, por uma plataforma de software como serviço ou por outra equipe da empresa.

Quando isso acontece, o cliente escreve apenas o código que se conecta ao servidor. Não é necessário ler o código-fonte do servidor nem acrescentar instruções de depuração internas. O trabalho se concentra na comunicação por meio do protocolo, na listagem das ferramentas e no tratamento dos erros retornados.

Esse é o cenário em que o MCP de fato passa a justificar seu investimento.

## 2. O padrão de uso no mundo real

Esse exemplo mostra o padrão mais comum em ambientes reais. No lado direito da arquitetura, o servidor continua sendo escrito por outra pessoa. O cliente apenas se conecta ao servidor, pergunta quais ferramentas ele expõe e usa as que precisa.

Neste caso, a empresa ou o fornecedor disponibiliza um servidor MCP compatível com OCI. O cliente não precisa conhecer os detalhes de implementação da infraestrutura de origem. Ele apenas descobre o que está disponível e chama a ferramenta apropriada.

Uma observação importante: o cliente nunca chama diretamente as APIs REST da OCI. A chamada é feita pelo servidor MCP, que encapsula a integração com a plataforma. O cliente acessa o recurso por meio do protocolo MCP.

## 3. O que permanece igual

Mesmo em um cenário com servidor de terceiros, a parte fundamental do MCP continua igual:

- o cliente segue usando a comunicação baseada em JSON-RPC;
- a conexão pode ocorrer via STDIO;
- o cliente usa `tools/list` para descobrir as ferramentas;
- o cliente usa `tools/call` para executar uma ferramenta específica;
- o protocolo continua sendo o mesmo, independentemente de quem escreveu o servidor.

Esses são os mecanismos subjacentes do MCP, e eles não mudam apenas porque o servidor foi entregue por outra pessoa.

## 4. O que muda

O que muda é o responsável pelo servidor e o que ele encapsula.

Em exemplos reais, alguém cria e mantém o servidor. O cliente apenas usa esse recurso. Isso muda a forma como o agente interage com o ambiente externo: em vez de implementar integrações próprias, ele passa a descobrir e consumir ferramentas padronizadas.

O cliente não precisa se preocupar com o código da implementação do servidor. Ele só precisa saber como listar e invocar as ferramentas que o servidor oferece.

## 5. Exemplo com OCI e PyPI

O exemplo prático desta lição usa um servidor MCP com suporte a OCI. Em outras palavras, o servidor encapsula a API de custos da Oracle e expõe uma ferramenta para consultar o uso de recursos.

Esse servidor é publicado no PyPI, que é o índice oficial de pacotes Python de terceiros. Em vez de implementarmos a integração manualmente, usamos um pacote já disponibilizado pela Oracle ou pela comunidade.

O servidor encapsula a mesma lógica que alimenta a página de faturamento do console da OCI. Ele permite consultar valores do último dia, últimas 24 horas, últimos sete dias, mês atual e outros intervalos.

Isso é relevante porque, em um ambiente real, o cliente pode validar o resultado comparando o valor retornado pelo MCP com o valor mostrado no console da plataforma. A superfície de integração é pequena e a lógica de negócio está encapsulada no servidor.

## 6. Arquitetura do exemplo real

A arquitetura do exemplo é a seguinte:

1. O cliente MCP inicia um servidor MCP local.
2. O servidor MCP chama a API da OCI por meio de HTTPS.
3. O cliente nunca acessa a OCI diretamente.
4. O cliente lista e chama ferramentas por meio do protocolo MCP.

Esse padrão é muito importante porque separa a camada de protocolo da camada de integração com o sistema externo.

### O papel do UVX

Uma parte do exemplo usa `uvx`, um utilitário que acompanha o `uv` e executa ferramentas Python sem instalar o pacote previamente no ambiente local.

O `uvx` funciona como o equivalente em Python do `npx` do Node.js. Quando você executa um comando com `uvx`, ele baixa o pacote para um ambiente temporário, cria um ambiente isolado e executa o ponto de entrada do pacote.

Isso é útil porque o cliente não precisa instalar o servidor MCP da Oracle manualmente com `pip`, nem lidar com conflitos de dependências. O `uvx` cuida disso para você.

O que acontece na prática é: o cliente usa `uvx` para iniciar o servidor MCP, o servidor se instala em um ambiente temporário e passa a comunicar-se com o cliente por meio de STDIO. A comunicação entre cliente e servidor local ocorre por entrada e saída padrão.

É importante notar que, apesar de o servidor ter origem remota e ser mantido por um provedor externo, a comunicação entre o cliente e esse servidor, em execução localmente, acontece por pipes locais e não por uma conexão direta com a OCI.

Por outro lado, a conexão HTTPS acontece entre o servidor MCP e a API da OCI, não entre o cliente e a plataforma. O cliente nunca se comunica diretamente com a infraestrutura externa.

## 7. O valor do MCP em cenários reais

Essa lição mostra onde o MCP realmente agrega valor: quando você não precisa escrever o servidor e quer reutilizar uma ferramenta já pronta por outra equipe ou fornecedor.

Ao invés de construir integrações customizadas para cada aplicação, você se conecta a um servidor MCP padrão, lista as ferramentas disponíveis e usa aquilo que precisa.

Isso reduz a necessidade de código específico, melhora a reutilização e facilita a interoperabilidade entre aplicações e ferramentas.

## Conclusão

Nesta lição, vimos que o MCP ganha muito mais valor quando o servidor é fornecido por terceiros. O cliente continua usando o mesmo protocolo e os mesmos métodos básicos — listagem e chamada de ferramentas —, mas agora a lógica de integração fica encapsulada no servidor.

O que muda não é o protocolo, e sim a origem e a responsabilidade do servidor. A principal vantagem é que você pode consumir um recurso padronizado sem implementar uma nova integração para cada aplicação.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!