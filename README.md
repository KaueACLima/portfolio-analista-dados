# 📊 Pipeline de Dados — Projeto de Portfólio

Projeto ponta-a-ponta de engenharia/análise de dados, construído aos poucos, alimentado pelas práticas e desafios dos cursos e certificações que estou cursando em paralelo (Google Skills, Rocketseat). Não é um projeto isolado de portfólio "genérico" — cada etapa nasce de uma trilha de estudo real, versionada aqui desde a primeira linha.

## 🎯 Objetivo

Construir um pipeline de dados completo seguindo a **Arquitetura Medallion** (Bronze → Silver → Gold), do zero até um dashboard final, aplicando na prática o que cada frente de estudo ensina:

```
[Fonte de dado público] -> [Bronze: ingestão bruta] -> [Silver: limpeza/tratamento] -> [Gold: modelagem/agregação] -> [Dashboard/saída]
```

## 🗂️ Estrutura do repositório

```
├── 01-primeiros-passos-com-o-git/     # Resumos e prática do módulo introdutório de Git
├── 02-branches-fluxos-e-conflitos/    # (em andamento)
├── bronze/                            # Ingestão de dado público, ainda cru
├── silver/                            # Dados limpos e tratados
├── gold/                              # Dados modelados/agregados, prontos para análise
└── README.md
```

> As pastas `bronze/`, `silver/` e `gold/` nascem conforme o projeto avança — hoje o repositório ainda está na etapa de fundação (Git).

## 🚧 Status atual

| Estágio | Alimentado por | Status |
|---|---|---|
| Repo + README + versionamento | Git (módulo "Primeiros passos") | ✅ Concluído |
| Ingestão de dado público → Bronze | Python/Pandas + Coletando os Dados | ⬜ Não iniciado |
| Limpeza/transformação → Silver | Tratando os Dados + SQL | ⬜ Não iniciado |
| Modelagem/agregação → Gold | BigQuery (Data Engineer/ADP) | ⬜ Não iniciado |
| Dashboard/saída | Looker Studio / Power BI | ⬜ Não iniciado |

## 🛠️ Stack prevista

- **Versionamento:** Git/GitHub
- **Linguagem:** Python (Pandas, Numpy)
- **Banco de dados / SQL:** PostgreSQL
- **Cloud/Data Warehouse:** Google Cloud Platform (BigQuery)
- **Visualização:** Looker Studio e/ou Power BI

## 📚 Contexto de estudo

Este repositório acompanha minha jornada como Analista de Dados Júnior, estudando em paralelo:
- Google Skills — Associate Data Practitioner Certification
- Google Skills — Professional Data Engineer Certification
- Rocketseat — Formação Data Analytics
- Rocketseat — Banco de Dados (PostgreSQL)
- Rocketseat — Git e GitHub

Cada módulo concluído nessas trilhas que gera prática real (lab, desafio, projeto) alimenta uma etapa deste pipeline, em vez de ficar em arquivos soltos.

## 📝 Convenção de commits

```
docs(<curso-abreviado>): resumo aula - [Nome da Aula]
docs(<curso-abreviado>): fechamento do módulo - [Nome do Módulo]
```

---

*Última atualização: 21/09/2026 — módulo "Primeiros passos com o Git" concluído.*
