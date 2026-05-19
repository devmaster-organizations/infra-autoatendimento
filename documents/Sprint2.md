# Sprint 2

## 🎯 Objetivo da Sprint 2

Implementar a camada completa de serviços e regras de negócio do chatbot, incluindo a gestão dinâmica de conteúdo pelo Administrador, o registro do fluxo de navegação, o encaminhamento de perguntas à Secretaria Acadêmica e a coleta de avaliação de satisfação.

Além disso, construir a interface funcional do chatbot (frontend) integrada à API, a tela de autenticação para usuários administrativos e a proteção de rotas no frontend.

**Entregas principais:**

  * CRUD completo de nós de navegação (endpoints GET, POST, PUT, PATCH, DELETE).

  * CRUD de usuários e gestão de documentos oficiais (Administrador).

  * Endpoints de envio de perguntas, atualização de status e vinculo de responsável (Secretária Acadêmica).

  * Registro de logs de navegação e avaliação de satisfação.

  * Fluxo de recuperação de senha.

  * Deploy da aplicação (frontend + backend).

  * Interface do chatbot responsiva com navegação por menus, evidências documentais e formulário de dúvidas.

  * Tela de login e proteção de rotas no frontend.

  * Diagrama de Classes (UML).

  * Testes unitários referentes às funcionalidades do aluno, secretária e navegação.

---

## 🧩 Sprint Backlog - Sprint 2

| ID       | Seção / Atividade                                                                 | Pontuação | Disciplina | Sprint | Requisito      |
|----------|-----------------------------------------------------------------------------------|-----------|------------|--------|----------------|
| **RF04.1**  | Criar endpoints GET de nós de navegação (listagem e busca por ID)                 |           | TP         | 2      | RF04           |
| **RF04.2**  | Criar endpoints GET de usuários (listagem e busca por ID)                         |           | TP         | 2      | RF04           |
| **RF04.3**  | Criar endpoint GET de logs de navegação (listagem administrativa)                 |           | TP         | 2      | RF04           |
| **RF01.2**  | Criar endpoints POST e PUT de nós de navegação (cadastro e edição)                |           | TP         | 2      | RF01           |
| **RF01.3**  | Criar endpoints PATCH de status e DELETE de nós de navegação                      |           | TP         | 2      | RF01           |
| **RF01.4**  | Popular banco com seed dos dados iniciais fornecidos pelo cliente                 |           | BD         | 2      | RF01           |
| **RF04.4**  | Criar endpoints POST, PUT e DELETE de usuários                                    |           | TP         | 2      | RF04           |
| **RF04.5**  | Criar endpoints POST e PUT de documentos oficiais                                 |           | TP         | 2      | RF04           |
| **RF09.2**  | Implementar fluxo de recuperação de senha                                         |           | TP         | 2      | RF09           |
| **INF-03.1**| Realizar o deploy da aplicação (Frontend e Backend)                               |           | DW         | 2      | INF-03         |
| **RF05.1**  | Criar endpoint `POST /questions` (texto da dúvida e e-mail institucional)         |           | TP         | 2      | RF05           |
| **RF06.2**  | Criar endpoint `PATCH /questions/:id/status` (em aberto / respondida)             |           | TP         | 2      | RF06           |
| **RF06.3**  | Criar endpoint `PATCH /questions/:id/assign` (vincular responsável)               |           | TP         | 2      | RF06           |
| **RF07.1**  | Criar endpoint `POST /sessions/:id/satisfaction` (Gostei / Não gostei)            |           | TP         | 2      | RF07           |
| **RF08.1**  | Criar endpoint `POST /logs` (abertura de log de interação)                        |           | TP         | 2      | RF08           |
| **RF08.2**  | Criar endpoint `PATCH /logs/:sessionId/navigation` (atualizar fluxo de navegação) |           | TP         | 2      | RF08           |
| **RF08.3**  | Criar endpoint `PATCH /logs/:sessionId/question` (associar solicitação à sessão)  |           | TP         | 2      | RF08           |
| **FE-01.1** | Criar layout e componente de chat (bolhas, opções, scroll automático)            |           | DW         | 2      | RP01 / RNF01   |
| **FE-01.2** | Implementar fluxo de navegação no frontend consumindo a API de nós                |           | DW         | 2      | RP01 / RNF01   |
| **FE-01.3** | Implementar exibição de trecho de evidência documental ao final da navegação      |           | DW         | 2      | RP01 / RNF01   |
| **FE-01.4** | Implementar formulário de envio de pergunta à secretaria (texto + e-mail)         |           | DW         | 2      | RP01 / RNF01   |
| **FE-02.1** | Criar tela de login para Administrador e Secretária Acadêmica                     |           | DW         | 2      | RP01           |
| **FE-02.2** | Implementar proteção de rotas no frontend (redirecionar não autenticados)         |           | DW         | 2      | RP01           |
| **ARQ-02.1**| Criar e entregar Diagrama de Classes                                              |           | ES         | 2      | ARQ-02         |
| **TESTE-01.1** | Teste unitário de RF01: Navegar por menus conversacionais                     |           | TP         | 2      | TESTE-01       |
| **TESTE-01.2** | Teste unitário de RF02: Consultar repositório de conhecimento                 |           | TP         | 2      | TESTE-01       |
| **TESTE-03.1** | Teste unitário de RF05: Enviar pergunta à secretaria                          |           | TP         | 2      | TESTE-03       |
| **TESTE-03.2** | Teste unitário de RF07: Registrar avaliação de satisfação                    |           | TP         | 2      | TESTE-03       |
| **TESTE-03.3** | Teste unitário de RF08: Registrar log de navegação                           |           | TP         | 2      | TESTE-03       |
| **TESTE-04.1** | Teste unitário de RF06: Listar perguntas recebidas                           |           | TP         | 2      | TESTE-04       |
| **TESTE-04.2** | Teste unitário de RF06: Atualizar status de pergunta                         |           | TP         | 2      | TESTE-04       |

---

## Backlog de Gestão do Projeto

| ID       | Atividade                                                                                                                               | Pontuação | Disciplina | Sprint |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------|-----------|------------|--------|
| **G-01** | **Scrum Master:** Facilitar cerimônias ágeis (Daily, Planning, Review, Retrospective), acompanhar impedimentos, garantir comunicação eficaz e apoiar a equipe na aplicação do DoD. | 20        | ES         | 2      |
| **G-02** | **Product Owner:** Refinar e priorizar backlog, alinhar requisitos com stakeholders, validar entregas nas reviews e garantir clareza nos critérios de aceitação.                 | 20        | ES         | 2      |

---

## 📅 Distribuição de Atividades - Sprint 2

| Integrante                           | 08/maio | 12/maio | 15/maio | 18/maio | 19/maio    | 22/maio              |
|--------------------------------------|--------|--------|--------|--------|---------------------|---------------------|
| **Victor Ramos (SM)**                | G-01   | G-01   | G-01   | G-01   |         |                     | 
| **Ricardo Ladeira (PO)**             | G-02   | G-02   | G-02   | G-02   |         |                     | 
| **Caio Julião**                      |        |        |        |        |         |                     |
| **Jocelio Gomes Silva**              |   FE-01.3     |   FE-01.3     |        |        |         |                     | 
| **Lucas dos Santos Ribeiro**         |    FE-01.1    |    FE-01.1    |    FE-02.1    |    FE-02.1    |         |                     | 
| **Luis Gustavo**                     | FE-01.1       | FE-01.1       | FE-02.1       |  FE-02.1      |         |                     |

---

<!-- ## Sprint Burndown
<img src="./Burndown/Burndown_Sprint1.png" alt="Burndown Chart" width="700"/> -->

---

## 🔄 Retrospectiva da Sprint 2



---

## 📖 Legenda das Disciplinas

| Sigla | Disciplina                   |
|-------|------------------------------|
| ES    | Engenharia de Software       |
| TP    | Técnicas de Programação      |
| DW    | Desenvolvimento Web          |
| BD    | Banco de Dados relacional    |
