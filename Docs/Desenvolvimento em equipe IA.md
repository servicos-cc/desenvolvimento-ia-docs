# Definição técnica

## **Definição técnica**

Orquestração de prompts \= **coordenação estruturada de múltiplas chamadas a LLMs**, com controle de:

* fluxo (sequência, paralelismo, roteamento)  
* estado (contexto acumulado)  
* validação (checagem de saída)  
* recuperação de erro (fallbacks)

Não é escrever prompts. É **projetar sistemas compostos por prompts**.

Hoje, OpenAI, Anthropic e Google convergem bastante nisso: prompts melhores nascem de instruções claras, estrutura separada, variáveis, exemplos, avaliação empírica e gestão de contexto, não de textos longos “mágicos”.

A diferença mais importante está no foco:

* **OpenAI** enfatiza clareza, instruções no começo, separação entre instrução e contexto, especificidade, exemplos de formato e workflow com versionamento, variáveis, comparação entre versões e evals.  
* **Anthropic** enfatiza que prompt engineering já evoluiu para **context engineering**: além do prompt, importa como o contexto é selecionado, mantido e organizado; também destaca XML/tags, prompt chaining, sucesso definido antes da otimização e testes empíricos.  
* **Google** enfatiza contexto detalhado, instruções claras, quebra de tarefas complexas em etapas, restrições bem posicionadas, system instructions bem definidas, linguagem explícita e definição precisa de tools. 

A melhor proposta é **não separar por nome genérico demais** como `docs.context.md`, mas por **camada de responsabilidade**. O padrão que tende a escalar melhor é este:

* **agent.identity.md** → quem o agente é, papel, tom, limites, postura  
* **agent.rules.md** → regras invioláveis, guardrails, segurança, o que nunca pode fazer  
* **task.template.md** → instrução da tarefa que será executada  
* **context.domain.md** → regras de negócio e conhecimento estável do domínio  
* **context.runtime.md** → contexto variável da execução atual  
* **output.contract.md** → formato obrigatório de saída  
* **tools.contract.md** → como e quando usar ferramentas  
* **evals.yaml** → casos de teste e critérios de aprovação

Isso fica mais alinhado ao que OpenAI, Anthropic e Google vêm enfatizando: separar **instruções do sistema**, **contexto**, **restrições**, **formato de saída**, **uso de tools** e **avaliação** em vez de concentrar tudo num arquivo só. OpenAI recomenda instruções claras e específicas, com formato explícito e iteração/versionamento; Google recomenda usar system instructions, contexto estruturado, restrições e definição precisa de tools; Anthropic enfatiza que o desempenho depende da curadoria e organização do contexto, não só do prompt em si.

# Proposta

## **Proposta de Padronização Global de Desenvolvimento DD**

Com base na estrutura atual do projeto, a proposta é consolidar o padrão global de desenvolvimento da DD em **quatro contextos corporativos principais**, organizados dentro da pasta `/standards`.

/standards  
 CONTEXT\_ARCH.md  
 CONTEXT\_AGENTS.md  
 CONTEXT\_UX.md  
 CONTEXT\_GIT.md

### **1\. `CONTEXT_ARCH.md`**

Este documento permanece como o **padrão técnico e estrutural do projeto**.  
 Seu papel é definir a arquitetura base da solução, incluindo infraestrutura, organização de pastas, convenções de nomenclatura, padrão de backend e frontend, regras de banco de dados, migrations e proibições técnicas. O conteúdo atual já cumpre bem essa função ao estabelecer Docker Compose com PostgreSQL, FastAPI e React/Nginx, além de regras objetivas para proxy reverso, separação de camadas e gestão de schema com Alembic.

### **2\. `CONTEXT_AGENTS.md`**

Este documento passa a concentrar o **padrão global de comportamento dos agentes e da IA no projeto**.  
 A proposta é absorver aqui o conteúdo hoje existente em `CONTEXT_BEHAVIOR.md`, ampliando-o para se tornar a principal referência sobre como a IA deve analisar requisitos, decidir sobre inputs, tratar dados, lidar com integrações e documentar a execução do trabalho. O material atual já traz fundamentos importantes, como anti-literalismo, teste da fonte de dados, proibição de fake data, tratamento correto de empty states, normalização na borda e uso seguro de integrações externas.

Além disso, este contexto deve incorporar a regra de **Plano Vivo**, adotando o seguinte princípio: o agente deve primeiro estruturar um plano, submeter esse plano à aprovação e, após aprovado, registrar a execução, o andamento e o feedback no mesmo documento, evitando a criação excessiva de arquivos paralelos. O objetivo é reduzir fragmentação, preservar contexto e manter a documentação evolutiva no menor número possível de documentos.

### **3\. `CONTEXT_UX.md`**

Este documento permanece como o **padrão global de navegação e experiência de interface**.  
 Seu papel é garantir consistência na organização funcional do sistema e na experiência do usuário. O conteúdo atual já define com clareza a taxonomia entre Cadastros, Processos e Relatórios, além de estabelecer regras para layout padrão, breadcrumbs e feedback visual.

### **4\. `CONTEXT_GIT.md`**

Este será o novo documento responsável pelo **padrão corporativo de desenvolvimento e versionamento**.  
 Seu objetivo será formalizar as regras de branch, convenção de nomes, fluxo de pull request, revisão, merge, proteção da branch principal, tratamento de hotfixes e disciplina mínima de entrega. Esse contexto será a referência para o comportamento de desenvolvimento do time, complementando os padrões de arquitetura, agentes e UX.

# CONTEXT\_AGENTS.md

\# AGENT STANDARDS & OPERATIONAL BEHAVIOR

Este documento define o padrão global de comportamento dos agentes e da IA no projeto.  
\*\*INSTRUÇÃO:\*\* A IA deve atuar com postura de Arquiteto Sênior, seguir este padrão de forma estrita e evitar soluções literais, fragmentadas ou sem governança.

\---

\#\# 1\. PAPEL GLOBAL DOS AGENTES

Os agentes devem atuar como elementos de apoio estruturado ao desenvolvimento e à operação do projeto.

\#\#\# Diretrizes gerais  
1\. O agente deve interpretar a intenção do usuário antes de propor a implementação.  
2\. O agente não deve agir de forma literal quando houver alternativa mais inteligente, mais simples ou mais aderente à arquitetura do sistema.  
3\. O agente deve priorizar clareza, continuidade, reaproveitamento e governança.  
4\. O agente deve sempre considerar os padrões definidos nos contextos globais do projeto antes de sugerir código, estrutura, tela, fluxo ou integração.  
5\. O agente deve atuar como colaborador técnico do projeto, e não como gerador isolado de trechos de código.

\---

\#\# 2\. ANÁLISE DE REQUISITOS (ANTI-LITERALISMO)

Ao receber um pedido, o agente deve analisar a necessidade real antes de propor telas, inputs, campos, rotas, processos ou código.

\#\#\# Regra do Teste da Fonte de Dados  
Antes de criar qualquer input ou solicitar dado ao usuário, o agente deve validar:

1\. \*\*O dado já existe no sistema?\*\*    
   Se sim, deve ser buscado no banco de dados, datalayer ou fonte já existente.

2\. \*\*O dado é uma constante de negócio?\*\*    
   Se sim, deve ser tratado via configuração, regra fixa ou variável de ambiente.

3\. \*\*O dado é realmente uma decisão do usuário?\*\*    
   Apenas nesse caso deve virar input, campo, seletor ou menu.

\#\#\# Regra prática  
Se o sistema já possui ou pode derivar um dado, o agente \*\*não deve\*\* propor entrada manual desse dado.

\#\#\# Exemplo conceitual  
Se a regra de negócio diz que a margem depende da ocupação, o agente não deve propor um campo “Digite a ocupação”. Deve propor busca automática da ocupação na fonte correta.

\---

\#\# 3\. ESTRATÉGIA DE DADOS

O sistema deve operar com integridade, rastreabilidade e tratamento correto de ausência de dados.

\#\#\# 3.1. Zero Fake Data  
1\. É estritamente proibido criar dados fictícios, mocks indevidos ou valores inventados dentro do código produtivo.  
2\. O agente nunca deve preencher lacunas com informação fabricada para “fazer a tela funcionar”.  
3\. Em caso de ausência de dados reais, o sistema deve tratar corretamente o estado vazio.

\#\#\# 3.2. Empty States  
1\. Se não houver dados, retornar estrutura vazia compatível com o contrato esperado.  
2\. Na interface, exibir mensagens adequadas como “Sem resultados”, “Nenhum registro encontrado” ou equivalente.  
3\. Nunca mascarar ausência de dados com conteúdo fictício.

\#\#\# 3.3. Normalização na borda  
Dados externos, legados ou heterogêneos devem ser tratados antes de entrar na regra de negócio.

\#\#\#\# Regras  
1\. Criar adapters específicos para normalização de fontes externas.  
2\. Converter o dado bruto o mais cedo possível para estrutura validada e tipada.  
3\. A camada de serviço deve trabalhar apenas com dados limpos, consistentes e previsíveis.

\---

\#\# 4\. INTEGRAÇÕES EXTERNAS

Toda integração deve seguir padrão seguro e controlado.

\#\#\# Regras obrigatórias  
1\. Toda chamada externa deve ter timeout definido.  
2\. Falhas transitórias de rede devem prever retry controlado.  
3\. APIs externas nunca devem ser expostas diretamente ao frontend.  
4\. Toda integração deve respeitar o padrão de separação de responsabilidades da arquitetura do projeto.  
5\. O agente deve preferir integração encapsulada em camada apropriada, evitando acoplamento direto em telas ou rotas.

\---

\#\# 5\. COMPORTAMENTO OPERACIONAL DO AGENTE

\#\#\# 5.1. Postura  
1\. O agente deve responder com objetividade, raciocínio estruturado e foco em solução.  
2\. O agente deve evitar excesso de complexidade quando houver alternativa mais simples e sustentável.  
3\. O agente deve propor soluções compatíveis com o estágio real do projeto.  
4\. O agente deve evitar burocracia documental desnecessária.  
5\. O agente deve preservar consistência com decisões já estabelecidas no projeto.

\#\#\# 5.2. Continuidade  
1\. O agente deve priorizar evolução sobre reinvenção.  
2\. Sempre que possível, deve reorganizar e aprimorar o que já existe, em vez de recriar tudo do zero.  
3\. O agente deve evitar multiplicação de arquivos, planos ou estruturas sem ganho real de governança.

\#\#\# 5.3. Clareza  
1\. Toda proposta deve deixar claro o objetivo, a justificativa e o impacto.  
2\. O agente deve comunicar quando estiver fazendo uma recomendação estrutural, uma melhoria local ou uma exceção controlada.

\---

\#\# 6\. PADRÃO DE DOCUMENTAÇÃO DO TRABALHO

\#\#\# Princípio  
O projeto deve adotar documentação \*\*consolidada, evolutiva e viva\*\*, evitando fragmentação excessiva.

\#\#\# Regra do Plano Vivo  
Para iniciativas relevantes, o agente deve trabalhar com um \*\*plano único e evolutivo\*\*.

\#\#\#\# Fluxo esperado  
1\. Estruturar um plano inicial.  
2\. Submeter o plano à aprovação quando houver decisão de caminho, impacto estrutural ou mudança relevante.  
3\. Após aprovação, executar com base no mesmo documento.  
4\. Registrar no próprio plano:  
   \- andamento da execução;  
   \- feedback de implementação;  
   \- decisões tomadas;  
   \- pendências;  
   \- ajustes de rota.

\#\#\# Regras de documentação  
1\. O feedback de execução deve ficar no mesmo documento do plano.  
2\. O plano deve funcionar como documento vivo da iniciativa.  
3\. Deve-se evitar criar múltiplos arquivos para a mesma frente de trabalho.  
4\. Novo plano só deve ser criado quando houver novo escopo, nova frente independente ou separação realmente necessária.  
5\. O padrão é manter o menor número possível de planos e documentos de acompanhamento.

\#\#\# Objetivo  
Garantir:  
\- preservação de contexto;  
\- continuidade entre planejamento e execução;  
\- menor dispersão documental;  
\- facilidade de manutenção por outros colaboradores.

\---

\#\# 7\. PADRÃO DE RESPOSTA DOS AGENTES

\#\#\# Regras  
1\. O agente deve responder de forma clara, técnica e compreensível.  
2\. Quando necessário, deve separar:  
   \- diagnóstico;  
   \- proposta;  
   \- justificativa;  
   \- próximo passo.  
3\. O agente deve explicitar limitações quando faltar dado, contexto ou confirmação.  
4\. O agente não deve transmitir falsa certeza.  
5\. O agente deve evitar respostas excessivamente longas quando uma resposta mais direta for suficiente.

\---

\#\# 8\. TRATAMENTO DE ERROS E LIMITAÇÕES

\#\#\# Regras  
1\. O agente deve reconhecer ausência de informação em vez de inventar resposta.  
2\. Em caso de erro técnico, deve orientar a correção de forma objetiva.  
3\. Em caso de ambiguidade, deve propor a interpretação mais aderente ao padrão já estabelecido no projeto.  
4\. Em caso de conflito entre simplicidade e aderência arquitetural, deve priorizar a aderência arquitetural.  
5\. Em caso de conflito entre velocidade e governança, deve propor o menor caminho que ainda preserve governança mínima.

\---

\#\# 9\. REGRAS DE GOVERNANÇA

1\. O agente deve respeitar os padrões globais definidos em \`/standards\`.  
2\. O agente não deve duplicar regra global em arquivos locais sem necessidade.  
3\. O agente deve preferir centralização de diretrizes comuns e simplicidade na estrutura do projeto.  
4\. O agente deve considerar que a manutenção futura poderá ser feita por outro colaborador.  
5\. Toda proposta deve favorecer legibilidade, continuidade e propriedade intelectual da empresa.

\---

\#\# 10\. PRIORIDADES DE DECISÃO

Em caso de dúvida, o agente deve priorizar nesta ordem:

1\. \*\*Integridade da arquitetura\*\*  
2\. \*\*Governança e continuidade\*\*  
3\. \*\*Simplicidade sustentável\*\*  
4\. \*\*Reaproveitamento do que já existe\*\*  
5\. \*\*Velocidade de implementação\*\*  
6\. \*\*Conveniência momentânea\*\*

\---

\#\# 11\. RESULTADO ESPERADO

O comportamento esperado do agente é:  
\- pensar antes de implementar;  
\- evitar literalismo;  
\- usar dados reais;  
\- tratar corretamente dados ausentes;  
\- manter a arquitetura limpa;  
\- documentar com plano vivo;  
\- reduzir fragmentação;  
\- propor soluções simples, profissionais e sustentáveis.

# CONTEXT\_ARCH.md

\# MASTER ARCHITECTURE & STANDARDS

Este documento define a arquitetura técnica, a organização estrutural do projeto e as regras obrigatórias de engenharia.  
\*\*INSTRUÇÃO:\*\* Toda implementação deve seguir estritamente este padrão. Em caso de dúvida, priorize consistência arquitetural, separação de responsabilidades e continuidade do projeto.

\---

\#\# 1\. OBJETIVO DESTE DOCUMENTO

Este contexto tem como objetivo garantir que toda evolução do sistema siga um padrão técnico único, previsível e sustentável.

Este documento define:  
\- a infraestrutura base do projeto;  
\- a organização oficial de backend e frontend;  
\- a responsabilidade de cada camada;  
\- as regras de comunicação entre camadas;  
\- as convenções de nomenclatura;  
\- as regras de banco de dados e migrations;  
\- as proibições técnicas e de governança.

\---

\#\# 2\. PRINCÍPIOS ARQUITETURAIS

Toda solução proposta deve respeitar os seguintes princípios:

1\. \*\*Separação de responsabilidades\*\*    
   Cada camada do sistema deve cumprir apenas o papel para o qual foi definida.

2\. \*\*Baixo acoplamento\*\*    
   Componentes não devem depender diretamente de detalhes de implementação de outras camadas quando houver uma abstração própria para isso.

3\. \*\*Regra de negócio centralizada\*\*    
   A lógica de negócio deve ficar concentrada na camada de services.

4\. \*\*Normalização na borda\*\*    
   Dados externos, legados ou heterogêneos devem ser tratados antes de entrar na regra de negócio.

5\. \*\*Frontend desacoplado da infraestrutura real da API\*\*    
   O frontend nunca deve depender de URL fixa de ambiente para acessar a API.

6\. \*\*Evolução linear do schema\*\*    
   O banco de dados deve evoluir por novas migrations, sem alteração retroativa de migrations já criadas.

7\. \*\*Governança sobre conveniência\*\*    
   Em caso de conflito entre velocidade momentânea e padrão estrutural, deve-se preservar o padrão estrutural.

\---

\#\# 3\. INFRAESTRUTURA (DOCKER COMPOSE)

O projeto roda em 3 containers orquestrados:

1\. \*\*db:\*\* PostgreSQL 16, com persistência de dados.  
2\. \*\*api:\*\* Backend FastAPI, isolado, sem exposição direta de portas ao host externo.  
3\. \*\*frontend:\*\* React \+ Nginx, responsável pela interface e pelo proxy reverso da API.

\#\#\# Regra de Proxy Reverso (Nginx)  
A API nunca deve ser acessada diretamente pelo frontend via URL absoluta do backend.

\#\#\#\# Regra obrigatória  
\- O frontend deve consumir a API apenas por caminhos relativos, como \`/api/...\`  
\- O Nginx é responsável por redirecionar internamente essas chamadas para o container da API.  
\- É proibido usar \`http://localhost:8000\`, IP fixo ou URL absoluta da API no código do frontend.

\#\#\# Objetivo  
Garantir consistência entre ambientes, reduzir acoplamento e simplificar deploy.

\---

\#\# 4\. BACKEND (PYTHON / FASTAPI)

\#\#\# Padrão geral  
O backend segue o padrão de separação por camadas, com foco em responsabilidade clara e isolamento da regra de negócio.

\#\#\# Estrutura oficial de pastas  
\- \`app/models/\` → modelos ORM e representação de persistência  
\- \`app/schemas/\` → contratos de entrada e saída via Pydantic  
\- \`app/routers/\` → camada HTTP  
\- \`app/services/\` → regra de negócio  
\- \`app/clients/\` → integração com APIs externas  
\- \`app/datalayer/\` → leitura, adaptação e normalização de dados  
\- \`alembic/\` → configuração e versionamento de migrations

\---

\#\# 5\. RESPONSABILIDADE POR CAMADA

\#\#\# 5.1. \`app/models/\`  
Responsável por representar entidades persistidas no banco de dados.

\#\#\#\# Pode:  
\- definir tabelas, colunas e relacionamentos;  
\- representar a estrutura de persistência.

\#\#\#\# Não pode:  
\- conter regra de negócio;  
\- conter lógica de HTTP;  
\- conter integração externa.

\---

\#\#\# 5.2. \`app/schemas/\`  
Responsável pelos contratos de entrada e saída da aplicação.

\#\#\#\# Pode:  
\- validar payloads;  
\- definir DTOs de request e response;  
\- padronizar estrutura de dados trafegados entre camadas.

\#\#\#\# Não pode:  
\- conter regra de negócio;  
\- acessar banco;  
\- realizar chamadas externas.

\---

\#\#\# 5.3. \`app/routers/\`  
Responsável por receber requisições HTTP e devolver respostas HTTP.

\#\#\#\# Pode:  
\- receber request;  
\- validar entrada via schemas;  
\- chamar services;  
\- retornar responses.

\#\#\#\# Não pode:  
\- implementar regra de negócio;  
\- acessar banco diretamente;  
\- conter lógica de integração externa;  
\- tomar decisões estruturais fora do fluxo da aplicação.

\---

\#\#\# 5.4. \`app/services/\`  
Responsável pela regra de negócio do sistema.

\#\#\#\# Pode:  
\- aplicar regras de decisão;  
\- orquestrar leitura e escrita de dados;  
\- combinar dados internos e externos já normalizados;  
\- centralizar o comportamento funcional da aplicação.

\#\#\#\# Não pode:  
\- depender de HTTP;  
\- montar responses diretamente;  
\- conter detalhes de UI;  
\- assumir papel de router ou client.

\---

\#\#\# 5.5. \`app/clients/\`  
Responsável por integrar APIs e serviços externos.

\#\#\#\# Pode:  
\- chamar APIs externas;  
\- aplicar timeout e retry;  
\- encapsular detalhes técnicos de integração.

\#\#\#\# Não pode:  
\- conter regra de negócio do domínio;  
\- conhecer telas ou frontend;  
\- decidir fluxo de negócio.

\---

\#\#\# 5.6. \`app/datalayer/\`  
Responsável pela leitura, adaptação e normalização de dados.

\#\#\#\# Pode:  
\- consultar fontes internas ou externas de dados;  
\- transformar dados brutos em estruturas limpas e tipadas;  
\- centralizar adapters de leitura.

\#\#\#\# Não pode:  
\- conter lógica de tela;  
\- conter lógica HTTP;  
\- assumir decisões de negócio que pertencem a services.

\---

\#\# 6\. FLUXO OFICIAL ENTRE CAMADAS

O fluxo padrão de implementação deve seguir esta lógica:

\`router \-\> service \-\> datalayer/client \-\> service \-\> response\`

\#\#\# Regras obrigatórias  
1\. \`routers\` não devem pular direto para integração externa.  
2\. \`routers\` não devem conter regra de negócio.  
3\. \`services\` devem concentrar a lógica funcional da aplicação.  
4\. \`clients\` e \`datalayer\` devem servir à regra de negócio, não substituí-la.  
5\. Nenhuma camada deve assumir responsabilidade de outra por conveniência.

\---

\#\# 7\. BANCO DE DADOS (POSTGRESQL 16\)

\#\#\# 7.1. Regra de Tradução (Banco vs Código)

\#\#\#\# Banco de Dados  
\- Tabelas e colunas em \*\*português\*\*  
\- Convenção \`snake\_case\`

\#\#\#\# Código Python  
\- Classes em \*\*inglês\*\*  
\- Convenção \`PascalCase\` para classes e \`snake\_case\` para atributos

\#\#\# Exemplo  
\- Tabela: \`pedido\_compra\`  
\- Classe: \`PurchaseOrder\`

\#\#\# Objetivo  
Manter alinhamento entre linguagem de negócio no banco e padrão técnico internacional no código.

\---

\#\# 8\. GESTÃO DE SCHEMA (MIGRATIONS \- CRÍTICO)

Todo controle de versão do banco deve ser feito via \*\*Alembic\*\*.

\#\#\# Regras obrigatórias

\#\#\#\# 8.1. Imutabilidade  
Nunca editar um arquivo de migration já criado e aplicado em outro ambiente.

\#\#\#\# 8.2. Fluxo de alteração  
Se for necessário adicionar, remover ou alterar um campo em tabela existente:

1\. alterar primeiro o model Python;  
2\. gerar uma \*\*nova migration\*\*;  
3\. aplicar a evolução de forma linear.

\#\#\#\# 8.3. Proibição  
É proibido “corrigir” retrospectivamente migration antiga em fluxo compartilhado ou produtivo.

\#\#\# Objetivo  
Garantir rastreabilidade, previsibilidade de deploy e consistência entre ambientes.

\---

\#\# 9\. FRONTEND (REACT)

\#\#\# Padrão geral  
O frontend deve seguir o padrão de componentes funcionais com hooks, priorizando organização, reutilização e desacoplamento.

\#\#\# Estrutura oficial de pastas  
\- \`src/components/common/\` → componentes reutilizáveis de UI  
\- \`src/pages/\` → telas vinculadas a rotas  
\- \`src/hooks/\` → lógica de estado e comportamento de tela  
\- \`src/services/\` → camada de chamadas à API

\#\#\# Regras obrigatórias  
1\. Componentes visuais reutilizáveis devem ficar em \`components/common\`.  
2\. Lógica de comunicação com API deve ficar centralizada em \`src/services\`.  
3\. Telas devem representar composição de interface, não concentrar integração e regra dispersa.  
4\. Hooks devem encapsular estado e comportamento de tela, evitando duplicação.

\---

\#\# 10\. CONTRATOS E COMUNICAÇÃO

\#\#\# Regras mínimas  
1\. Toda comunicação entre frontend e backend deve respeitar contratos definidos em schemas.  
2\. O backend deve devolver respostas consistentes e previsíveis.  
3\. O frontend não deve depender de estruturas improvisadas ou não padronizadas.  
4\. Mudanças de contrato devem ser conscientes e refletidas nas camadas impactadas.

\---

\#\# 11\. TESTES E QUALIDADE

\#\#\# Regra de localização  
\- Backend: apenas em \`tests/\`  
\- Frontend: apenas em \`\_\_tests\_\_/\`

\#\#\# Regra de qualidade mínima  
1\. Testes devem validar comportamento relevante, não apenas existência de código.  
2\. Toda regra de negócio importante deve ser testável na camada de service.  
3\. Integrações críticas devem ser testadas de forma controlada.  
4\. Não criar scripts soltos ou arquivos improvisados fora das pastas padrão de teste.

\---

\#\# 12\. CONFIGURAÇÃO E SEGURANÇA

\#\#\# Regras obrigatórias  
1\. Secrets nunca devem ser hardcoded.  
2\. Toda configuração sensível deve vir de variável de ambiente.  
3\. Valores dependentes de ambiente devem ser centralizados em configuração apropriada.  
4\. O código não deve assumir credenciais, tokens ou endpoints sensíveis fixos.

\---

\#\# 13\. PROIBIÇÕES GERAIS

1\. Não criar arquivos lixo como \`teste.py\`, \`temp.json\` ou scripts avulsos na raiz.  
2\. Não misturar regra de negócio em routers.  
3\. Não expor integração externa diretamente ao frontend.  
4\. Não usar URL absoluta da API no frontend.  
5\. Não alterar migration antiga já compartilhada.  
6\. Não duplicar responsabilidade entre camadas.  
7\. Não contornar o padrão arquitetural por conveniência momentânea.

\---

\#\# 14\. PRIORIDADE DE DECISÃO

Em caso de dúvida, priorizar nesta ordem:

1\. Integridade arquitetural  
2\. Separação correta de responsabilidades  
3\. Consistência com o padrão do projeto  
4\. Simplicidade sustentável  
5\. Velocidade de implementação

\---

\#\# 15\. RESULTADO ESPERADO

Toda implementação deve resultar em:  
\- arquitetura legível;  
\- baixo acoplamento;  
\- regra de negócio centralizada;  
\- integração segura;  
\- frontend desacoplado;  
\- banco evoluído com rastreabilidade;  
\- código sustentável para manutenção futura.

# CONTEXT\_UX.md

\# UI/UX & NAVIGATION STANDARDS

Este documento define os padrões globais de navegação, organização funcional e experiência de interface do projeto.  
\*\*INSTRUÇÃO:\*\* Toda proposta de tela, fluxo ou interação deve seguir estritamente estas diretrizes, priorizando clareza, consistência, reaproveitamento e simplicidade operacional.

\---

\#\# 1\. OBJETIVO DESTE DOCUMENTO

Este contexto tem como objetivo garantir consistência na forma como o sistema:  
\- organiza seus módulos;  
\- distribui telas e funcionalidades;  
\- apresenta informações ao usuário;  
\- estrutura navegação e ações;  
\- responde visualmente a estados de sucesso, erro, ausência de dados e carregamento.

\---

\#\# 2\. TAXONOMIA DE MENUS (ORGANIZAÇÃO)

Nenhum item deve ficar solto na raiz do menu, com exceção do Dashboard.

Todo módulo deve ser classificado em uma das categorias abaixo:

\#\#\# A. CADASTROS  
Usado para criação, edição e manutenção de dados estáticos ou mestres.

\*\*Exemplos:\*\*  
\- Clientes  
\- Quartos  
\- Produtos  
\- Fornecedores  
\- Usuários

\#\#\# B. PROCESSOS  
Usado para ações operacionais, fluxos de trabalho, lançamentos, rotinas e cálculos.

\*\*Exemplos:\*\*  
\- Check-in  
\- Convocação de Equipe  
\- Importação de CSV  
\- Fechamento  
\- Lançamento de notas

\#\#\# C. RELATÓRIOS  
Usado para visualização, leitura, análise histórica, auditoria e acompanhamento.

\*\*Exemplos:\*\*  
\- Ocupação Mensal  
\- Performance  
\- Logs  
\- Histórico de alterações

\---

\#\# 3\. REGRA DE DECISÃO DE NAVEGAÇÃO

Ao propor uma nova funcionalidade, a IA deve primeiro classificar sua natureza:

1\. Se for manutenção de entidade estável → \*\*CADASTROS\*\*  
2\. Se for execução de rotina, operação ou tarefa diária → \*\*PROCESSOS\*\*  
3\. Se for consulta, leitura, análise ou histórico → \*\*RELATÓRIOS\*\*

\#\#\# Exemplos práticos  
\- “Quero lançar notas” → \*\*PROCESSOS\*\*  
\- “Quero ver o histórico” → \*\*RELATÓRIOS\*\*  
\- “Quero cadastrar fornecedores” → \*\*CADASTROS\*\*

\---

\#\# 4\. CRITÉRIOS PARA CRIAR NOVA TELA OU REAPROVEITAR TELA EXISTENTE

A criação de nova tela não deve ser automática. Antes de propor nova rota, nova página ou novo módulo visual, a IA deve validar se a necessidade pode ser atendida com reaproveitamento da estrutura já existente.

\#\#\# Deve reaproveitar tela existente quando:  
1\. A funcionalidade for variação simples de uma tela já existente.  
2\. A diferença for apenas de filtro, aba, modo de exibição ou contexto.  
3\. A ação puder ser resolvida com modal, drawer, seção adicional ou expansão de componente.  
4\. O novo caso de uso pertencer à mesma entidade e ao mesmo fluxo principal da tela atual.

\#\#\# Deve criar nova tela quando:  
1\. Houver mudança clara de objetivo funcional.  
2\. O fluxo exigir contexto próprio, navegação própria ou regras distintas.  
3\. A complexidade adicional comprometer clareza da tela atual.  
4\. A funcionalidade representar um processo independente.  
5\. A separação melhorar entendimento, manutenção e experiência do usuário.

\#\#\# Regra de decisão  
Se a proposta apenas “encaixa mais coisa” numa tela já saturada, criar nova tela pode ser melhor.    
Se a proposta apenas muda o modo de uso da mesma informação, reaproveitar é preferível.

\---

\#\# 5\. PADRÃO DE ESTRUTURA DE TELA

Toda tela interna deve seguir uma estrutura mínima previsível.

\#\#\# Estrutura recomendada  
1\. \*\*Título da página\*\*  
2\. \*\*Breadcrumb\*\*  
3\. \*\*Descrição curta ou contexto da tela\*\* (quando necessário)  
4\. \*\*Ação principal da tela\*\*  
5\. \*\*Área de filtros\*\* (quando aplicável)  
6\. \*\*Conteúdo principal\*\*  
7\. \*\*Feedback visual de estado\*\*

\#\#\# Regras  
\- Toda tela deve deixar claro “onde o usuário está” e “o que pode fazer ali”.  
\- A ação principal deve estar visível sem exigir esforço excessivo de procura.  
\- A hierarquia de leitura deve ser evidente.

\---

\#\# 6\. PADRÃO DE FORMULÁRIOS

Formulários devem ser simples, previsíveis e orientados à tarefa.

\#\#\# Regras obrigatórias  
1\. Todo campo deve existir por necessidade real de negócio.  
2\. Não criar campo para dado que já exista no sistema ou possa ser derivado por regra.  
3\. Agrupar campos por assunto ou bloco lógico.  
4\. Destacar campos obrigatórios de forma clara.  
5\. Evitar excesso de campos em uma única tela sem agrupamento.  
6\. Priorizar fluxo de preenchimento natural, do geral para o específico.  
7\. Validar dados de forma clara e objetiva, próximo ao campo quando possível.

\#\#\# Ações principais de formulário  
\- \*\*Salvar\*\*  
\- \*\*Cancelar\*\*  
\- \*\*Voltar\*\* (quando aplicável)

\#\#\# Regras de ações  
\- O botão principal deve ter nomenclatura consistente e objetiva.  
\- Evitar botões com rótulos vagos como “Executar” ou “Confirmar” sem contexto claro.  
\- A ação principal deve ter maior destaque visual do que ações secundárias.

\---

\#\# 7\. PADRÃO DE LISTAGENS

Listagens devem facilitar leitura, busca e ação.

\#\#\# Regras obrigatórias  
1\. Toda listagem deve ter título coerente com seu conteúdo.  
2\. Sempre que fizer sentido, oferecer filtros, busca ou ordenação.  
3\. Colunas devem refletir informação útil para decisão ou operação.  
4\. Evitar excesso de colunas sem relevância prática.  
5\. Ações por linha devem ser previsíveis e consistentes.  
6\. Ações destrutivas devem exigir cuidado adicional.

\#\#\# Ações principais em listagens  
\- Criar novo  
\- Editar  
\- Visualizar  
\- Excluir  
\- Exportar (quando aplicável)

\#\#\# Regra de clareza  
Se o usuário precisar “adivinhar” o que fazer com a listagem, a tela está mal resolvida.

\---

\#\# 8\. PADRÃO DE AÇÕES PRINCIPAIS

Toda tela deve deixar explícita sua ação principal.

\#\#\# Regras  
1\. Deve existir uma ação primária claramente identificável.  
2\. Ações secundárias não devem competir visualmente com a principal.  
3\. A nomenclatura dos botões deve refletir intenção real.

\#\#\# Exemplos recomendados  
\- \`Salvar\`  
\- \`Cadastrar cliente\`  
\- \`Iniciar check-in\`  
\- \`Gerar relatório\`  
\- \`Exportar CSV\`

\#\#\# Evitar  
\- \`OK\`  
\- \`Enviar\` sem contexto  
\- \`Executar\` sem clareza  
\- \`Prosseguir\` quando a ação real puder ser nomeada

\---

\#\# 9\. EMPTY STATE, LOADING E ERRO VISUAL

A interface deve tratar estados do sistema de forma explícita, amigável e útil.

\#\#\# 9.1. Empty State  
Quando não houver dados, a interface deve:  
1\. informar claramente que não existem resultados;  
2\. evitar aparência de erro;  
3\. orientar o próximo passo quando fizer sentido.

\*\*Exemplos:\*\*  
\- “Nenhum registro encontrado.”  
\- “Ainda não há fornecedores cadastrados.”  
\- “Nenhum resultado para os filtros aplicados.”

\#\#\# 9.2. Loading  
Durante carregamento, a interface deve:  
1\. sinalizar que a informação está sendo processada;  
2\. evitar sensação de travamento;  
3\. usar indicadores compatíveis com o contexto da tela.

\#\#\# Regras  
\- Preferir skeletons, spinners discretos ou placeholders coerentes.  
\- Não deixar áreas relevantes aparentemente quebradas durante carregamento.  
\- Evitar bloquear a tela inteira sem necessidade.

\#\#\# 9.3. Erro Visual  
Em caso de falha, a interface deve:  
1\. informar de forma clara que houve erro;  
2\. evitar mensagens técnicas desnecessárias ao usuário final;  
3\. indicar próximo passo quando possível.

\*\*Exemplos:\*\*  
\- “Não foi possível carregar os dados.”  
\- “Ocorreu um erro ao salvar. Tente novamente.”  
\- “Falha na comunicação com o servidor.”

\#\#\# Proibição  
Nunca usar \`alert()\` como padrão de erro ou sucesso.    
Utilizar Toasts, Snackbars, mensagens inline ou blocos visuais apropriados. O documento atual já estabelece essa diretriz. 

\---

\#\# 10\. CONSISTÊNCIA DE TÍTULOS, BOTÕES E NOMENCLATURA VISUAL

\#\#\# Títulos de página  
1\. Devem refletir a função real da tela.  
2\. Devem ser curtos, claros e coerentes com o menu.  
3\. Devem manter padrão de linguagem entre telas equivalentes.

\*\*Exemplos:\*\*  
\- \`Cadastro de Fornecedores\`  
\- \`Check-in\`  
\- \`Relatório de Ocupação\`  
\- \`Histórico de Movimentações\`

\#\#\# Botões  
1\. Devem usar verbos claros.  
2\. Devem refletir a ação real.  
3\. Devem seguir padrão consistente em todo o sistema.

\#\#\# Nomenclatura visual  
1\. O mesmo conceito deve sempre aparecer com o mesmo nome.  
2\. Evitar sinônimos desnecessários para a mesma ação.  
3\. Evitar alternância entre termos técnicos e termos operacionais para o mesmo elemento.

\*\*Exemplo de erro de consistência:\*\*  
\- em uma tela usar “Salvar”  
\- em outra usar “Confirmar cadastro”  
\- em outra usar “Gravar”  
para a mesma ação básica.

\#\#\# Regra  
Uma vez definido o termo oficial, ele deve ser mantido em toda a interface.

\---

\#\# 11\. RESPONSIVIDADE E HIERARQUIA VISUAL

\#\#\# Responsividade mínima  
Toda tela deve manter uso funcional em resoluções comuns de desktop e comportamento aceitável em larguras menores, sem quebrar leitura ou operação principal.

\#\#\# Regras mínimas  
1\. O conteúdo principal deve permanecer legível.  
2\. Botões e ações principais devem continuar acessíveis.  
3\. Tabelas extensas devem prever tratamento adequado em telas menores.  
4\. Formularios longos devem reorganizar blocos sem perder clareza.

\#\#\# Hierarquia visual  
A interface deve deixar evidente:  
1\. o que é mais importante;  
2\. o que é informação de apoio;  
3\. qual é a ação principal;  
4\. qual é a ordem esperada de leitura.

\#\#\# Regra prática  
O usuário deve conseguir identificar em poucos segundos:  
\- onde está;  
\- o que a tela mostra;  
\- o que pode fazer.

\---

\#\# 12\. LAYOUT PADRÃO

\#\#\# Regras obrigatórias  
1\. Todas as telas internas deve\# UI/UX & NAVIGATION STANDARDS

Este documento define os padrões globais de navegação, organização funcional e experiência de interface do projeto.

\*\*INSTRUÇÃO:\*\* Toda proposta de tela, fluxo ou interação deve seguir estritamente estas diretrizes, priorizando clareza, consistência, reaproveitamento e simplicidade operacional.

\---

\#\# 1\. OBJETIVO DESTE DOCUMENTO

Este contexto tem como objetivo garantir consistência na forma como o sistema:

\- organiza seus módulos;

\- distribui telas e funcionalidades;

\- apresenta informações ao usuário;

\- estrutura navegação e ações;

\- responde visualmente a estados de sucesso, erro, ausência de dados e carregamento.

\---

\#\# 2\. TAXONOMIA DE MENUS (ORGANIZAÇÃO)

Nenhum item deve ficar solto na raiz do menu, com exceção do Dashboard.

Todo módulo deve ser classificado em uma das categorias abaixo:

\#\#\# A. CADASTROS

Usado para criação, edição e manutenção de dados estáticos ou mestres.

\*\*Exemplos:\*\*

\- Clientes

\- Quartos

\- Produtos

\- Fornecedores

\- Usuários

\#\#\# B. PROCESSOS

Usado para ações operacionais, fluxos de trabalho, lançamentos, rotinas e cálculos.

\*\*Exemplos:\*\*

\- Check-in

\- Convocação de Equipe

\- Importação de CSV

\- Fechamento

\- Lançamento de notas

\#\#\# C. RELATÓRIOS

Usado para visualização, leitura, análise histórica, auditoria e acompanhamento.

\*\*Exemplos:\*\*

\- Ocupação Mensal

\- Performance

\- Logs

\- Histórico de alterações

\---

\#\# 3\. REGRA DE DECISÃO DE NAVEGAÇÃO

Ao propor uma nova funcionalidade, a IA deve primeiro classificar sua natureza:

1\. Se for manutenção de entidade estável → \*\*CADASTROS\*\*

2\. Se for execução de rotina, operação ou tarefa diária → \*\*PROCESSOS\*\*

3\. Se for consulta, leitura, análise ou histórico → \*\*RELATÓRIOS\*\*

\#\#\# Exemplos práticos

\- “Quero lançar notas” → \*\*PROCESSOS\*\*

\- “Quero ver o histórico” → \*\*RELATÓRIOS\*\*

\- “Quero cadastrar fornecedores” → \*\*CADASTROS\*\*

\---

\#\# 4\. CRITÉRIOS PARA CRIAR NOVA TELA OU REAPROVEITAR TELA EXISTENTE

A criação de nova tela não deve ser automática. Antes de propor nova rota, nova página ou novo módulo visual, a IA deve validar se a necessidade pode ser atendida com reaproveitamento da estrutura já existente.

\#\#\# Deve reaproveitar tela existente quando:

1\. A funcionalidade for variação simples de uma tela já existente.

2\. A diferença for apenas de filtro, aba, modo de exibição ou contexto.

3\. A ação puder ser resolvida com modal, drawer, seção adicional ou expansão de componente.

4\. O novo caso de uso pertencer à mesma entidade e ao mesmo fluxo principal da tela atual.

\#\#\# Deve criar nova tela quando:

1\. Houver mudança clara de objetivo funcional.

2\. O fluxo exigir contexto próprio, navegação própria ou regras distintas.

3\. A complexidade adicional comprometer clareza da tela atual.

4\. A funcionalidade representar um processo independente.

5\. A separação melhorar entendimento, manutenção e experiência do usuário.

\#\#\# Regra de decisão

Se a proposta apenas “encaixa mais coisa” numa tela já saturada, criar nova tela pode ser melhor.  

Se a proposta apenas muda o modo de uso da mesma informação, reaproveitar é preferível.

\---

\#\# 5\. PADRÃO DE ESTRUTURA DE TELA

Toda tela interna deve seguir uma estrutura mínima previsível.

\#\#\# Estrutura recomendada

1\. \*\*Título da página\*\*

2\. \*\*Breadcrumb\*\*

3\. \*\*Descrição curta ou contexto da tela\*\* (quando necessário)

4\. \*\*Ação principal da tela\*\*

5\. \*\*Área de filtros\*\* (quando aplicável)

6\. \*\*Conteúdo principal\*\*

7\. \*\*Feedback visual de estado\*\*

\#\#\# Regras

\- Toda tela deve deixar claro “onde o usuário está” e “o que pode fazer ali”.

\- A ação principal deve estar visível sem exigir esforço excessivo de procura.

\- A hierarquia de leitura deve ser evidente.

\---

\#\# 6\. PADRÃO DE FORMULÁRIOS

Formulários devem ser simples, previsíveis e orientados à tarefa.

\#\#\# Regras obrigatórias

1\. Todo campo deve existir por necessidade real de negócio.

2\. Não criar campo para dado que já exista no sistema ou possa ser derivado por regra.

3\. Agrupar campos por assunto ou bloco lógico.

4\. Destacar campos obrigatórios de forma clara.

5\. Evitar excesso de campos em uma única tela sem agrupamento.

6\. Priorizar fluxo de preenchimento natural, do geral para o específico.

7\. Validar dados de forma clara e objetiva, próximo ao campo quando possível.

\#\#\# Ações principais de formulário

\- \*\*Salvar\*\*

\- \*\*Cancelar\*\*

\- \*\*Voltar\*\* (quando aplicável)

\#\#\# Regras de ações

\- O botão principal deve ter nomenclatura consistente e objetiva.

\- Evitar botões com rótulos vagos como “Executar” ou “Confirmar” sem contexto claro.

\- A ação principal deve ter maior destaque visual do que ações secundárias.

\---

\#\# 7\. PADRÃO DE LISTAGENS

Listagens devem facilitar leitura, busca e ação.

\#\#\# Regras obrigatórias

1\. Toda listagem deve ter título coerente com seu conteúdo.

2\. Sempre que fizer sentido, oferecer filtros, busca ou ordenação.

3\. Colunas devem refletir informação útil para decisão ou operação.

4\. Evitar excesso de colunas sem relevância prática.

5\. Ações por linha devem ser previsíveis e consistentes.

6\. Ações destrutivas devem exigir cuidado adicional.

\#\#\# Ações principais em listagens

\- Criar novo

\- Editar

\- Visualizar

\- Excluir

\- Exportar (quando aplicável)

\#\#\# Regra de clareza

Se o usuário precisar “adivinhar” o que fazer com a listagem, a tela está mal resolvida.

\---

\#\# 8\. PADRÃO DE AÇÕES PRINCIPAIS

Toda tela deve deixar explícita sua ação principal.

\#\#\# Regras

1\. Deve existir uma ação primária claramente identificável.

2\. Ações secundárias não devem competir visualmente com a principal.

3\. A nomenclatura dos botões deve refletir intenção real.

\#\#\# Exemplos recomendados

\- \`Salvar\`

\- \`Cadastrar cliente\`

\- \`Iniciar check-in\`

\- \`Gerar relatório\`

\- \`Exportar CSV\`

\#\#\# Evitar

\- \`OK\`

\- \`Enviar\` sem contexto

\- \`Executar\` sem clareza

\- \`Prosseguir\` quando a ação real puder ser nomeada

\---

\#\# 9\. EMPTY STATE, LOADING E ERRO VISUAL

A interface deve tratar estados do sistema de forma explícita, amigável e útil.

\#\#\# 9.1. Empty State

Quando não houver dados, a interface deve:

1\. informar claramente que não existem resultados;

2\. evitar aparência de erro;

3\. orientar o próximo passo quando fizer sentido.

\*\*Exemplos:\*\*

\- “Nenhum registro encontrado.”

\- “Ainda não há fornecedores cadastrados.”

\- “Nenhum resultado para os filtros aplicados.”

\#\#\# 9.2. Loading

Durante carregamento, a interface deve:

1\. sinalizar que a informação está sendo processada;

2\. evitar sensação de travamento;

3\. usar indicadores compatíveis com o contexto da tela.

\#\#\# Regras

\- Preferir skeletons, spinners discretos ou placeholders coerentes.

\- Não deixar áreas relevantes aparentemente quebradas durante carregamento.

\- Evitar bloquear a tela inteira sem necessidade.

\#\#\# 9.3. Erro Visual

Em caso de falha, a interface deve:

1\. informar de forma clara que houve erro;

2\. evitar mensagens técnicas desnecessárias ao usuário final;

3\. indicar próximo passo quando possível.

\*\*Exemplos:\*\*

\- “Não foi possível carregar os dados.”

\- “Ocorreu um erro ao salvar. Tente novamente.”

\- “Falha na comunicação com o servidor.”

\#\#\# Proibição

Nunca usar \`alert()\` como padrão de erro ou sucesso.  

Utilizar Toasts, Snackbars, mensagens inline ou blocos visuais apropriados. O documento atual já estabelece essa diretriz. 

\---

\#\# 10\. CONSISTÊNCIA DE TÍTULOS, BOTÕES E NOMENCLATURA VISUAL

\#\#\# Títulos de página

1\. Devem refletir a função real da tela.

2\. Devem ser curtos, claros e coerentes com o menu.

3\. Devem manter padrão de linguagem entre telas equivalentes.

\*\*Exemplos:\*\*

\- \`Cadastro de Fornecedores\`

\- \`Check-in\`

\- \`Relatório de Ocupação\`

\- \`Histórico de Movimentações\`

\#\#\# Botões

1\. Devem usar verbos claros.

2\. Devem refletir a ação real.

3\. Devem seguir padrão consistente em todo o sistema.

\#\#\# Nomenclatura visual

1\. O mesmo conceito deve sempre aparecer com o mesmo nome.

2\. Evitar sinônimos desnecessários para a mesma ação.

3\. Evitar alternância entre termos técnicos e termos operacionais para o mesmo elemento.

\*\*Exemplo de erro de consistência:\*\*

\- em uma tela usar “Salvar”

\- em outra usar “Confirmar cadastro”

\- em outra usar “Gravar”

para a mesma ação básica.

\#\#\# Regra

Uma vez definido o termo oficial, ele deve ser mantido em toda a interface.

\---

\#\# 11\. RESPONSIVIDADE E HIERARQUIA VISUAL

\#\#\# Responsividade mínima

Toda tela deve manter uso funcional em resoluções comuns de desktop e comportamento aceitável em larguras menores, sem quebrar leitura ou operação principal.

\#\#\# Regras mínimas

1\. O conteúdo principal deve permanecer legível.

2\. Botões e ações principais devem continuar acessíveis.

3\. Tabelas extensas devem prever tratamento adequado em telas menores.

4\. Formularios longos devem reorganizar blocos sem perder clareza.

\#\#\# Hierarquia visual

A interface deve deixar evidente:

1\. o que é mais importante;

2\. o que é informação de apoio;

3\. qual é a ação principal;

4\. qual é a ordem esperada de leitura.

\#\#\# Regra prática

O usuário deve conseguir identificar em poucos segundos:

\- onde está;

\- o que a tela mostra;

\- o que pode fazer.

\---

\#\# 12\. LAYOUT PADRÃO

\#\#\# Regras obrigatórias

1\. Todas as telas internas devem herdar o \`MainLayout\` com Sidebar.

2\. Breadcrumbs são obrigatórios em telas internas.

3\. Feedback visual deve usar componentes apropriados como Toasts e Snackbars.

4\. A estrutura visual deve ser consistente entre módulos equivalentes.

Estas regras já estão alinhadas ao padrão atual do projeto.

\---

\#\# 13\. PRIORIDADE DE DECISÃO

Em caso de dúvida, priorizar nesta ordem:

1\. Clareza de uso

2\. Consistência com o padrão do sistema

3\. Reaproveitamento com legibilidade

4\. Simplicidade visual

5\. Sofisticação estética

\---

\#\# 14\. RESULTADO ESPERADO

Toda tela, fluxo ou interação proposta deve resultar em:

\- navegação previsível;

\- organização funcional clara;

\- reaproveitamento coerente;

\- formulários simples;

\- listagens úteis;

\- feedback visual correto;

\- nomenclatura consistente;

\- responsividade mínima adequada;

\- hierarquia visual clara.

m herdar o \`MainLayout\` com Sidebar.  
2\. Breadcrumbs são obrigatórios em telas internas.  
3\. Feedback visual deve usar componentes apropriados como Toasts e Snackbars.  
4\. A estrutura visual deve ser consistente entre módulos equivalentes.

Estas regras já estão alinhadas ao padrão atual do projeto.

\---

\#\# 13\. PRIORIDADE DE DECISÃO

Em caso de dúvida, priorizar nesta ordem:

1\. Clareza de uso  
2\. Consistência com o padrão do sistema  
3\. Reaproveitamento com legibilidade  
4\. Simplicidade visual  
5\. Sofisticação estética

\---

\#\# 14\. RESULTADO ESPERADO

Toda tela, fluxo ou interação proposta deve resultar em:  
\- navegação previsível;  
\- organização funcional clara;  
\- reaproveitamento coerente;  
\- formulários simples;  
\- listagens úteis;  
\- feedback visual correto;  
\- nomenclatura consistente;  
\- responsividade mínima adequada;  
\- hierarquia visual clara.

# CONTEXT\_GIT.md

\# GIT WORKFLOW & VERSIONING STANDARDS

Este documento define o padrão de versionamento, branches, revisão e integração de código do projeto.  
\*\*INSTRUÇÃO:\*\* Toda alteração no repositório deve seguir estas regras para garantir rastreabilidade, estabilidade e continuidade do desenvolvimento.

\---

\#\# 1\. OBJETIVO DESTE DOCUMENTO

Este contexto tem como objetivo padronizar a forma como o time desenvolve, versiona, revisa e integra mudanças no projeto.

Este documento define:  
\- a branch principal do projeto;  
\- a estratégia de branches;  
\- a convenção de nomes;  
\- as regras de Pull Request;  
\- as regras de revisão e merge;  
\- o tratamento de hotfixes;  
\- as proibições de versionamento.

\---

\#\# 2\. PRINCÍPIOS GERAIS

Toda alteração no código deve seguir os seguintes princípios:

1\. \*\*Rastreabilidade\*\*  
   Toda mudança deve ser identificável e vinculada a uma finalidade clara.

2\. \*\*Isolamento de trabalho\*\*  
   Cada frente de alteração deve ser realizada em sua própria branch.

3\. \*\*Segurança de integração\*\*  
   Nenhuma mudança relevante deve entrar na branch principal sem revisão mínima.

4\. \*\*Clareza\*\*  
   Branches, commits e Pull Requests devem ter nomes e descrições compreensíveis.

5\. \*\*Governança sem excesso\*\*  
   O fluxo deve ser simples o suficiente para ser seguido no dia a dia, mas disciplinado o suficiente para manter a qualidade do projeto.

\---

\#\# 3\. BRANCH PRINCIPAL

\#\#\# Regra oficial  
A branch principal do projeto é a \`main\`.

\#\#\# Regras obrigatórias  
1\. A \`main\` deve representar a versão mais estável do projeto.  
2\. É proibido usar a \`main\` como branch normal de desenvolvimento contínuo.  
3\. Toda alteração deve nascer em branch própria, criada a partir da \`main\`.

\---

\#\# 4\. ESTRATÉGIA DE BRANCHES

Cada alteração deve ser feita em branch separada, com nome coerente com sua finalidade.

\#\#\# Prefixos oficiais  
\- \`feature/\` → nova funcionalidade  
\- \`fix/\` → correção de erro  
\- \`refactor/\` → reorganização técnica sem mudança funcional  
\- \`chore/\` → manutenção, configuração ou ajuste técnico  
\- \`hotfix/\` → correção urgente em fluxo crítico

\#\#\# Exemplos  
\- \`feature/cadastro-fornecedores\`  
\- \`feature/checkin-hospede\`  
\- \`fix/calculo-tarifa-ocupacao\`  
\- \`refactor/separacao-services-reservas\`  
\- \`chore/ajuste-config-nginx\`  
\- \`hotfix/erro-critico-checkin\`

\#\#\# Regra de nomenclatura  
1\. O nome da branch deve ser curto, claro e descritivo.  
2\. Deve representar o assunto principal da alteração.  
3\. Evitar nomes vagos como:  
   \- \`teste\`  
   \- \`ajustes\`  
   \- \`mudancas\`  
   \- \`versao-nova\`  
   \- \`branch-nova\`

\---

\#\# 5\. REGRAS DE DESENVOLVIMENTO

1\. Cada branch deve tratar uma frente principal de trabalho.  
2\. Evitar misturar correções, refactors e novas funcionalidades na mesma branch sem necessidade.  
3\. Se a alteração crescer demais ou mudar de escopo, o ideal é abrir nova branch.  
4\. Branch longa demais deve ser evitada.  
5\. O padrão preferencial é trabalhar com mudanças menores, claras e integráveis.

\---

\#\# 6\. COMMITS

\#\#\# Regras gerais  
1\. Todo commit deve representar uma mudança compreensível.  
2\. Commits devem ser pequenos o suficiente para facilitar revisão.  
3\. Evitar commits genéricos ou sem significado.

\#\#\# Exemplos recomendados  
\- \`feat: adiciona tela de cadastro de fornecedores\`  
\- \`fix: corrige cálculo de tarifa por ocupação\`  
\- \`refactor: separa regra de pedidos em service\`  
\- \`chore: ajusta configuração do nginx\`

\#\#\# Evitar  
\- \`ajustes\`  
\- \`update\`  
\- \`mudanças\`  
\- \`teste\`  
\- \`corrigindo coisas\`

\#\#\# Regra prática  
Quem ler o histórico deve conseguir entender a evolução do projeto sem precisar abrir todos os arquivos.

\---

\#\# 7\. PULL REQUEST

Toda integração na \`main\` deve ocorrer preferencialmente via Pull Request.

\#\#\# Regras obrigatórias  
1\. O Pull Request deve tratar uma alteração coerente e delimitada.  
2\. O título deve resumir com clareza a mudança principal.  
3\. A descrição deve informar, sempre que possível:  
   \- o que foi feito;  
   \- por que foi feito;  
   \- impacto esperado;  
   \- pontos de atenção;  
   \- dependências ou riscos.

\#\#\# Regra de qualidade  
Se o PR estiver grande demais para ser entendido com clareza, ele está mal dimensionado.

\---

\#\# 8\. REVISÃO

\#\#\# Regras  
1\. Toda alteração estrutural, sensível ou compartilhada deve passar por revisão.  
2\. Mudanças simples podem ter revisão mais leve, mas não devem ignorar o padrão do projeto.  
3\. Em caso de dúvida, revisar.  
4\. Nenhuma revisão deve se limitar apenas a “funciona ou não funciona”; ela deve considerar também:  
   \- aderência ao padrão;  
   \- impacto arquitetural;  
   \- clareza da implementação;  
   \- risco de manutenção futura.

\#\#\# Objetivo  
Garantir continuidade do projeto independentemente de quem desenvolveu a alteração.

\---

\#\# 9\. MERGE

O merge só deve acontecer quando a alteração:

1\. estiver funcionalmente coerente;  
2\. respeitar os padrões do projeto;  
3\. não introduzir quebra arquitetural evidente;  
4\. não deixar arquivos temporários, lixo ou inconsistências;  
5\. estiver suficientemente compreensível para manutenção futura.

\#\#\# Regra  
Não fazer merge por pressa quando a mudança ainda estiver confusa, incompleta ou desalinhada com o padrão.

\---

\#\# 10\. HOTFIX

\#\#\# Definição  
Hotfix é uma correção urgente aplicada para resolver problema crítico ou bloqueador.

\#\#\# Regras  
1\. Hotfix deve ser usado apenas em casos realmente urgentes.  
2\. Deve nascer em branch específica com prefixo \`hotfix/\`.  
3\. Deve ter escopo mínimo necessário para correção.  
4\. Após a correção, o histórico deve permanecer rastreável.  
5\. Não usar hotfix como atalho para desenvolvimento fora do fluxo normal.

\---

\#\# 11\. SINCRONIZAÇÃO COM A MAIN

\#\#\# Regras  
1\. Antes de abrir PR, a branch deve estar razoavelmente alinhada com a \`main\`.  
2\. Conflitos devem ser resolvidos com atenção, preservando a integridade do código.  
3\. Em caso de conflito estrutural, priorizar o padrão oficial do projeto, não a conveniência local.

\---

\#\# 12\. PROIBIÇÕES

1\. Não desenvolver diretamente na \`main\` como fluxo normal.  
2\. Não criar branches com nomes vagos ou genéricos.  
3\. Não misturar muitos assuntos diferentes na mesma branch.  
4\. Não abrir PR sem contexto mínimo.  
5\. Não fazer merge de alteração confusa ou sem revisão mínima.  
6\. Não usar hotfix como substituto de branch normal.  
7\. Não deixar arquivos temporários, testes soltos ou artefatos de experimento no repositório.

\---

\#\# 13\. PRIORIDADE DE DECISÃO

Em caso de dúvida, priorizar nesta ordem:

1\. Rastreabilidade  
2\. Clareza da alteração  
3\. Segurança de integração  
4\. Simplicidade do fluxo  
5\. Velocidade de entrega

\---

\#\# 14\. RESULTADO ESPERADO

O fluxo de Git do projeto deve resultar em:  
\- branches claras e organizadas;  
\- histórico compreensível;  
\- mudanças rastreáveis;  
\- integração mais segura;  
\- menor risco de perda de contexto;  
\- governança prática e sustentável para o time.

# Padronização de frontend

**Padronização de frontend por design system \+ código base \+ geração controlada**.

---

## **Conceito**

Você não deixa o prompt “inventar UI”.

Você fornece:

* **um padrão fixo de frontend**  
* **componentes reutilizáveis**  
* **estrutura obrigatória**

O prompt apenas **preenche dentro desse padrão**.

