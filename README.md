# Padrões e Contextos Globais (Desenvolvimento IA)

Este repositório consolida os **4 contextos corporativos principais** que ditam as regras, padrões operacionais e arquiteturais a serem seguidos tanto pelo time de desenvolvedores humanos quanto por Agentes e IAs atuando no projeto.

## Estrutura do Repositório

Todos os padrões estão localizados na pasta `Docs/CONTEXT`:

- 🏛️ **`CONTEXT_ARCH_00.md`**: Padrão técnico e estrutural do projeto (Infraestrutura, separação de camadas, Docker Compose, FastAPI, regras de banco).
- 🤖 **`CONTEXT_AGENTS_00.md`**: Padrão global de comportamento da IA e Agentes (Instruções sobre como analisar requisitos, criar planos, "Plano Vivo" e evitar soluções literais).
- 🧭 **`CONTEXT_UX_00.md`**: Padrão de navegação, taxonomia e experiência de interface.
- 🔀 **`CONTEXT_GIT_00.md`**: Padrão corporativo de desenvolvimento e versionamento (Fluxo de PRs, nomenclatura de branches e revisão).

## Como Utilizar

A IA ou o Agente em execução no projeto deve ser alimentado com esses contextos antes de realizar qualquer tarefa. 

1. **Contexto de Sistema**: Esses arquivos funcionam em conjunto com arquivos de regras de negócios locais e assumem a prioridade para tomadas de decisões arquiteturais globais. 
2. **Desenvolvedores**: Usem esse repositório como guia de estilo. Sempre que uma exceção precisar ser adotada ou um novo padrão emergir, este repositório deve ser votado, atualizado e versionado de acordo.
3. **Plano Vivo**: Ao iniciar frentes de trabalho relevantes, a IA construirá as soluções guiando-se estritamente por estas definições, criando e mantendo um único "Plano Vivo" na raiz do foco de desenvolvimento, sem causar fraturas documentais.
