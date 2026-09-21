# 📌 Criando e alternando entre branches

### 1. Conceito Central
Esta aula mostra, na prática do terminal, como criar branches, alternar entre elas e integrar (merge) o trabalho de uma branch em outra. O ponto central é entender que uma branch nova **herda** todos os commits da branch em que você estava no momento da criação — ela não começa "vazia". A partir daí, cada branch guarda seu próprio histórico de commits de forma isolada: um commit feito numa branch só existe nela até que seja explicitamente integrado (merge) em outra.

### 2. Pontos-chave e Sintaxe
- `git branch` sem argumento **lista** as branches existentes e indica em qual você está no momento.
- `git branch <nome>` **cria** uma nova branch, mas não muda para ela automaticamente.
- Convenção de nomenclatura de mercado usada na aula: `feature/nome-da-funcionalidade` (ex.: `feature/login-with-email-and-password`).
- **Checkout** é o processo de trocar de branch (`git checkout <nome>`).
- Uma branch nova nasce com todos os commits da branch de origem — por isso, ao trocar para ela logo após criá-la, o histórico (`git log`) é idêntico ao da branch original.
- O fluxo de commit **dentro** de uma branch é igual ao fluxo sem branches: `git add` seguido de `git commit`.
- Um commit feito numa branch fica isolado nela: ao voltar para a branch original (ex.: `main`), esse commit não aparece no `git log`.
- **Merge**: para integrar as mudanças de uma branch em outra, é preciso primeiro fazer checkout para a branch que vai **receber** a mudança, e só então rodar `git merge <branch-de-origem>`.
- ⚠️ **Ponto de atenção:** o professor levanta a questão de escalabilidade — se um projeto acumula, por exemplo, 120 features, ter 120 branches soltas não é sustentável. Esse problema (boas práticas de merge e organização de branches) será o foco da próxima aula.

```bash
# Lista todas as branches e mostra em qual você está
git branch

# Cria uma nova branch (não muda para ela)
git branch feature/login-with-email-and-password

# Troca (checkout) para a branch criada
git checkout feature/login-with-email-and-password

# Fluxo de commit normal, agora dentro da branch
git add .
git commit -m "login with email and password"

# Para integrar (merge) a feature na main:
git checkout main                                  # 1. vá para quem VAI RECEBER a mudança
git merge feature/login-with-email-and-password     # 2. traga as mudanças da outra branch
```

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[main] -> git branch feature/login-with-email-and-password
       -> [feature/x criada, herda commits da main; você continua na main]

[main] -> git checkout feature/x
       -> [você está em feature/x]
       -> git add . / git commit -> [commit exclusivo de feature/x, não existe na main]

[feature/x] -> git checkout main
       -> [você volta pra main; commit de feature/x não aparece no log aqui]

[main] -> git merge feature/x
       -> [main recebe os commits de feature/x; as duas branches ficam com o mesmo histórico]
```

### 4. Links e Referências Oficiais
- **git branch** — cria, lista ou apaga branches. Documentação: [git-scm.com/docs/git-branch](https://git-scm.com/docs/git-branch)
- **git checkout** — alterna entre branches (ou restaura arquivos, a depender do uso). Documentação: [git-scm.com/docs/git-checkout](https://git-scm.com/docs/git-checkout)
- **git merge** — integra o histórico de uma branch em outra. Documentação: [git-scm.com/docs/git-merge](https://git-scm.com/docs/git-merge)
- **git add / git commit** — fluxo de staging e commit, já visto no módulo anterior.
