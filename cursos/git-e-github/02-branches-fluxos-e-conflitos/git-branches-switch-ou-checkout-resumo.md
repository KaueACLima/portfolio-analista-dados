# 📌 Trocar de branches de forma atualizada: Switch ou Checkout?

### 1. Conceito Central
O `git checkout` é um comando "canivete suíço": ele serve para trocar de branch, restaurar arquivos e navegar para commits específicos — tudo com a mesma sintaxe base. Essa versatilidade virou um problema de usabilidade (ex.: um autocomplete errado no terminal pode restaurar um arquivo sem querer, quando a intenção era trocar de branch). Por isso, o Git introduziu dois comandos mais específicos: `git restore` (pra restaurar arquivos) e `git switch` (pra trocar de branch ou navegar entre commits). O `checkout` continua funcionando normalmente, mas `switch`/`restore` são a forma mais moderna e explícita de fazer a mesma coisa.

### 2. Pontos-chave e Sintaxe
- `git checkout` acumula três funções diferentes: trocar de branch, restaurar arquivos e ir para um commit específico (via hash) — o que a aula chama de "erro de padrão" do Git, por concentrar funcionalidades demais num só comando.
- `git restore <arquivo>` substitui o `checkout` na função de restaurar um arquivo ao estado do último commit — sintaxe mais clara e direta.
- `git switch <branch>` substitui o `checkout` na função de trocar de branch.
- `git switch -c <nova-branch>` cria e já muda para uma nova branch (equivalente ao `checkout -b`).
- `git switch --detach <hash>` navega até um commit específico sem estar "preso" a nenhuma branch — deixa explícito que, nesse caso, você está navegando entre **commits**, e não entre **branches**.
- 💡 **Regra prática:** se o objetivo é explorar/debugar commits antigos, use `switch --detach`; se o objetivo é trabalhar em outra branch, use `switch` puro. O comando deixa a intenção clara — diferente do `checkout`, que é ambíguo.
- Navegar manualmente entre commits não é o padrão recomendado no dia a dia — pra desfazer mudanças, o correto continua sendo `revert`/`reset` (já vistos no módulo anterior).
- `checkout` continua válido e funcional — ainda é comum ver em projetos legados ou em versões antigas do Git — mas `switch`/`restore` são a recomendação atual por serem mais explícitos e não terem efeitos colaterais indesejados.

```bash
# --- Checkout: um comando fazendo várias coisas diferentes ---
git checkout <branch>              # troca de branch
git checkout -- <arquivo>          # restaura arquivo ao estado do último commit
git checkout <hash-do-commit>      # vai para um commit específico
git checkout -b <nova-branch>      # cria e muda para uma nova branch

# --- Alternativas modernas, uma função por comando ---
git restore <arquivo>                  # restaura arquivo (substitui checkout -- <arquivo>)
git switch <branch>                    # troca de branch (substitui checkout <branch>)
git switch -c <nova-branch>            # cria e muda para uma nova branch (substitui checkout -b)
git switch --detach <hash-do-commit>   # navega até um commit específico (substitui checkout <hash>)
```

### 3. 🔀 Mapeamento: função do Checkout → comando moderno equivalente
```
[checkout: trocar de branch]        -> git switch <branch>
[checkout: restaurar arquivo]       -> git restore <arquivo>
[checkout: ir p/ commit específico] -> git switch --detach <hash>
[checkout: criar + trocar branch]   -> git switch -c <nova-branch>
```

### 4. Links e Referências Oficiais
- **git switch** — comando dedicado a trocar de branch ou navegar entre commits. Documentação: [git-scm.com/docs/git-switch](https://git-scm.com/docs/git-switch)
- **git restore** — comando dedicado a restaurar arquivos ao estado de um commit. Documentação: [git-scm.com/docs/git-restore](https://git-scm.com/docs/git-restore)
- **git checkout** — comando legado multifuncional (trocar branch / restaurar arquivo / navegar commit). Documentação: [git-scm.com/docs/git-checkout](https://git-scm.com/docs/git-checkout)

---

**Salvar como:** `git-branches-switch-ou-checkout-resumo.md`
**Commit:** `docs(git): resumo aula - Trocar de branches de forma atualizada: Switch ou Checkout?`
**Pasta:** `02-branches-fluxos-conflitos/`

Nota informativa: restam **5 de 8 aulas** no módulo "Branches, fluxos e conflitos".