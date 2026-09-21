# 📌 Rebase: reescrevendo o histórico

### 1. Conceito Central
`merge` e `rebase` resolvem o mesmo problema — integrar mudanças de uma branch em outra —, mas produzem históricos visualmente diferentes. O `merge` **preserva** o histórico de ambas as branches, criando um commit extra que marca o ponto de união (a árvore fica com bifurcações visíveis). Já o `rebase` **reescreve** o histórico: ele reaplica os commits de uma branch sobre a outra como se tivessem sido criados ali, produzindo um histórico linear, sem bifurcações — mas às custas de perder o registro de quando/onde a integração realmente aconteceu.

### 2. Pontos-chave e Sintaxe
- **Merge**: analisa o ponto comum entre as branches e cria um commit de união. Se não houver ponto de divergência real, pode ocorrer um *fast-forward* (sem commit extra) — mas isso é raro na prática de mercado.
  - ✅ Vantagens: histórico fiel e auditável, rastreia quem/quando integrou cada mudança, seguro para branches compartilhadas.
  - ⚠️ Desvantagens: histórico fica "poluído" com muitas bifurcações à medida que o projeto cresce; menos linear, pode confundir quem está entrando no projeto.
  - Quando usar: branches compartilhadas (`main`, `develop`), times grandes, quando o histórico precisa refletir o fluxo real, e ao abrir pull requests para produção.
- **Rebase**: remove temporariamente os commits locais, atualiza a branch base e reaplica os commits como se fossem novos — resultando num único "galho" linear.
  - ✅ Vantagens: histórico linear, mais fácil de ler/debugar, ideal pra organizar branches locais antes de integrar.
  - ⚠️ Desvantagens: reescreve o histórico (perde-se rastreabilidade de datas/autoria originais); perigoso em branches compartilhadas entre vários devs; pode gerar conflitos repetitivos de forma mais agressiva.
  - ⚠️ **Regra de ouro:** nunca fazer rebase numa branch que outras pessoas estão usando — o risco de perder rastreabilidade e gerar conflitos é alto.
  - Quando usar: branches locais/individuais, antes de abrir um pull request (pra "limpar" o histórico), em times que valorizam linearidade.
- **Fluxo recomendado pelo professor:** desenvolver em branch local → usar `rebase` pra manter o histórico local limpo (se usou várias branches intermediárias) → entregar na branch principal usando `merge`. Na dúvida, prefira `merge` — é a opção mais segura.
- Importante: o **conteúdo final** do código é o mesmo nos dois casos — a diferença é só em como o histórico de commits fica registrado.

```bash
# Merge: mantém o histórico das duas branches, cria commit de união
git checkout main
git merge feature

# Rebase: reaplica os commits da feature sobre a main, histórico linear
git checkout feature
git rebase main
# (nesse fluxo, a feature "sobe" e se torna a sequência mais recente sobre a main)
```

### 3. 🏗️ Diagrama Lógico — Merge vs. Rebase
```
Ponto de divergência: commits iniciais compartilhados por [master] e [feature]

--- MERGE ---
[master: c1 -> c2 -> c3] \
                          -> [merge commit] -> histórico com bifurcação visível
[feature: c1 -> f1 -> f2] /

--- REBASE ---
[master: c1 -> c2 -> c3] -> [f1' -> f2'] -> histórico linear único
(commits da feature são "reaplicados" na ponta da master, sem bifurcação)
```

### 4. Links e Referências Oficiais
- **git merge** — integra branches preservando histórico. Documentação: [git-scm.com/docs/git-merge](https://git-scm.com/docs/git-merge)
- **git rebase** — reaplica commits de uma branch sobre outra, linearizando o histórico. Documentação: [git-scm.com/docs/git-rebase](https://git-scm.com/docs/git-rebase)
- **Fast-forward** — tipo de merge sem commit extra, quando não há divergência real entre as branches.

---

**Salvar como:** `git-branches-rebase-reescrevendo-o-historico-resumo.md`
**Commit:** `docs(git): resumo aula - Rebase: reescrevendo o histórico`
**Pasta:** `02-branches-fluxos-conflitos/`

Nota informativa: restam **4 de 8 aulas** no módulo "Branches, fluxos e conflitos".