# 📌 Instalando e Configurando o Git (Windows, macOS, Linux)

### 1. Conceito Central
Depois de entender o que é o Git, o passo seguinte é colocá-lo pra funcionar na máquina. O processo se divide em duas etapas conceituais: **instalar** o Git no sistema operacional (o mecanismo muda conforme Windows, macOS ou Linux, mas o resultado é o mesmo — o binário do Git disponível em qualquer terminal) e **configurar a identidade** do usuário (nome + e-mail), que é o que o Git usa para registrar *quem* fez cada alteração em cada commit/snapshot.

#### Instalação no Windows
Baixa-se o instalador direto da documentação oficial do Git, escolhendo a arquitetura correta (64-bit, ARM64 ou 32-bit — verificável em "Informações do Sistema" do Windows, no campo "Tipo do sistema"). A instalação segue o padrão "next, next, next". Junto com o Git, vem o **Git Bash**, um terminal instalado especificamente para rodar comandos Git.

#### Instalação no macOS
O Mac tem três caminhos possíveis:
- **Xcode** (editor de código da Apple, focado em desenvolvimento com Swift para o ecossistema Apple) — instala o Git como parte do pacote, mas só vale a pena se você já for usar o Xcode por outro motivo.
- **Download direto** pela documentação oficial (inclui opção via binário).
- **Homebrew** (gerenciador de pacotes usado em Mac e Linux para instalar ferramentas e projetos), que foi o caminho demonstrado na aula:
```bash
# Instala o Git via Homebrew
brew install git
```

#### Instalação no Linux
Varia conforme a distribuição:
```bash
# Distribuições baseadas em Debian (ex: Ubuntu) — usando apt-get
sudo apt-get install git -y
```
A documentação oficial também traz comandos equivalentes para Fedora (RPM), Mageia, openSUSE e Arch Linux — o pacote muda, mas a lógica é a mesma: usar o gerenciador de pacotes nativo da distro.

#### Verificando a instalação (qualquer SO)
```bash
# Retorna a versão do Git instalada — se aparecer uma versão, deu certo
git --version
```
Esse comando funciona em qualquer terminal (padrão do SO, terminal customizado como iTerm2, ou integrado ao editor de código), porque a instalação do Git é feita na máquina como um todo, não em uma ferramenta isolada.

#### Configurando usuário (nome e e-mail)
Depois de instalar, é necessário configurar identidade para que os commits carreguem quem fez a alteração:
```bash
# Configuração global — vale para todos os repositórios da máquina
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"

# Para ver o que está configurado:
git config user.name
```
Se a flag `--global` for omitida, a configuração vale **só para a pasta/repositório atual** (útil pra separar identidade pessoal de identidade de trabalho, por exemplo) — mas isso só funciona se o comando for rodado dentro de um repositório Git já iniciado.

### 2. Pontos-chave e Sintaxe
- 💡 **Dica:** o comando `git --version` é o teste universal de que a instalação funcionou — independente do sistema operacional ou do terminal usado.
- ⚠️ **Ponto de atenção:** a diferença entre `git config --global user.name` e `git config user.name` (sem `--global`) é o escopo — global afeta todos os projetos da máquina, local afeta só o repositório atual. Confundir os dois pode fazer commits saírem com a identidade errada.

### 3. 🧭 Implicações Práticas
- Como o Git é instalado na máquina como um todo, ele fica acessível de qualquer terminal e também via integração com editores de código — não é preciso reinstalar por ferramenta.
- A configuração global de nome/e-mail é o que garante que **todo** commit feito na máquina, em qualquer projeto, carregue a mesma identidade — importante lembrar disso antes de configurar, especialmente se a máquina for compartilhada entre contextos diferentes (pessoal/trabalho).
- Cada sistema operacional tem seu próprio gerenciador de instalação (instalador gráfico no Windows, Homebrew/Xcode no Mac, gerenciador de pacotes nativo no Linux), mas o comando de verificação (`git --version`) e o de configuração (`git config`) são idênticos entre eles — o Git abstrai a diferença de plataforma depois de instalado.

### 4. Links e Referências Oficiais
- **[Git — Downloads oficiais](https://git-scm.com/downloads)** — página oficial com instaladores para Windows, Mac e Linux, citada como fonte em todas as aulas.
- **Homebrew** — gerenciador de pacotes usado no Mac (e Linux) para instalar o Git com um único comando; não tenho certeza de uma URL oficial estável específica pra linkar aqui, vale buscar `brew.sh`.
- **Xcode** — editor de código da Apple citado como uma das formas de obter o Git no macOS (via App Store), mas fora de escopo se você não desenvolve para o ecossistema Apple.
- Documentações específicas da Rocketseat linkadas por você:
  - [Instalação — Windows](https://efficient-sloth-d85.notion.site/Windows-ad987bb4e40245fabb27c8d4fd80e8a2)
  - [Instalação — Linux](https://efficient-sloth-d85.notion.site/Linux-50a64d714418496ea199cab4eb719756)
  - [Instalação — Mac](https://efficient-sloth-d85.notion.site/Mac-145ab38e79dc4d3fa7f2ec24c8e85cc1)
