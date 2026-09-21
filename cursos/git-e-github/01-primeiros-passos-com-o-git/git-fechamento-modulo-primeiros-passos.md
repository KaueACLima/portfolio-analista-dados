# 🏆 Fechamento de Módulo e Teste de Fixação
**Módulo:** Primeiros passos com o Git — *Git e GitHub: Guia Definitivo na Era da IA* (Rocketseat)

### 1. Resumo Executivo
Este módulo constrói, de forma incremental, todo o alicerce necessário para versionar um projeto sozinho, localmente, antes de qualquer colaboração via GitHub. Ele começa pelo *porquê*: entender que versionamento resolve problemas concretos (colaboração sem sobrescrita, histórico completo, rollback e experimentação segura), e que o Git venceu o mercado não por ser pioneiro — pelo contrário, ele chegou depois de RCS, CVS/SVN e BitKeeper —, mas por resolver as limitações de velocidade, escala e simplicidade que esses antecessores tinham. A peça central de todo o modelo mental do Git é o **snapshot**: cada commit é uma fotografia completa do projeto, não um diff incremental, e é isso que torna operações como rollback praticamente instantâneas.

A partir daí, o módulo desce para a prática: instalar o Git (Windows/Mac/Linux), configurar identidade (`user.name`/`user.email`), e entender o fluxo de três estados que **todo** arquivo percorre — Working Directory → Staging Area → Commit — usando `git init`, `git add`, `git commit`, `git status` e `git log` como ferramentas do dia a dia. Um ponto sutil e importante aqui é que, para o Git, a identidade de um arquivo é seu nome + sua pasta — renomear ou mover é, na prática, "apagar e criar", não "alterar".

A "grande lição" técnica do módulo, porém, está no bloco final: existem **quatro formas diferentes de desfazer trabalho** (`restore`, `reset --soft/--mixed/--hard`, `revert`), e cada uma resolve um problema distinto — desfazer o que não foi commitado, apagar um commit local recente, ou desfazer um commit específico *sem* perder o histórico. Entender essa diferença evita dois erros comuns de quem está começando: usar `reset --hard` sem saber que ele apaga código de verdade, e não saber que `revert` é a ferramenta certa quando o objetivo é manter rastreabilidade de "o que foi desfeito e por quê". O `git diff` fecha o módulo como a ferramenta de inspeção que amarra tudo isso — permitindo enxergar exatamente o que mudou antes de decidir se aquilo deve ser commitado, revertido ou descartado.

### 2. Glossário Técnico
- **Versionamento (controle de versão):** processo de rastrear e gerenciar mudanças em um projeto ao longo do tempo, permitindo navegar entre pontos anteriores da história do código.
- **Snapshot / Commit:** uma "fotografia" completa do estado do projeto em um momento específico. No Git, cada commit é um snapshot, identificado por um hash único (SHA-1) e por metadados automáticos (autor, data, mensagem).
- **Working Directory:** o diretório de trabalho — onde você edita os arquivos no dia a dia, refletindo o estado atual do repositório mais as alterações ainda não commitadas.
- **Staging Area:** área de preparação onde você seleciona, com `git add`, quais mudanças específicas vão entrar no próximo commit.
- **HEAD:** ponteiro que aponta para um commit específico — por padrão, o último commit feito. Serve de referência padrão em operações como `restore`, `reset` e `revert` quando nenhum commit é especificado.
- **git init:** comando que transforma uma pasta comum em um repositório Git, criando a pasta oculta `.git` onde todo o histórico de versionamento é armazenado.
- **git status:** comando que mostra o estado atual de cada arquivo do repositório (não rastreado, pronto para commit, modificado, deletado) e em qual branch você está.
- **git diff:** compara estados do projeto entre si. Sem flag, compara Working Directory com o último commit; com `--cached`/`--staged`, compara a Staging Area com o último commit; com dois hashes, compara dois commits diretamente.
- **git restore / git reset / git revert:** as três formas de desfazer trabalho, cada uma com escopo diferente — `restore` desfaz mudanças não commitadas; `reset` (soft/mixed/hard) desfaz commits locais, decidindo o destino do conteúdo; `revert` desfaz um commit criando um novo commit que anula seu efeito, preservando o histórico.
- **.gitignore:** arquivo de configuração que diz ao Git quais arquivos/pastas ele deve ignorar ao versionar (ex: arquivos de sistema como `.DS_Store` no Mac).

### 3. Desafio de Fixação (Quiz Interativo)

**Questão 1**
Você está trabalhando em uma funcionalidade nova, fez `git add .` em parte dos arquivos, mas continuou editando um deles depois disso (ou seja: parte da mudança está em staging, e há mais mudança ainda solta no working directory, no mesmo arquivo). Se você rodar `git diff` (sem nenhuma flag) neste momento, o que exatamente será mostrado?
- (a) Todas as mudanças do arquivo, desde o último commit até agora
- (b) Apenas a parte da mudança que ainda não foi adicionada com `git add` (a que está fora da staging area)
- (c) Apenas a parte que já está em staging
- (d) Nada, porque o arquivo já tem alguma mudança em staging

**Questão 2**
Você commitou uma funcionalidade ontem, e hoje descobriu que ela está causando um bug em produção. Você já fez outros 3 commits depois dela, e não quer perder o trabalho feito nesses commits mais recentes. Qual comando é o mais adequado para desfazer especificamente aquele commit problemático, mantendo o restante do histórico e deixando claro, para quem olhar o log depois, que aquela mudança foi removida intencionalmente?
- (a) `git reset --hard` apontando para o commit anterior ao problemático
- (b) `git restore` no arquivo afetado
- (c) `git revert` no hash do commit problemático
- (d) Apagar manualmente as linhas de código e commitar de novo sem mensagem

**Questão 3**
Você criou um arquivo `config.js` na raiz do projeto, fez commit, e depois decidiu movê-lo para dentro de uma pasta `src/`. Ao rodar `git status` depois de mover o arquivo, o que você deve esperar ver, e por quê?
- (a) Nenhuma mudança, porque o conteúdo do arquivo não mudou
- (b) O arquivo aparecendo como modificado, porque só o caminho mudou
- (c) `config.js` aparecendo como deletado e `src/config.js` aparecendo como um arquivo novo, porque para o Git a identidade do arquivo é nome + pasta
- (d) Um erro, porque o Git não permite mover arquivos versionados

Pronto para o teste? Envie suas respostas e eu faço a correção comentada.

**Correção comentada**
- Mandou bem — as três estão certas! ✅

**Questão 1 — b.** Exatamente: sem flag, o `git diff` só olha pro que está fora da staging area. A parte que já foi adicionada com `git add` fica "escondida" até você usar `--cached`/`--staged`. É o erro clássico de achar que "não mudou nada" quando na verdade só migrou de estado.

**Questão 2 — c.** `git revert` é a ferramenta certa aqui: ele cria um commit novo que anula o commit problemático, sem tocar nos 3 commits feitos depois. `reset --hard` destruiria esse histórico recente junto, o que não é o objetivo.

**Questão 3 — c.** Isso conecta direto com o "segredo de ouro" da aula de Ciclo de Vida dos Arquivos: pro Git, a identidade de um arquivo é nome + caminho. Mover ou renomear é, na prática, apagar o antigo e criar um novo — mesmo sem mexer em uma linha de código.

Quiz do fechamento 100%. 🎉