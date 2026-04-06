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
