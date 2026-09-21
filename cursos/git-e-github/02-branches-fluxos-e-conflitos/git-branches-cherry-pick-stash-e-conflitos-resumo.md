# 📌 Cherry pick, stash e um pouco sobre conflitos

### 1. Conceito Central
Esta aula traz duas ferramentas que fogem do fluxo linear "criar commit → trocar de branch → criar próximo commit": **stash** (guardar temporariamente alterações não commitadas, sem criar um ponto no histórico) e **cherry-pick** (trazer um commit específico de uma branch para outra, sem trazer todos os demais). Ambas resolvem situações do dia a dia em que você precisa interromper ou selecionar trabalho sem recorrer a merge/rebase completos. A aula também introduz, de forma breve, o conceito de **conflito**: quando o Git não consegue decidir sozinho qual de duas versões de um mesmo trecho deve prevalecer — algo que tanto stash quanto cherry-pick podem gerar.

### 2. Pontos-chave e Sintaxe

**Git Stash**
- Serve pra guardar temporariamente alterações que ainda não foram commitadas, limpando o diretório de trabalho — sem criar um commit, já que a mudança ainda não é "um ponto definitivo no histórico".
- Caso de uso típico: você está no meio de algo, surge uma prioridade urgente (ex.: corrigir um bug) e você precisa trocar de branch sem perder o que estava fazendo nem commitar algo incompleto.
- O stash funciona como uma **pilha** (o último que entrou é o primeiro a ser considerado pra aplicar).
- Por padrão, guarda arquivos **modificados e rastreados** pelo Git — arquivos não rastreados (novos, nunca commitados) só entram com a flag `-u`.
- ⚠️ **Stash não substitui commit** — commit existe pra dar rastreabilidade; stash é só uma pausa temporária.
- ⚠️ Stash pode gerar **conflito**, porque ele não é um ponto do histórico — o Git não tem como comparar de forma automática se o conteúdo do stash ou o do commit atual deve prevalecer.
- Boas práticas: aplicar o stash o quanto antes (quanto mais tempo passa, maior a chance de conflito) e não acumular stashes sem uso — dar `drop` no que não serve mais.

```bash
git stash                    # guarda alterações não commitadas (nome automático)
git stash -m "meu stash"     # guarda alterações com nome customizado
git stash list               # lista os stashes salvos

git stash apply              # aplica o último stash SEM removê-lo da lista
git stash pop                # aplica o último stash e REMOVE ele da lista

git stash drop stash@{0}     # apaga um stash específico
git stash -u                 # inclui também arquivos não rastreados no stash
```

**Cherry-pick**
- Traz **um commit específico** de outra branch — diferente de merge/rebase, que trazem todos os commits de uma vez.
- O Git cria um **novo commit** com o mesmo conteúdo/nome do original, mas com um **hash diferente** — não é uma referência ao commit original, é uma duplicata.
- Casos de uso: corrigir um bug em produção rapidamente puxando só o commit da correção; aproveitar uma feature específica sem trazer o resto da branch; recuperar um commit que foi feito por engano na branch errada.
- ⚠️ Consequência importante: se depois você fizer merge/rebase da branch de origem, pode acabar com **dois commits de mesmo nome** no histórico (o original e a "cópia" do cherry-pick) — quebra a rastreabilidade por nomes que o time costuma usar no dia a dia.
- Em caso de conflito durante o cherry-pick, o processo pausa e você decide: resolver e continuar, ou abortar.
- ⚠️ **Regra de uso:** cherry-pick deve ser exceção, não rotina — usar com cuidado especial em times, pois pode introduzir mudanças inesperadas na branch de alguém. Fazer cherry-picks com frequência costuma ser sintoma de um fluxo de lançamento de features mal organizado.

```bash
git checkout feature-login     # vá até a branch de origem, para localizar o commit
git log                        # pegue o hash do commit desejado

git checkout main              # vá para a branch de DESTINO
git cherry-pick <hash>         # traz apenas aquele commit para a branch atual

git cherry-pick --continue     # após resolver um conflito, continua o processo
git cherry-pick --abort        # aborta o cherry-pick em andamento
```

### 3. 🔀 Mapeamento: quando usar cada comando
```
[Preciso pausar trabalho não commitado p/ trocar de branch] -> git stash
[Quero voltar ao que estava fazendo depois]                 -> git stash apply / git stash pop
[Quero descartar um stash que não serve mais]                -> git stash drop

[Quero só 1 commit específico de outra branch]                -> git cherry-pick <hash>
[Quero TODOS os commits de outra branch, linear]               -> git rebase
[Quero TODOS os commits de outra branch, preservando histórico] -> git merge
```

### 4. Links e Referências Oficiais
- **git stash** — guarda temporariamente alterações não commitadas. Documentação: [git-scm.com/docs/git-stash](https://git-scm.com/docs/git-stash)
- **git cherry-pick** — aplica as mudanças de um commit específico em outra branch. Documentação: [git-scm.com/docs/git-cherry-pick](https://git-scm.com/docs/git-cherry-pick)
- **Conflitos de merge (introdução)** — situação em que o Git não consegue decidir automaticamente entre duas versões de um mesmo trecho; será aprofundado em aulas futuras do módulo.

---

**Salvar como:** `git-branches-cherry-pick-stash-e-conflitos-resumo.md`
**Commit:** `docs(git): resumo aula - Cherry pick, stash e um pouco sobre conflitos`
**Pasta:** `02-branches-fluxos-conflitos/`

Nota informativa: restam **3 de 8 aulas** no módulo "Branches, fluxos e conflitos".