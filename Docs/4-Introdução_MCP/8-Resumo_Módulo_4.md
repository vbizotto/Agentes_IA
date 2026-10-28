# Resumo do Módulo 4 — Model Context Protocol

## Considerações iniciais

### Visão geral

Neste resumo, vamos recapitular os principais conceitos do módulo sobre MCP: sua função como protocolo de conexão, os componentes que oferece, a descoberta e execução de ferramentas e os cenários em que sua adoção faz sentido.

---

# Recapitulação do módulo

## 1. Um protocolo para conectar agentes e ferramentas

Um único protocolo pode conectar diferentes agentes a diferentes servidores de ferramentas. O MCP funciona como um conector universal, oferecendo uma interface padrão para que aplicações de IA utilizem ferramentas de forma interoperável.

Essa padronização reduz a necessidade de integrações personalizadas e facilita o compartilhamento de ferramentas entre aplicações e frameworks.

## 2. As primitivas do MCP

O MCP define três primitivas principais:

- **Ferramentas:** permitem executar ações.
- **Recursos:** fornecem acesso a dados.
- **Prompts:** ajudam a padronizar instruções reutilizáveis.

Embora o protocolo defina as três primitivas, as ferramentas são as mais usadas para executar ações. Por isso, o MCP também pode ser entendido como uma camada padronizada de ferramentas.

## 3. Arquitetura cliente-servidor

Em vez de chamar funções locais diretamente, os aplicativos se comunicam com ferramentas por meio de um protocolo cliente-servidor. Essa separação torna as ferramentas mais portáteis, escaláveis e fáceis de compartilhar entre equipes.

O servidor MCP executa as ferramentas e retorna resultados estruturados para o cliente. Assim, os aplicativos podem se concentrar na orquestração e na experiência do usuário, sem precisar gerenciar os detalhes de implementação de cada ferramenta.

## 4. Descoberta dinâmica de ferramentas

Com o MCP, os agentes podem descobrir as ferramentas disponíveis em tempo de execução, em vez de depender de definições codificadas diretamente no agente.

Novas ferramentas podem ser adicionadas ao servidor sem exigir alterações no código do agente, o que aumenta a flexibilidade e facilita a manutenção.

## 5. O papel do LLM

O MCP altera a forma como as ferramentas são conectadas, mas não muda a maneira como o modelo de linguagem (LLM) raciocina ou decide usá-las.

Do ponto de vista do LLM, o processo de uso das ferramentas continua semelhante, independentemente de elas serem locais ou acessadas por meio do MCP.

## 6. Quando o MCP é mais adequado

O MCP nem sempre é necessário. Para ferramentas locais simples, chamadas diretas de função podem ser mais fáceis e introduzir menos sobrecarga, como no exemplo matemático do módulo.

O MCP oferece mais valor quando as ferramentas são externas, compartilhadas, reutilizáveis ou gerenciadas por equipes diferentes, como no exemplo prático com um servidor de terceiros.

## 7. Um modelo mental para o MCP

Uma forma útil de pensar no MCP é como uma camada de rede padronizada para ferramentas de IA. Ele desacopla os agentes das implementações das ferramentas e permite interoperabilidade, descoberta e reutilização em escala.

## Conclusão

Ao longo deste módulo, vimos como o MCP padroniza a conexão entre agentes e ferramentas, permite a descoberta dinâmica e mantém separadas a orquestração do agente e a execução no servidor.

Parabéns por concluir este módulo e obrigado pelo seu comprometimento com o aprendizado!
