# 📌 Visualizando o que Mudou no Código com git diff

### 1. Conceito Central
O `git diff` é o comando que mostra **diferenças entre estados do projeto** — ele revela exatamente o que mudou (linhas adicionadas, removidas, alteradas) entre dois pontos de referência. As comparações mais úteis no dia a dia são: Working Directory (o código que você está editando, ainda não commitado) contra o último commit; Staging Area (arquivos já preparados com `git add`) contra o último commit; e commit A contra commit B (comparando duas versões específicas do histórico).

O ponto central da aula é entender que o `git diff`, sem parâmetros, sempre olha para o Working Directory — e que existe uma flag específica para olhar para a Staging Area em vez disso. Sem entender essa distinção, é fácil rodar o comando e concluir erroneamente que "não mudou nada", quando na verdade a mudança só migrou de estado (de working directory para staging).

### 2. Pontos-chave e Sintaxe
```bash
# Compara o Working Directory com o último commit (uso padrão, sem flags)
git diff

# Compara a Staging Area (arquivos já preparados com git add) com o último commit
git diff --cached
# (equivalente, também citado na aula:)
git diff --staged

# Compara dois commits específicos entre si, usando os hashes
git diff <hash-commit-A> <hash-commit-B>
```
- Se um arquivo tem mudanças tanto no Working Directory quanto na Staging Area (por exemplo, parte do conteúdo já foi adicionada com `git add`, e depois mais alterações foram feitas por cima), o `git diff` sem flag mostra **só** as mudanças que ainda estão fora da staging area — não o total.
- Depois de mover tudo para a staging area com `git add`, o `git diff` (sem flag) não mostra mais nada, porque não há mais mudanças "soltas" no Working Directory — nesse caso, é preciso usar `--staged`/`--cached` para ver o que está pronto pra commit.
- Ao comparar commits diretamente (`git diff <hashA> <hashB>`), o resultado mostra as diferenças de conteúdo entre as duas versões — útil para investigar o que mudou entre pontos específicos do histórico.
- 💡 **Dica:** o `git diff` pode ser combinado com o `git blame` (comando que mostra, linha por linha de um arquivo, quem foi a última pessoa a alterar aquela linha) para investigar mudanças de forma mais profunda — por exemplo, ao revisar código de outra pessoa ou investigar a origem de um bug.
- 🔎 **Observação:** a aula lista três casos de uso centrais para o `git diff` no dia a dia: (1) revisar o próprio código antes de commitar, (2) revisar código de outra pessoa (em conjunto com `git blame`), e (3) revisar código gerado por IA antes de commitar — já que uma IA pode "querer" commitar direto sem que o desenvolvedor tenha, de fato, lido a mudança.

### 3. 🧠 Raciocínio Lógico
- `git diff` (sem flag) sempre compara: **Working Directory → último commit**, mostrando apenas o que está fora da staging area.
- `git diff --cached` (ou `--staged`) compara: **Staging Area → último commit**, mostrando o que já está preparado para o próximo commit.
- `git diff <hashA> <hashB>` ignora o estado atual do projeto e compara diretamente dois pontos do histórico entre si.
- Se um arquivo tem parte do conteúdo em staging e parte ainda solta no working directory, cada modo do `git diff` mostra apenas a "fatia" correspondente ao estado que está analisando — nunca as duas juntas.

### 4. Links e Referências Oficiais
- **[Git — git-diff](https://git-scm.com/docs/git-diff)** — documentação oficial do comando central desta aula, incluindo as flags `--cached`/`--staged`.
- **[Git — git-blame](https://git-scm.com/docs/git-blame)** — documentação oficial do comando citado como complemento ao `git diff` para investigar autoria linha a linha.