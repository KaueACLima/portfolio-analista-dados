# 📌 Iniciando um Repositório Local

### 1. Conceito Central
Esta aula mostra o primeiro passo prático de versionamento: transformar uma pasta comum do sistema operacional em um **repositório Git**. Até aqui, o Git só estava instalado e configurado na máquina — mas nenhuma pasta específica estava sendo rastreada por ele. O comando que faz essa transição é o `git init`, que inicializa o controle de versão *dentro* de uma pasta específica (o projeto), criando a estrutura interna que o Git usa para gerenciar commits e snapshots.

É importante notar a distinção feita na aula entre **repositório local** (existe só na sua máquina, não é visível para outras pessoas, não está na nuvem) e o que viria depois com o GitHub (hospedagem remota) — este é só o primeiro, o alicerce.

### 2. Pontos-chave e Sintaxe
- Enquanto uma pasta não é inicializada com `git init`, comandos de versionamento do Git (exceto o próprio `init`) retornam erro, porque o Git não a reconhece como um projeto rastreado. A mensagem de erro citada na aula é do tipo "fatal: não é um repositório do Git (ou não está dentro de um)".
- A partir do `git init`, é criada uma pasta oculta chamada `.git` dentro do projeto — essa pasta é onde o Git armazena toda a estrutura de versionamento (é ela que guarda o histórico, os commits, os snapshots). No macOS, é possível visualizar pastas ocultas no Finder com `Command + Shift + .`.

```bash
# Cria a pasta onde o projeto vai ficar
mkdir curso-git

# Entra na pasta criada
cd curso-git

# Confirma que o Git está instalado (visto em aulas anteriores)
git --version

# Antes do init: qualquer comando de versionamento falha
git commit -m "teste"
# -> erro: "fatal: não é um repositório do Git (ou não está dentro de um)"

# Inicializa o repositório Git dentro da pasta atual
git init
# -> "Iniciamos o repositório vazio do Git nesta pasta"

# Depois do init: o mesmo comando não gera mais erro
git commit -m "teste"
```
> A aula ainda não explica o que o `commit` faz de fato (mensagem, staging, etc.) — isso fica para as próximas aulas. Aqui ele aparece só como prova de que, após o `init`, o Git passa a aceitar comandos de versionamento na pasta.

- 💡 **Dica:** o comando `git init` não move nem apaga nada dos seus arquivos — ele só cria a pasta `.git` oculta, que é a "memória" do Git para aquele projeto. Por isso é seguro rodar em qualquer pasta que você queira começar a versionar.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Pasta comum no sistema operacional]
  -> Contém código do projeto, mas NÃO é rastreada pelo Git
  -> Tentativa de comando de versionamento (ex: git commit) -> [ERRO: "não é um repositório do Git"]

[git init executado na pasta]
  -> Cria a pasta oculta .git dentro do projeto
  -> [Repositório Git local] (agora existe estrutura de versionamento ali)
  -> Comandos de versionamento (ex: git commit) passam a funcionar sem erro
```

### 4. Links e Referências Oficiais
- **[Git — git-init](https://git-scm.com/docs/git-init)** — documentação oficial do comando usado nesta aula para criar o repositório local.
- **Repositório local** — termo usado na aula para diferenciar de repositório remoto/GitHub (que só é abordado em aulas futuras); não é uma ferramenta separada, é o conceito de um projeto versionado só na própria máquina.
- **Pasta `.git`** — estrutura interna criada pelo Git dentro do projeto ao rodar `git init`; a aula não detalha o conteúdo dela além de mencionar que é onde o versionamento "mora".
