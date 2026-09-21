# 📌 Adicionando e Confirmando Alterações (via Terminal)

### 1. Conceito Central
Esta aula coloca em prática os conceitos vistos até aqui (repositório local, `git init`, os três estados working directory/staging/commit) usando o terminal integrado ao VS Code. O foco é o comando `git status`, que funciona como o "raio-x" do projeto — ele mostra em que estado cada arquivo está (não rastreado, pronto para commit, modificado, deletado) e orienta quais comandos usar em seguida. A aula também introduz o `git log`, que exibe o histórico de commits já realizados.

### 2. Pontos-chave e Sintaxe
- `git status` é o comando central da aula — ele informa: em qual branch você está, se existem commits no repositório, e o estado atual de cada arquivo (não rastreado / pronto para stage / modificado / deletado).
- A aula introduz de forma breve o conceito de **branch** (ramificação): o Git é comparado a uma árvore com galhos, onde cada galho pode ter alterações diferentes — mas por padrão o Git sempre começa na branch principal (`main`). O aprofundamento desse conceito fica para aulas futuras.

```bash
# Cria o arquivo do projeto (neste exemplo, um script.js com um console.log)

# Verifica o estado atual do repositório
git status
# -> mostra: está na branch main, nenhum commit ainda, script.js não rastreado

# Adiciona o arquivo específico à staging area
git add script.js

# Verifica novamente: agora mostra que há uma mudança pronta para commit
git status

# Cria o primeiro commit, com mensagem descritiva
git commit -m "Primeira versão do meu projeto"

# Verifica novamente: agora existe 1 commit registrado
git status

# Exibe o histórico de commits (autor, data, mensagem)
git log
```

- Depois do primeiro commit, alterar o arquivo (ex: mudar o conteúdo do `console.log`) faz o VS Code marcar o arquivo com um **"M" de modificado** na interface visual do editor — e o `git status` reflete o mesmo status.
- Apagar um arquivo já commitado também aparece refletido no `git status`, indicando que o arquivo foi deletado.
- O `git log` mostra os commits do mais recente para o mais antigo, cada um com autor (vindo da configuração `user.name` feita em aula anterior), data e mensagem descritiva.
- 🔎 **Observação:** durante a demonstração, aparece um arquivo extra que o Git não está rastreando, mencionado só de passagem — o próprio professor diz que vai explicar o que é esse arquivo só na próxima aula, e que ele não necessariamente vai aparecer na máquina de todo mundo. Não acrescentei detalhe sobre esse arquivo aqui porque a transcrição não deixa claro qual é (o áudio ficou ambíguo nesse trecho) — vale prestar atenção na próxima aula pra fechar esse ponto.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Arquivo criado no Working Directory] (ex: script.js)
        |
        v git status
"Arquivo não rastreado" -> Git sugere usar git add
        |
        v git add script.js
[Staging Area] -> "Mudança pronta para commit"
        |
        v git commit -m "mensagem"
[Commit registrado] -> branch main -> visível via git log
        |
        v (arquivo é alterado depois do commit)
[Working Directory] -> "Arquivo modificado" (M no VS Code + git status)
        |
        v (arquivo é apagado)
[Working Directory] -> "Arquivo deletado" (refletido no git status)
```

### 4. Links e Referências Oficiais
- **[Git — git-status](https://git-scm.com/docs/git-status)** — documentação oficial do comando central desta aula, usado para verificar o estado do repositório e dos arquivos.
- **[Git — git-log](https://git-scm.com/docs/git-log)** — documentação oficial do comando usado para visualizar o histórico de commits.
- **Branch (ramificação)** — conceito citado de forma introdutória (comparação com "árvore com galhos"); a aula explicitamente adia o aprofundamento para módulos futuros ("Branches, fluxos e conflitos", segundo o painel).
