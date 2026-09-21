📌 O que é Controle de Versão?
1. Conceito Central

Versionamento de software é o processo de rastrear e gerenciar as mudanças de um projeto ao longo do tempo, criando pontos de referência que permitem navegar entre diferentes momentos da história do código — saber o que mudou, quem mudou e quando. Isso é o que sustenta o trabalho em equipe sem sobrescrita de código, o histórico completo de alterações e a possibilidade de reverter mudanças problemáticas de forma rápida e consistente.

O Git é hoje a ferramenta dominante nesse espaço, mas é importante separar dois conceitos: controle de versão é a ideia geral (existem várias formas de fazer isso), e Git é uma implementação específica dessa ideia — a mais usada atualmente, mas não a única historicamente.

2. Pontos-chave e Sintaxe
Versionamento resolve quatro problemas centrais: colaboração em equipe (múltiplos devs trabalhando sem sobrescrever uns aos outros), histórico completo (quem alterou o quê e quando), recuperação de erros/rollback (voltar a um ponto anterior sem o bug) e experimentação segura (testar funcionalidades novas sem comprometer o código em produção — isso é feito via branches, conceito que a aula cita mas deixa para as próximas aulas aprofundar).
No Git, cada ponto do histórico é um snapshot (uma "fotografia" completa do estado do projeto naquele momento) — não apenas a diferença entre versões. Cada snapshot é chamado de commit.
Evolução histórica do controle de versões:
Anos 80 — RCS: versionava arquivo por arquivo, individualmente. Não escalava — um projeto com muitos arquivos gerava muitos históricos separados, tornando tudo lento.
Anos 90 — sistemas centralizados: já permitiam trabalho em equipe, mas dependiam de um único servidor central, o que tornava a colaboração lenta.
Anos 2000 — sistemas distribuídos (ex: BitKeeper): avanço em relação ao modelo centralizado, mas ainda lentos e pouco intuitivos.
2005 — Git: criado por Linus Torvalds (criador do Linux) para suprir a necessidade de um versionamento rápido e robusto no desenvolvimento do kernel Linux.
Objetivos que Linus Torvalds tinha ao criar o Git: velocidade (os sistemas anteriores eram lentos), simplicidade de uso e design, suporte robusto a desenvolvimento não-linear (branches), arquitetura distribuída, e capacidade de gerenciar projetos grandes sem perder performance.
Comparação de escala citada na aula: em sistemas anteriores, um projeto de ~15 mil linhas podia levar 20–30 minutos para gerar uma nova versão; com o Git, isso leva de 15 a 20 segundos (às vezes menos).
Toda versão no Git é verificada por um hash SHA-1, garantindo integridade — se os arquivos forem corrompidos, o Git detecta isso ao tentar lançar uma nova versão.
Números citados: 94% dos desenvolvedores usam Git como sistema primário de versionamento; o GitHub sozinho hospeda mais de 100 milhões de repositórios.
💡 Dica: o motivo do rollback ser tão rápido e confiável no Git é justamente porque cada commit é um snapshot completo — não é preciso reconstruir o estado do projeto a partir de uma sequência de diffs, basta "saltar" para a fotografia certa.
⚠️ Ponto de atenção: a aula (e o material de apoio) afirma que "o GitHub foi criado em 2005" — isso não corresponde à realidade (o GitHub foi fundado em 2008; 2005 é o ano de criação do Git, não do GitHub). Vale confirmar esse dado antes de levar para qualquer avaliação.
3. 🧭 Implicações Práticas
Como o Git guarda snapshots completos (não apenas diffs), reverter para qualquer ponto do histórico é praticamente instantâneo — isso muda a forma como equipes lidam com bugs em produção: em vez de "consertar correndo", dá pra reverter e investigar com calma.
A arquitetura distribuída (cada dev tem uma cópia completa do histórico) é o que permite que as operações sejam rápidas mesmo localmente, sem depender da rede — diferente dos sistemas centralizados antigos.
A verificação por hash SHA-1 significa que corrupção de dados é detectada automaticamente pelo próprio Git, sem precisar de checagem manual.
Rastreabilidade completa (quem fez o quê) é o que viabiliza um dos usos mais citados no mercado: entender a origem de um bug ou medir contribuição individual em um time.
4. Links e Referências Oficiais
Git — sistema de controle de versão distribuído, criado por Linus Torvalds em 2005; ferramenta central da aula.
GitHub — plataforma de hospedagem de repositórios Git na nuvem; a aula usa como exemplo o próprio ambiente da Rocketseat rodando em produção via Git.
RCS (Revision Control System) — sistema pioneiro dos anos 80, versionava arquivo por arquivo. Não encontrei uma doc oficial ativa e confiável para linkar; vale pesquisar se quiser mais contexto histórico.
CVS / Subversion (SVN) — sistemas centralizados dos anos 90, citados como etapa intermediária antes dos sistemas distribuídos.
BitKeeper — sistema distribuído dos anos 2000, citado como precursor direto que influenciou a criação do Git.