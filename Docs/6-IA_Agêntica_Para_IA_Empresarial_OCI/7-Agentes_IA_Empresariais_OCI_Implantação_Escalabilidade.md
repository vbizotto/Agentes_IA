# Implantação e escalabilidade de agentes de IA empresariais na OCI

## Considerações iniciais

### Visão geral

Nesta lição, vamos explorar duas formas de criar aplicações com agentes usando o OCI Enterprise AI Agents Service: chamar diretamente a API de Respostas da OCI ou implantar uma aplicação de agente hospedada pela OCI.

Vamos comparar onde cada aplicação é executada, quais responsabilidades ficam com o desenvolvedor e como funciona, em linhas gerais, o processo de empacotamento e implantação de uma aplicação hospedada.

### Objetivos de aprendizagem

Ao concluir esta lição, você será capaz de:

- Diferenciar o uso da API de Respostas da implantação de uma aplicação hospedada.
- Identificar quais componentes são gerenciados pela OCI em cada abordagem.
- Descrever as etapas gerais para empacotar e implantar um agente como contêiner.
- Entender como clientes ou outros agentes acessam uma aplicação implantada.

### Benefícios para você

Conhecer as duas abordagens ajuda a escolher como levar um agente à produção: mantendo a aplicação em uma infraestrutura própria e consumindo as APIs da OCI, ou implantando a aplicação no serviço gerenciado para que a OCI cuide de mais aspectos operacionais.

---

# Transcrição da aula

Bem-vindos de volta. Nesta lição, vamos explorar como usar o OCI Enterprise AI Agents Service para passar de agentes desenvolvidos localmente a aplicações prontas para uso em produção. O serviço oferece duas abordagens principais, que diferem principalmente pelo local onde a aplicação é executada e por quem gerencia sua orquestração.

## 1. Duas abordagens para criar aplicações com agentes

### Usar a API de Respostas da OCI

Nesta abordagem, a aplicação pode ser executada em diferentes ambientes, como um computador, uma máquina virtual, um cluster Kubernetes ou um backend corporativo. O código chama diretamente a API de Respostas da OCI.

A OCI gerencia a infraestrutura de IA, a execução do modelo e os recursos de raciocínio e uso de ferramentas oferecidos pela API. Essa foi a abordagem usada no exemplo em Python da demonstração anterior, que reutilizou um SDK compatível com OpenAI e configurou a URL base para a OCI.

### Implantar uma aplicação hospedada

Nesta segunda abordagem, a OCI hospeda a aplicação completa do agente. Você pode desenvolvê-la com diferentes frameworks, empacotá-la em um contêiner e implantá-la no serviço.

Nesse modelo, a OCI gerencia aspectos da aplicação hospedada, como escalabilidade, rede, autenticação, endpoints e infraestrutura de execução, conforme a configuração do serviço.

Uma forma simples de distinguir as opções é: na primeira, a aplicação consome uma API gerenciada; na segunda, a aplicação do agente é implantada como um serviço hospedado.

## 2. Etapas gerais da implantação hospedada

A aula descreve o processo de implantação nos seguintes passos:

1. **Desenvolver o agente:** criar e testar a aplicação localmente usando um framework de sua preferência, como LangGraph, LangChain ou o SDK de Agentes da OpenAI.
2. **Empacotar a aplicação:** criar uma imagem Docker com o código do agente e suas dependências.
3. **Enviar a imagem:** publicar a imagem no Oracle Cloud Infrastructure Registry (OCIR).
4. **Criar uma aplicação de IA generativa:** configurar o contexto da aplicação e aspectos como escalabilidade, armazenamento, rede e autenticação.
5. **Criar uma implantação:** selecionar a imagem enviada ao OCIR e associá-la à aplicação.
6. **Acessar o agente:** usar o endpoint disponibilizado pelo serviço para que clientes ou outros agentes enviem solicitações.

Os nomes das etapas, os requisitos e as opções de configuração podem variar. Consulte a documentação atual da OCI antes de realizar uma implantação.

## 3. Acesso à aplicação implantada

Após o provisionamento, o serviço fornece um endpoint HTTP para invocar a aplicação. Clientes e, em sistemas multiagentes, outros agentes podem enviar solicitações a esse endpoint, de acordo com as configurações de rede e autenticação.

A demonstração não percorre a implantação completa, pois o processo exige mais etapas. O fluxo é apresentado conceitualmente; outros materiais podem detalhar a configuração de ponta a ponta.

## 4. Como escolher uma abordagem

O uso da API de Respostas pode ser adequado quando você deseja executar a aplicação em sua própria infraestrutura e consumir os recursos de IA gerenciados pela OCI.

A implantação hospedada pode ser considerada quando você deseja que a aplicação do agente também seja executada no ambiente gerenciado da OCI e prefere delegar mais responsabilidades operacionais ao serviço.

A decisão depende dos requisitos de arquitetura, controle, integração e operação do projeto.

## 5. Recapitulando

Nesta lição, comparamos duas formas de criar aplicações com agentes na OCI: consumir a API de Respostas a partir de uma aplicação executada onde você escolher ou implantar a aplicação do agente como um serviço hospedado.

Também vimos as etapas gerais da implantação hospedada: desenvolver o agente, empacotá-lo em um contêiner, enviar a imagem ao OCIR, configurar a aplicação e a implantação e acessar o endpoint fornecido pelo serviço.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
