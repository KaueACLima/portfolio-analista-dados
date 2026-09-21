# 📌 Desfazendo e Revertendo Mudanças

### 1. Conceito Central
Esta aula cobre as três formas de descartar ou desfazer mudanças em um projeto Git: **restore**, **reset** e **revert**. A ideia central que amarra os três é o conceito de **HEAD** — um ponteiro que aponta para um commit específico (por padrão, o último commit realizado). Toda operação de restauração/reversão precisa de uma referência de "para onde voltar", e se você não especificar um commit, o Git usa o HEAD como base.

Os três comandos resolvem problemas diferentes: `restore` desfaz mudanças **não commitadas** (voltando arquivos para o estado de um commit); `reset` desfaz **commits já feitos**, movendo o HEAD para trás e decidindo o que acontece com as alterações desses commits; `revert` desfaz um commit **sem apagar histórico**, criando um novo commit que anula as mudanças do commit anterior.

### 2. Pontos-chave e Sintaxe

#### HEAD
- É um ponteiro que aponta para um commit específico — por padrão, o último commit feito no projeto.
- Toda operação de restore/reset/revert que não especifica um commit usa o HEAD como referência.

#### `git restore` — desfazer mudanças não commitadas
```bash
# Restaura o(s) arquivo(s) para o estado do HEAD (último commit)
git restore script.js
# ou, para todos os arquivos:
git restore .

# Restaura com base em um commit específico (não o HEAD)
git restore --source <hash-do-commit> .
```
- Uso típico no dia a dia: descartar mudanças recentes ainda não commitadas (ex: começar uma funcionalidade, decidir abandonar a abordagem antes de commitar).
- Também pode restaurar para um commit mais antigo específico (passando o hash via `git log`), efetivamente removendo do arquivo qualquer conteúdo adicionado depois daquele commit.

#### `git reset` — desfazer commits, com três variações
```bash
git reset --soft   # desfaz o commit, mas mantém as mudanças já na staging area (como se tivesse dado git add)
git reset --mixed  # desfaz o commit, mantém as mudanças no projeto, mas TIRA da staging area (precisa dar git add de novo)
git reset --hard   # desfaz o commit E APAGA as mudanças/arquivos por completo
```
- Sempre usa o HEAD como base se nenhum commit for especificado — e a recomendação da aula é resetar preferencialmente **apenas o último commit**, não vários para trás, porque isso descarta muito histórico e dificulta o trabalho.
- Diferença prática entre soft e mixed: ambos mantêm o conteúdo do arquivo no projeto — a diferença é só se ele já está "pronto" (staged) para o próximo commit (soft) ou se precisa passar por `git add` de novo (mixed).
- `--hard` é o único que efetivamente **apaga o código** da máquina — a aula reforça que isso exige consciência total de que você não vai precisar mais daquele conteúdo, porque não há como recuperá-lo depois (sem outras ferramentas fora do escopo do curso).

#### `git revert` — desfazer um commit sem perder histórico
```bash
# Reverte um commit específico criando um NOVO commit que desfaz as mudanças dele
git revert <hash-do-commit>
```
- Diferente do reset, o revert **não apaga nada do histórico** — ele cria um commit novo que anula o efeito do commit revertido, preservando o registro de que aquela mudança existiu e foi desfeita depois.
- É especialmente útil para reverter commits mais antigos (vários commits para trás) sem precisar mexer no histórico inteiro.
- O Git abre um editor de texto (Vim, no exemplo) com uma mensagem de commit automática do tipo "Reverte o commit \<hash\>", que pode ser mantida ou editada.

#### Critério de escolha (resumo da aula)
- **Desfazer alterações não commitadas** → `restore`.
- **Desfazer um commit local sem apagar histórico** → `reset --soft` ou `reset --mixed` (a diferença é só se o conteúdo fica pronto pra próximo commit ou não).
- **Desfazer um commit específico (inclusive mais antigo) mantendo o histórico visível** → `revert`.
- **Descartar tudo em relação ao commit anterior, sem intenção de recuperar** → `reset --hard`.

- 💡 **Dica:** o `git log` é a ferramenta usada ao longo de toda a aula para localizar o hash do commit que se quer usar como referência em `restore`, `reset` ou `revert` — sem ele, fica impossível apontar para um commit específico que não seja o HEAD.
- ⚠️ **Ponto de atenção:** `reset --hard` apaga os arquivos de verdade — a aula é explícita que, se aquele código for necessário depois, ele **não estará mais ali**, diferente de `revert`, que preserva tudo no histórico mesmo desfazendo o efeito.

### 3. 🧠 Raciocínio Lógico
- Sempre que uma operação de restore/reset/revert é chamada sem um commit explícito, o Git assume o HEAD (o último commit) como ponto de referência.
- No `restore`: o Git compara o estado atual do arquivo com o commit de referência e sobrescreve o arquivo para bater com aquele commit — por isso é indicado para mudanças que ainda não foram commitadas.
- No `reset`: o Git move o ponteiro HEAD para um commit anterior e "esquece" o commit removido do histórico; a flag (`--soft`/`--mixed`/`--hard`) decide apenas o destino do conteúdo daquele commit desfeito — permanece pronto pra commit (soft), permanece no projeto mas sem preparo (mixed), ou é apagado (hard).
- No `revert`: em vez de mover o HEAD para trás, o Git cria um commit **novo**, cujo conteúdo é o oposto do commit alvo — por isso o histórico cresce (soma um commit) em vez de encolher, preservando o registro de que a mudança existiu e depois foi desfeita.

### 4. Links e Referências Oficiais
- **[Git — git-restore](https://git-scm.com/docs/git-restore)** — documentação oficial do comando usado para desfazer mudanças não commitadas.
- **[Git — git-reset](https://git-scm.com/docs/git-reset)** — documentação oficial do comando usado para desfazer commits, com as flags `--soft`, `--mixed` e `--hard` detalhadas.
- **[Git — git-revert](https://git-scm.com/docs/git-revert)** — documentação oficial do comando usado para desfazer um commit criando um novo commit reverso.
- **HEAD** — ponteiro interno do Git que aponta para o commit atual (geralmente o último); conceito central que unifica os três comandos desta aula, coberto na própria documentação de `git-reset` e `git-revert` acima.

---

Lembretes de sempre:
- Salvar este resumo na base como `git-primeiros-passos-desfazendo-e-revertendo-mudancas-resumo.md`.
- Atualizar o painel marcando esta aula como ✅ no módulo "Primeiros passos com o Git" (Frente 5) — restam 2 aulas nesse módulo depois desta (a próxima já entra em branches, segundo o próprio professor).