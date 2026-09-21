# 📌 Ciclo de Vida dos Arquivos no Git

### 1. Conceito Central
Todo arquivo dentro de um projeto versionado pelo Git passa por três estados possíveis: **Working Directory** (diretório de trabalho — onde você edita os arquivos no seu editor de código, refletindo o estado atual do repositório com as alterações feitas desde o último commit), **Staging Area** (área de preparação — onde você seleciona quais alterações específicas vão entrar na próxima versão, sem ainda tê-las versionado) e **Commit** (o histórico propriamente dito — o registro definitivo daquilo que estava em staging, agora confirmado como uma nova versão/snapshot do projeto).

Esse fluxo de três etapas é o coração de como o Git trabalha: você não versiona tudo de uma vez de forma automática — você escolhe o que vai para a próxima versão (staging), e só depois confirma essa versão (commit).

### 2. Pontos-chave e Sintaxe
- **Working Directory:** reflete o estado atual dos arquivos na sua máquina. Se for o primeiro commit do projeto, ele começa vazio; a partir do segundo, reflete as alterações em relação aos commits anteriores. Editar, remover ou atualizar um arquivo aparece aqui primeiro.
- **Staging Area:** é o "pré-commit" — arquivos são movidos do diretório de trabalho para cá usando `git add`, indicando que vão entrar na próxima versão, mas ainda não foram de fato versionados.
- **Commit:** é a confirmação de uma alteração (arquivo novo, funcionalidade adicionada, funcionalidade removida). Cada commit tem:
  - um **hash único**, gerado automaticamente pelo motor do Git, garantindo que não existam dois commits com o mesmo identificador;
  - uma **mensagem de commit**, escrita por quem versiona, descrevendo o que foi feito;
  - **metadados automáticos**: autor da alteração (vindo da configuração `user.name`/`user.email` feita em aula anterior) e a data/hora do commit.

```bash
# Marca arquivos específicos (ou todos, com o ponto) para irem no próximo commit
git add .

# Confirma a versão com uma mensagem descritiva
git commit -m "descrição breve da alteração"
```

- 🔎 **Observação:** o Git não guarda cópias completas do projeto a cada commit — ele identifica **apenas o que mudou** desde a versão anterior. Arquivos que não sofreram alteração são simplesmente referenciados/citados da versão anterior, e não duplicados.
- ⚠️ **Ponto de atenção (o "segredo de ouro" da aula):** para o Git, a identidade de um arquivo é o nome + a pasta onde ele está. Isso significa que **renomear um arquivo** ou **movê-lo de pasta** não é entendido como uma "alteração" no sentido comum — o Git interpreta isso como **apagar o arquivo antigo e criar um arquivo novo**. Por isso é comum ver um arquivo marcado como "apagado" no status do Git mesmo sem ter apagado nada de fato — só foi renomeado ou movido.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Working Directory] -> arquivo criado/editado/removido
        |
        v (git add)
[Staging Area] -> arquivo selecionado para entrar na próxima versão
        |
        v (git commit -m "mensagem")
[Commit / Histórico] -> snapshot confirmado, com hash único + autor + data + mensagem
```

**Caso especial — renomear/mover arquivo:**
```
[Arquivo "sobre.css" existente no projeto]
  -> Renomeado para "novo_sobre.css" ou movido de pasta
  -> Git identifica pelo nome+pasta, não pelo conteúdo
  -> SIM (nome/pasta mudou): [arquivo antigo marcado como apagado] + [arquivo novo marcado como criado]
```

**Exemplo de progressão de versões citado na aula:**
```
[Pasta vazia (git init)]
  -> Cria index.html, script.js, style.css (arquivos novos)
  -> git add + git commit -> [V1: 3 arquivos versionados]
  -> Altera index.html, apaga script.js, cria 3 arquivos novos (página "sobre")
  -> git add + git commit -> [V2: 5 arquivos — script.js removido, 3 novos incluídos, index.html alterado]
```

### 4. Links e Referências Oficiais
- **[Git — git-add](https://git-scm.com/docs/git-add)** — documentação oficial do comando usado para mover arquivos do diretório de trabalho para a staging area.
- **[Git — git-commit](https://git-scm.com/docs/git-commit)** — documentação oficial do comando usado para confirmar uma versão a partir do que está em staging.
- **Working Directory, Staging Area, Commit** — os três estados centrais do fluxo de trabalho do Git explicados na aula; não são ferramentas separadas, são conceitos internos do próprio Git (cobertos na documentação oficial acima).
- **Hash (SHA)** — identificador único gerado para cada commit, citado na aula como parte do "funcionamento por debaixo dos panos" do Git; já mencionado com mais detalhe na primeira aula do módulo (verificação de integridade via SHA-1).
