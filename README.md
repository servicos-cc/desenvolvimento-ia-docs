# Padrões e Contextos Globais (Desenvolvimento IA)

Este repositório consolida a fundação de **Context Engineering** do projeto. Ele estabelece as regras de negócio, as diretrizes arquiteturais e o comportamento operacional esperado para o desenvolvimento assistido por inteligência artificial e para a colaboração do time.

A adoção estrita desta base de conhecimento garante que agentes e plataformas copilot atuem como engenheiros de software seniores, gerando código robusto, escalável e perfeitamente alinhado com a governança da empresa, mitigando ao máximo "alucinações" e implementações fora do padrão.

## Estrutura do Conhecimento Otimizado (Context Assets)

As diretrizes estão modularizadas dentro do diretório `Docs/CONTEXT/`. Essa quebra aumenta a precisão durante a injeção em prompts, dividindo as regras nas seguintes camadas lógicas:

- **`CONTEXT_ARCH_00.md`**: Define a Infraestrutura da aplicação (Docker, Nginx), as fronteiras das Camadas Lógicas (FastAPI com ORM), as regras de banco de dados e a imutabilidade estrita das migrations.
- **`CONTEXT_AGENTS_00.md`**: Estabelece o "System Prompt" comportamental da IA: regras de ponderação de decisões, obrigação do anti-literalismo, exigência de análise prévia e a utilização compulsória do método "Plano Vivo".
- **`CONTEXT_UX_00.md`**: Define a Experiência Operacional: taxonomia correta de menus, regras de empty/loading states, tratamento responsivo e padrões inegociáveis para renderização de telas e retorno de informações visuais.
- **`CONTEXT_GIT_00.md`**: Define a Estrutura de Versionamento: nomeação semântica de branches, padrão focado em features e a governança rígida para aprovação, revisão e execução de Pull Requests.

---

## Onboarding Diário: Integrando a IA ao Workflow

Para maximizar a precisão da IA e restringir as gerações à realidade da empresa, **nenhuma solicitação de escopo ou de código deve começar sem o pareamento prévio (few-shot context)** baseado nestes contextos.

### Passo a Passo para Desenvolvedores e Revisores

1. **Sincronize a Realidade Local**: Garanta que você está usando a última versão de diretrizes presente na branch `main` (`git pull`).
2. **Ancoragem de Contexto (Context Injection)**: 
   - Ao iniciar qualquer nova iteração ou thread em seu assistente de IA (Cursor, GitHub Copilot, Editores Inteligentes, etc.), **forneça uma referência explícita** aos 4 arquivos do diretório `Docs/CONTEXT/` utilizando as ferramentas nativas de anexos (ex: @Files, Context Symbols).
3. **Ponto de Inicialização Técnica (System Prompting)**: 
   - Antes de colar a descrição da tarefa (o backlog), adicione ao chat a seguinte instrução técnica que forçará a adoção estrutural da IA:
   > *"Leia rigorosamente os documentos de arquitetura, agenciamento, ux e versionamento anexados para carregar a configuração atual do projeto. Quaisquer propostas, elaborações de planos ou linhas de código emitidas a partir deste momento deverão obrigatoriamente honrar as regras de negócio expressas neles."*
4. **Validação de Conformidade (Governança Humana)**:
   - Torne o agente de IA responsável. Acuse desvios sempre que o LLM propor gerar falsos dados isolados sem autorização explícita ("Mocks"), promover dependências de frameworks não citados ou quando ignorar o ciclo do anti-literalismo priorizando atalhos arquiteturais proscritos no documento `CONTEXT_AGENTS_00.md`.

## Evolução dos Padrões e Continuous Learning

Os padrões documentados neste repositório refletem as configurações vivas de projeto e baseiam o amadurecimento constante dele:
- **Plano Vivo (Design Docs Iterativos)**: Na ideação de novas frentes de trabalho ou refatorações críticas, encoraje a IA a projetar previamente e submeter um plano. Autorize essa estruturação antes do início das escritas. Reúna os avanços unicamente naquele arquivo local da feature.
- **Retroalimentação de Regras Globais**: Se ao longo do desenvolvimento for consolidado um novo paradigma tecnológico ou surgir uma alteração de padronização, elas devem ser discutidas com a equipe e codificadas como um Pull Request para a própria documentação dos Contextos. Ao atualizar estes arquivos fonte, garantimos o alinhamento arquitetural para sessões de Inteligência Artificial subsequentes em todas as pontas da empresa.
