# Sprint 1

> **Epic:** [E06] Execução, documentação e avaliação de usabilidade #6 — [E06] Qualidade, documentação e avaliação  
> **Feature:** [F06.1] Documentação das sprints 1, 2 e 3 #52 — [F06.1] Documentação das sprints 1, 2 e 3  
> **RF:** RNF08, RP01–RP09  
> **Sprint:** 1  
> **Prioridade:** P1  
> **Área:** docs

---

## 📅 Período da Sprint 1

| Campo | Valor |
|-------|-------|
| Início | 27/03/2026 (kick-off) |
| Término | 04/05/2026 |

> **Nota:** O período foi confirmado no board do GitHub Projects e consta no README do repositório (`documents/Sprint1.md` indica entrega em 04/05/2026).

---

## 🎯 Objetivo da Sprint 1

Entregar a **base do backend** do chatbot de autoatendimento da Secretaria Acadêmica da FATEC Jacareí, incluindo:

- Configuração do ambiente de desenvolvimento com Docker, TypeScript e repositório padronizado.
- Modelagem e criação do banco de dados (PostgreSQL) com todas as tabelas, enums e índices via Prisma.
- Implementação dos endpoints iniciais:
  - Navegação conversacional (GET `/tree` e `/:slug`).
  - Consulta ao repositório de conhecimento (GET).
  - Autenticação com JWT (`POST /auth/login`) e hash de senha com bcrypt.
  - Middlewares de RBAC e proteção de rotas.
  - Gestão de perguntas (GET para Secretária Acadêmica).
- Configuração do Swagger e Jest para documentação e testes.
- Elaboração do Diagrama de Casos de Uso (UML).
- Testes unitários de autenticação e validação de token.

---

## 🧩 Itens Planejados (Sprint Backlog)

| ID | Atividade | Pontuação | Disciplina | Requisito |
|----|-----------|-----------|------------|-----------|
| S1-01 | INF-01.1 – Configurar repositório, estrutura de pastas e TypeScript | 5 | ES | INF-01 |
| S1-02 | INF-01.2 – Configurar Docker Compose (PostgreSQL, Backend, Frontend) | 13 | ES | INF-01 |
| S1-03 | BD-01.1 – Criar diagrama MER/DER do banco de dados | 8 | BD | BD-01 |
| S1-04 | BD-01.2 – Criar extensão pgcrypto, enums e tabela `users` com migration | 8 | BD | BD-01 |
| S1-05 | BD-01.3 – Criar tabela `navigation_nodes` e migration | 5 | BD | BD-01 |
| S1-06 | BD-01.4 – Criar tabelas `questions`, `interaction_logs`, `satisfaction_ratings` | 8 | BD | BD-01 |
| S1-07 | BD-01.5 – Mapear enums, índices e `updated_at` automático no Prisma | 5 | BD | BD-01 |
| S1-08 | RF01.1 – Criar endpoints GET de navegação (`/tree` e `/:slug`) | 8 | TP | RF01 |
| S1-09 | RF02.1 – Criar endpoint GET de consulta ao repositório de conhecimento | 5 | TP | RF02 |
| S1-10 | RF03.1 – Criar endpoint `POST /auth/login` com geração de JWT | 13 | TP | RF03 / RF09 |
| S1-11 | RF03.2 – Implementar hash de senha com bcrypt e variáveis de ambiente | 5 | TP | RF03 / RF09 |
| S1-12 | RF10.1 – Criar middlewares de autenticação JWT e autorização por role | 8 | TP | RF10 / RF11 |
| S1-13 | RF06.1 – Criar endpoints GET de perguntas (listagem e busca por ID) | 5 | TP | RF06 |
| S1-14 | INF-02.1 – Conectar Swagger ao backend e configurar Jest | 8 | TP | INF-02 |
| S1-15 | ARQ-01.1 – Criar e entregar Diagrama de Casos de Uso | 8 | ES | ARQ-01 |
| S1-16 | TESTE-02.1 – Teste unitário de RF09: Autenticar-se no sistema | 5 | TP | TESTE-02 |
| S1-17 | TESTE-02.2 – Teste unitário de RF11: Validar token de acesso | 5 | TP | TESTE-02 |

---

## ✅ Itens Entregues

Todos os itens planejados da Sprint Backlog foram concluídos com sucesso.

| ID | Atividade | Status | Evidência |
|----|-----------|--------|-----------|
| S1-01 | Configurar repositório, estrutura e TypeScript | ✅ | Commit `53c095c` / `f8c2133` (frontend), `479d169` (gitmodules) |
| S1-02 | Docker Compose (PostgreSQL, Backend, Frontend) | ✅ | PR #37 `feat/ajustem_docker_compose` ([#37](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/37)) |
| S1-03 | Diagrama MER/DER | ✅ | `documents/modelagem_bd.md` |
| S1-04 | pgcrypto, enums, tabela `users` | ✅ | PR #35 `feat/migrabancodedados` ([#35](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/35)) |
| S1-05 | Tabela `navigation_nodes` | ✅ | PR #35 (migration de banco) |
| S1-06 | Tabelas `questions`, `interaction_logs`, `satisfaction_ratings` | ✅ | PR #35 (migration de banco) |
| S1-07 | Enums, índices, `updated_at` no Prisma | ✅ | Prisma schema no backend |
| S1-08 | Endpoints GET navegação (`/tree`, `/:slug`) | ✅ | PR #39 `feat(navigation)` ([#39](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/39)) |
| S1-09 | GET repositório de conhecimento | ✅ | PR #39 (endpoints GET) |
| S1-10 | `POST /auth/login` com JWT | ✅ | PR #46 `pr/auth-token-bootstrap` ([#46](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/46)) |
| S1-11 | Hash de senha com bcrypt + env | ✅ | PR #46 (JWT + bcrypt) |
| S1-12 | Middlewares JWT + RBAC | ✅ | PR #46 (auth middleware) |
| S1-13 | GET perguntas (listagem e busca por ID) | ✅ | Backend `src/controllers/` |
| S1-14 | Swagger + Jest | ✅ | PR #46 (swagger docs), PR #39 (vitest) |
| S1-15 | Diagrama de Casos de Uso | ✅ | `documents/uml.md` |
| S1-16 | Teste RF09: Autenticação | ✅ | `backend/tests/` (vitest + supertest) |
| S1-17 | Teste RF11: Validar token | ✅ | `backend/tests/` (vitest + supertest) |

---

## 📋 RFs e RNFs Cobertos

| Requisito | Descrição | Status | Evidência |
|-----------|-----------|--------|-----------|
| **RF01** | Navegação conversacional (GET `/tree` e `/:slug`) | ✅ | PR #39, `src/controllers/` |
| **RF02** | Consulta ao repositório de conhecimento (GET) | ✅ | PR #39, `src/controllers/` |
| **RF03** | Autenticação com JWT (`POST /auth/login`) | ✅ | PR #46, `src/controllers/auth/` |
| **RF06** | Gestão de perguntas (GET listagem e busca por ID) | ✅ | `src/controllers/get-user` e relacionados |
| **RF09** | Hash de senha com bcrypt | ✅ | PR #46, `bcrypt` no `package.json` |
| **RF10** | Middleware de autenticação JWT | ✅ | PR #46, `src/middlewares/` |
| **RF11** | Validação de token de acesso | ✅ | PR #46, `src/middlewares/` |
| **BD-01** | Modelagem e criação do banco (PostgreSQL + Prisma) | ✅ | PR #35, `prisma/` |
| **INF-01** | Ambiente Docker Compose | ✅ | PR #37, `docker-compose.yml` |
| **INF-02** | Swagger + Jest | ✅ | PR #46 (swagger), PR #39 (vitest) |
| **ARQ-01** | Diagrama de Casos de Uso | ✅ | `documents/uml.md` |
| **RNF08** | Documentação técnica | ✅ | Este documento + `README.md` |
| **RP01** | Frontend React + TypeScript | ⚠️ | Frontend configurado (submódulo), pendente integração total |
| **RP02** | Backend NestJS/Express + TypeScript | ✅ | `backend/` com Express + TypeScript |
| **RP03** | PostgreSQL + Prisma ORM | ✅ | `prisma/` + migrations |
| **RP04** | Separação de responsabilidades | ✅ | `src/controllers/`, `src/repositories/`, `src/core/` |
| **RP05** | Execução containerizada | ✅ | `docker-compose.yml` |
| **RP06** | MVP funcional | ✅ | Backend com autenticação e navegação |
| **RP07** | Autenticação JWT | ✅ | PR #46 |

> **Nota:** Nenhum RF é afirmado como concluído sem link de código, PR ou teste associado.

---

## 🔗 PRs e Issues Relacionadas

### Pull Requests (Backend)

| PR | Título | Status | Link |
|----|--------|--------|------|
| #35 | feat: adicionando post de naviation_logs | Merged | [#35](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/35) |
| #36 | feat: apagando arquivos nao usados | Merged | [#36](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/36) |
| #37 | feat: carregar migration do prisma | Merged | [#37](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/37) |
| #39 | feat(navigation): add concise create and chatbot get endpoints | Merged | [#39](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/39) |
| #46 | feat(auth): add JWT auth with first-user bootstrap and swagger docs | Merged | [#46](https://github.com/devmaster-organizations/backend_abp_autoatendimento/pull/46) |

### Pull Requests (Frontend)

| PR | Título | Status | Link |
|----|--------|--------|------|
| #1 | ajustando front | Merged | [#1](https://github.com/devmaster-organizations/frontend_abp_autoatentimento/pull/1) |
| #2 | Merge branch 'main' into luis | Merged | [#2](https://github.com/devmaster-organizations/frontend_abp_autoatentimento/pull/2) |
| #3 | Criação da Tela de introdução | Merged | [#3](https://github.com/devmaster-organizations/frontend_abp_autoatentimento/pull/3) |
| #4 | Mudança de aparencia do chatbot | Merged | [#4](https://github.com/devmaster-organizations/frontend_abp_autoatentimento/pull/4) |

### Issues

| Issue | Título | Status | Link |
|-------|--------|--------|------|
| — | (nenhuma issue vinculada à Sprint 1 encontrada) | — | — |

> **Nota:** Os links de PR foram verificados nos remotos do backend e frontend. Todos apontam para o GitHub da organização `devmaster-organizations`.

---

## 📊 Evidências

### Comandos de verificação

```bash
# Verificar se o ambiente sobe
docker compose up --build

# Verificar saúde do banco
docker compose exec postgres pg_isready -U postgres -d autoatendimento

# Rodar testes do backend
cd backend
npm test

# Verificar build do TypeScript
npm run build
```

### Testes existentes

O backend utiliza **Vitest + Supertest** para testes de API. Os testes cobrem:
- Autenticação (RF09 / TESTE-02.1)
- Validação de token (RF11 / TESTE-02.2)

```bash
cd backend
npm test
```

### Links de código

- [Backend no GitHub](https://github.com/devmaster-organizations/backend_abp_autoatendimento)
- [Frontend no GitHub](https://github.com/devmaster-organizations/frontend_abp_autoatentimento)
- [Infra (compose, docs) no GitHub](https://github.com/devmaster-organizations/infra-autoatendimento)

---

## ⚠️ Pendências

| Item | Descrição | Motivo |
|------|-----------|--------|
| Frontend integrado com backend | O frontend está configurado como submódulo, mas a integração completa com a API ainda está em andamento | Sprint 2 |
| Deploy da aplicação | Não realizado na Sprint 1 | Planejado para Sprint 2 (INF-03) |
| Fluxo de recuperação de senha | Não implementado | Planejado para Sprint 2 (RF09.2) |
| Diagrama de Classes (UML) | Não entregue | Planejado para Sprint 2 (ARQ-02) |
| Testes de integração completos | Apenas testes unitários de auth e token | Cobertura parcial |

---

## 🔄 Retrospectiva da Sprint 1

### O que funcionou

- A equipe conseguiu configurar o ambiente base (Docker Compose + TypeScript + Prisma) rapidamente.
- A modelagem do banco de dados com Prisma e pgcrypto foi entregue conforme planejado.
- A autenticação com JWT e bcrypt foi implementada com testes (Vitest + Supertest).
- O uso de submódulos Git permitiu separar backend e frontend com clareza.
- A documentação (README, diagramas UML, modelagem BD) foi mantida atualizada.

### O que melhorar

- A divisão de tarefas entre desenvolvedores poderia ser mais equilibrada (alguns membros ficaram sobrecarregados).
- O frontend ficou com pouca entrega na Sprint 1; maior integração entre frontend e backend é necessária na próxima sprint.
- Não houve burndown chart visível para acompanhamento do progresso da sprint.
- Os PRs poderiam ter revisões mais formais antes do merge.

---

## 📖 Legenda das Disciplinas

| Sigla | Disciplina |
|-------|------------|
| ES | Engenharia de Software |
| TP | Técnicas de Programação |
| DW | Desenvolvimento Web |
| BD | Banco de Dados relacional |
