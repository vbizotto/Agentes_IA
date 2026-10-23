# Considerações Iniciais

## Fundamentos de IA Agética da Oracle Curso

Neste curso, você explorará os fundamentos da IA ​​agente e obterá experiência prática na criação de agentes de IA. Você aprenderá conceitos essenciais como arquitetura de agentes de IA, ferramentas, loops, padrões de raciocínio, MCP, LangChain e OpenAI Agents SDK, e então aplicará esses conceitos em cenários corporativos usando a OCI Enterprise AI Platform e o Oracle AI Database. Este curso fornece uma base sólida para o desenvolvimento e a implementação de soluções de IA agente e ajuda você a se preparar para a certificação gratuita Agentic AI Foundations.

 Após concluir este curso, você deverá ser capaz de:

 • Explicar os principais conceitos de agentes de IA, incluindo o LLM, ferramentas, loops e padrões de raciocínio.
 • Projetar agentes de IA usando LangChain e o OpenAI Agent Stack.
 • Implementar os conceitos do Model Context Protocol (MCP) em fluxos de trabalho de agentes.
 • Criar agentes usando a OCI Enterprise AI Platform.
 • Aplicar os recursos do Oracle AI Database para soluções de IA agente.

Para baixar os arquivos de código, use este link:  https://github.com/oracle-university-labs/ou-generativeai-pro/tree/main/agentic-ai-foundations

Benefícios para você
Ao final deste curso, você terá adquirido as habilidades necessárias para projetar e construir soluções de IA baseadas em agentes, utilizando tecnologias de código aberto e da Oracle. Você desenvolverá experiência prática com agentes de IA, LangChain, MCP, APIs e SDKs da OpenAI, agentes de IA corporativos da OCI e recursos do Oracle AI Database, o que o ajudará a transitar de conceitos fundamentais para implementações prontas para o ambiente corporativo. Essas habilidades, altamente requisitadas pelo mercado, fortalecerão sua capacidade de criar soluções de IA inteligentes e escaláveis, além de impulsionar a inovação em uma ampla gama de casos de uso de IA. 

# Transcrição do video  

Bem-vindo (a). Nesta lição, vamos analisar o que é um agente de IA . 

Comecemos pela pergunta mais fundamental : 
  - O que exatamente é um agente de IA ?
    . Antes de defini - lo , vamos compará - lo com coisas que você já conhece.
      - Um chatbot responde às suas perguntas.
      - Um fluxo de trabalho segue uma sequência fixa predefinida
      - Mas um agente de IA faz algo muito diferente.
        Ele pensa e decide o que fazer em seguida de forma dinâmica. Essa é a principal diferença.

Na IA clássica , um agente é qualquer sistema que percebe um ambiente e age nele . Neste curso, focamos em agentes baseados em LLM ( Modelo de Aprendizagem Baseado em LLM ) . Portanto, o modelo mental que quero que vocês sigam é o seguinte : um agente de IA baseado em LLM é uma combinação de LLM, ferramentas e um loop. Vamos detalhar isso. O LLM é o cérebro. Ele entende e raciocina. As ferramentas são as mãos. Elas podem agir no mundo real . E o loop é o sistema nervoso que mantém o processo em andamento.

Agora, vamos analisar as propriedades dos agentes . Os agentes são orientados a objetivos e trabalham para atingir uma meta. São autônomos e escolhem os próximos passos dinamicamente. Também utilizam ferramentas , não apenas gerando texto , mas interagindo com APIs, bancos de dados, execução de código , buscas na web , etc. Além disso , são iterativos , refinando constantemente sua abordagem .

Uma boa analogia seria a seguinte : imagine um profissional com mestrado em Direito (LLM) como uma pessoa muito inteligente sentada em uma sala sem telefone, computador ou livros, apenas com o próprio cérebro. Ele consegue responder perguntas de memória, mas não consegue pesquisar nada , enviar e -mails, verificar a previsão do tempo, etc. Um agente é a mesma pessoa, mas agora tem uma mesa com telefone , computador , livros de referência e uma lista de tarefas . Ele consegue, de fato, fazer coisas .

A principal diferença entre um chatbot e um agente é que o chatbot recebe sua mensagem, gera uma resposta e para. Já um agente recebe seu objetivo, divide -o em etapas, usa ferramentas para coletar informações ou tomar ações, avalia os resultados e continua até que o objetivo seja alcançado. A seguir, uma tabela que compara chatbots ou LLMs independentes com um agente de IA . Ambos são baseados em LLM, mas são agentes de IA .

Agora, o LLM por si só é apátrida e passivo. Você envia um comando , ele gera o texto e pronto . Ele não mantém memória entre chamadas, não pode executar ações no mundo real e , na maioria das vezes, não consegue verificar suas próprias respostas. Um agente, por outro lado , envolve o LLM em um loop de execução . Ele mantém o estado entre múltiplas chamadas do LLM . Pode chamar ferramentas para coletar informações ou executar ações . Pode se autocorrigir observando os resultados de suas ações. E decide quando terminou ou quando pedir ajuda .

O que eu quero que vocês entendam é que um agente de IA não é um modelo novo . É um padrão de arquitetura . Deixe - me repetir isso porque é crucial. Você não precisa de um modelo novo para construir um agente. Você pega um LLM e o envolve em um loop de decisão . Esse loop é o que o transforma de um respondente passivo em um tomador de decisões ativo .

Agora, vamos entender o núcleo de um agente, o que chamamos de ciclo de execução . Todo agente opera nesse ciclo . O primeiro passo é o que chamamos de percepção , que consiste em receber informações ou observações . O segundo passo é o raciocínio, que é simplesmente decidir o que fazer .

Aqui , o LLM, que é um componente da arquitetura do agente , seleciona a próxima etapa. Ele pode usar raciocínio implícito . A próxima etapa é a ação, onde o agente aciona uma ferramenta ou resposta. E a etapa seguinte é a observação, onde o agente analisa os resultados e repete todo o ciclo novamente .

Agora, se você pensar bem , isso é extremamente semelhante à forma como os humanos funcionam. Você não resolve um problema em uma única etapa. Você pensa , tenta algo, observa o resultado e ajusta . E é exatamente isso que esse loop permite . O loop termina quando o agente decide que tem informações suficientes para fornecer uma resposta final ou quando um número máximo de iterações é atingido, o que chamamos de limite de segurança .

Esse ciclo é o que dá poder aos agentes e também traz consigo certos riscos. Cada iteração custa dinheiro porque, ao final dela, há chamadas à API do LLM . Isso leva tempo , o que aumenta a latência e pode dar errado , o que chamamos de chamadas de ferramentas alucinadas ou até mesmo ciclos infinitos . É por isso que a orquestração e os mecanismos de proteção são tão importantes. E, ao final deste módulo , teremos uma aula dedicada a mecanismos de proteção e segurança.

Agora, vamos tornar isso prático com um exemplo. Digamos que você tenha um usuário que diga : " Quero reservar um voo de Austin para Zurique " . Essa é a consulta do usuário . Agora, vamos observar o loop . O primeiro passo é o usuário fazer uma pergunta específica : ele quer reservar um voo de Austin para Zurique. Então, o agente raciocina e diz : " Preciso encontrar voos disponíveis " . E ele tem uma caixa de ferramentas. E como parte dessa caixa de ferramentas, ele tem uma ferramenta de voos .

Então , o sistema sabe que existe uma ferramenta chamada " Ferramenta de Voos ", que pode buscar essas informações. O agente executa uma ação: chama a Ferramenta de Voos e envia os parâmetros. A busca é feita com base no destino , na origem, no ponto de partida e em uma data específica ou em um conjunto de datas específicas . Em seguida , o agente observa os resultados retornados pela ferramenta . A Ferramenta de Voos retorna três opções com preços diferentes .

Então o agente raciocina novamente. Ele pensa: " Ah , eu consultei a ferramenta. Tenho os resultados. Devo apresentar as opções claramente ao usuário ." Então o agente raciocina mais uma vez. E então o agente retorna a resposta final . Ele diz: " Aqui estão os voos disponíveis de Austin para Zurique . " A ideia principal aqui é observar como o raciocínio determina quando consultar uma ferramenta e quando parar .

Então, na etapa dois , o agente estava raciocinando e o resultado foi acionar a ferramenta, porque ele descobriu que precisava obter essa informação. Na etapa 5, o agente raciocina novamente. Mas, neste ponto , como já possui os resultados, ele diz : " Terminei . Não preciso acionar mais ferramentas . Devo apresentar as opções ou as respostas claramente ao usuário . " E informa : " Estes são os três voos com preços diferentes . "

A ideia principal é que o agente decide quando usar uma ferramenta ou quando parar . Essa tomada de decisão é o que o define como um agente . Na próxima aula , veremos os diferentes componentes dos agentes que os auxiliam nessa tomada de decisão específica . Espero que esta aula tenha sido útil . Obrigado pelo seu tempo .


