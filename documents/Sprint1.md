# Sprint 1

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

## 🧩 Sprint Backlog - Sprint 1

| ID       | Seção / Atividade                                                                 | Pontuação | Disciplina | Sprint | Requisito      |
|----------|-----------------------------------------------------------------------------------|-----------|------------|--------|----------------|
| **S1-01**  | INF-01.1 – Configurar repositório, estrutura de pastas e TypeScript               | 5         | ES         | 1      | INF-01         |
| **S1-02**  | INF-01.2 – Configurar Docker Compose (PostgreSQL, Backend, Frontend)              | 13        | ES         | 1      | INF-01         |
| **S1-03**  | BD-01.1 – Criar diagrama MER/DER do banco de dados                                | 8         | BD         | 1      | BD-01          |
| **S1-04**  | BD-01.2 – Criar extensão pgcrypto, enums e tabela `users` com migration           | 8         | BD         | 1      | BD-01          |
| **S1-05**  | BD-01.3 – Criar tabela `navigation_nodes` e migration                             | 5         | BD         | 1      | BD-01          |
| **S1-06**  | BD-01.4 – Criar tabelas `questions`, `interaction_logs`, `satisfaction_ratings`   | 8         | BD         | 1      | BD-01          |
| **S1-07**  | BD-01.5 – Mapear enums, índices e `updated_at` automático no Prisma               | 5         | BD         | 1      | BD-01          |
| **S1-08**  | RF01.1 – Criar endpoints GET de navegação (`/tree` e `/:slug`)                    | 8         | TP         | 1      | RF01           |
| **S1-09**  | RF02.1 – Criar endpoint GET de consulta ao repositório de conhecimento            | 5         | TP         | 1      | RF02           |
| **S1-10**  | RF03.1 – Criar endpoint `POST /auth/login` com geração de JWT                     | 13        | TP         | 1      | RF03 / RF09    |
| **S1-11**  | RF03.2 – Implementar hash de senha com bcrypt e variáveis de ambiente             | 5         | TP         | 1      | RF03 / RF09    |
| **S1-12**  | RF10.1 – Criar middlewares de autenticação JWT e autorização por role             | 8         | TP         | 1      | RF10 / RF11    |
| **S1-13**  | RF06.1 – Criar endpoints GET de perguntas (listagem e busca por ID)               | 5         | TP         | 1      | RF06           |
| **S1-14**  | INF-02.1 – Conectar Swagger ao backend e configurar Jest                          | 8         | TP         | 1      | INF-02         |
| **S1-15**  | ARQ-01.1 – Criar e entregar Diagrama de Casos de Uso                              | 8         | ES         | 1      | ARQ-01         |
| **S1-16**  | TESTE-02.1 – Teste unitário de RF09: Autenticar-se no sistema                     | 5         | TP         | 1      | TESTE-02       |
| **S1-17**  | TESTE-02.2 – Teste unitário de RF11: Validar token de acesso                      | 5         | TP         | 1      | TESTE-02       |

---

## Backlog de Gestão do Projeto

| ID       | Atividade                                                                                                                               | Pontuação | Disciplina | Sprint |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------|-----------|------------|--------|
| **G-01** | **Scrum Master:** Facilitar cerimônias ágeis (Daily, Planning, Review, Retrospective), acompanhar impedimentos, garantir comunicação eficaz e apoiar a equipe na aplicação do DoD. | 20        | ES         | 1      |
| **G-02** | **Product Owner:** Refinar e priorizar backlog, alinhar requisitos com stakeholders, validar entregas nas reviews e garantir clareza nos critérios de aceitação.                 | 20        | ES         | 1      |

---

## 📅 Distribuição de Atividades - Sprint 1

| Integrante                           | 10/abr | 24/abr | 27/abr | 28/abr | 30/abr              | 04/maio              | 05/maio |
|--------------------------------------|--------|--------|--------|--------|---------------------|---------------------|---------|
| **Victor Ramos (SM)**                | G-01   | G-01   | G-01   | G-01   | S1-01               | S1-02/S1-08         | G-01    |
| **Ricardo Ladeira (PO)**             | G-02   | G-02   | G-02   | G-02   | S1-15               | S1-01/S1-09         | G-02    |
| **Caio Julião**                      | S1-03  | S1-04  | S1-04  | S1-04  | S1-10/S1-11         | S1-10/S1-11         | S1-16   |
| **Jocelio Gomes Silva**              | S1-05  | S1-06  | S1-06  | S1-06  | S1-12               | S1-12               | S1-17   |
| **Lucas dos Santos Ribeiro**         | S1-07  | S1-13  | S1-13  | S1-13  | S1-14               | S1-14               | -       |
| **Luis Gustavo**                     | S1-15  | S1-15  | S1-15  | S1-15  | -                   | -                   | -       |

---

<!-- ## Sprint Burndown
<img src="./Burndown/Burndown_Sprint1.png" alt="Burndown Chart" width="700"/> -->

---

## 🔄 Retrospectiva da Sprint 1

O início da sprint foi marcado por um período de adaptação à metodologia **Scrum**, gerando desafios na organização e distribuição das atividades.  
Ao longo do processo, identificamos a necessidade de **estudos contínuos** sobre TypeScript, Docker, Prisma e autenticação JWT – tecnologias ainda não dominadas por parte da equipe.

Com o engajamento e colaboração de todos, superamos as dificuldades e aprimoramos a dinâmica de trabalho.  
O resultado foi extremamente positivo: todas as tasks foram concluídas com sucesso e o alinhamento com o Product Backlog foi mantido, garantindo a base sólida para as sprints seguintes.

---

## 📖 Legenda das Disciplinas

| Sigla | Disciplina                   |
|-------|------------------------------|
| ES    | Engenharia de Software       |
| TP    | Técnicas de Programação      |
| DW    | Desenvolvimento Web          |
| BD    | Banco de Dados relacional    |
