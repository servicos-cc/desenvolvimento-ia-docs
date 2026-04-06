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

