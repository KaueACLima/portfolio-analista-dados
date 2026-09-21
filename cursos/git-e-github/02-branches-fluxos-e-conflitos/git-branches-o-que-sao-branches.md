# 📌 O que são branches?

### 1. Conceito Central
Branches (ramificações) são um conceito fundamental do Git que permite desenvolver funcionalidades, corrigir bugs ou testar mudanças em um projeto sem alterar diretamente o código principal. A analogia usada é a de uma árvore: o Git é o tronco principal e cada branch é um galho que se ramifica dele, podendo depois se unir novamente ao tronco. A branch principal — geralmente chamada de `main` ou `master` — contém o código que está em produção, ou seja, a versão que o cliente final está usando. Trabalhar em branches separadas evita que alterações em desenvolvimento quebrem o que já está funcionando para o usuário.

### 2. Pontos-chave e Sintaxe
- Branches criam **ambientes de trabalho independentes**: cada pessoa (ou time) pode desenvolver em sua própria branch sem interferir no trabalho dos outros.
- **Integração controlada**: as alterações de uma branch ficam isoladas até serem revisadas, testadas e mescladas (merge) na branch principal.
- **Prevenção de erros**: problemas são resolvidos antes de o código chegar à branch principal, resultando em um projeto mais estável e numa experiência melhor para quem usa.
- **Trabalho em paralelo**: times inteiros podem trabalhar em branches diferentes ao mesmo tempo e depois unificar tudo em uma única entrega.
- Estrutura comum de branches no mercado:
  - `main`/`master`: código em produção, o que o cliente final acessa.
  - `develop`: onde a funcionalidade é testada internamente pelo time (QA, design, produto) antes de ir para produção.
  - `feature`: branches onde novas funcionalidades são desenvolvidas antes de irem para a `develop`.
- Comandos essenciais de branch (mencionados de forma conceitual, sem sintaxe exata dada na aula): listar branches existentes, criar uma nova branch, mudar de uma branch para outra, e integrar (merge) duas branches.
- 💡 **Dica:** a lógica de isolar o trabalho em branches por etapa (feature → develop → main) permite saber exatamente em que estágio do desenvolvimento um código está e se o cliente já tem acesso àquela funcionalidade ou não.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Feature (nova funcionalidade em desenvolvimento)]
   -> merge ->
[Develop (testada pelo time: QA, design, produto)]
   -> merge ->
[Main / Master (produção, acessada pelo cliente final)]
```

### 4. Links e Referências Oficiais
- **Git** — sistema de controle de versão distribuído no qual o conceito de branches (ramificações) se baseia. Documentação oficial: [git-scm.com](https://git-scm.com/doc)
- **Branch (ramificação)** — ponteiro para uma linha independente de desenvolvimento dentro de um repositório Git.
- **Merge** — operação que une o histórico de commits de duas branches diferentes; será aprofundada em aulas mais práticas futuras.
- **GitGraph** — extensão de visualização gráfica de branches citada como ferramenta que será usada na próxima aula (mencionada pelo nome, mas sem link confirmado com segurança — vale buscar diretamente no marketplace de extensões do VS Code).
