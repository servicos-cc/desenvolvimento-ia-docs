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
