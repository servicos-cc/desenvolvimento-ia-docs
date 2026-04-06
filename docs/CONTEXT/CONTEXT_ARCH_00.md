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
