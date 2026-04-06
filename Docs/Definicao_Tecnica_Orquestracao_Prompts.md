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

