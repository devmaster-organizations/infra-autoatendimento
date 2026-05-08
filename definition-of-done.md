# Definition of Done — Autoatendimento Secretaria Acadêmica FATEC Jacareí
**Projeto ABP 2026-1 · 2º DSM**

Uma tarefa só é considerada concluída quando todos os critérios abaixo estiverem atendidos.

---

## Sprint 1 — Base do Backend e Diagrama de Casos de Uso

---

### INF-01 / INF-02 / INF-03 – Ambiente, repositório e containerização

**User Story:**
Como dev, quero o ambiente padronizado, o repositório configurado e os containers funcionando para que qualquer membro execute o projeto com um único comando.

**Critérios de Aceitação – DoD:**
- `docker compose up` sobe os três containers (PostgreSQL, Backend, Frontend) sem erros.
- Backend responde com status 200 no endpoint `GET /health`.
- TypeScript compilando sem erros em backend e frontend.
- `.env.example` presente na raiz com todas as variáveis necessárias documentadas.
- `.gitignore` ignorando `.env`, `node_modules` e arquivos de build.
- README raiz com instruções mínimas de execução revisado e commitado.

---

### BD-01 – Modelagem e criação do banco de dados

**User Story:**
Como dev, quero o banco de dados modelado e as migrations rodando para que as tabelas estejam prontas para uso no backend.

**Critérios de Aceitação – DoD:**
- MER/DER commitado na pasta `/docs`.
- Todas as migrations rodando sem erro via Prisma no container PostgreSQL.
- Tabelas criadas: `users`, `navigation_nodes`, `questions`, `interaction_logs`, `satisfaction_ratings`.
- Enums, índices e trigger de `updated_at` funcionando conforme modelado.
- Seed inicial executável via comando documentado no README do backend.

---

### RF01 – Navegação conversacional (endpoints GET)

**User Story:**
Como aluno, quero que o chatbot carregue os menus e avance ao selecionar uma opção para que a navegação seja fluida e responsiva.

**Critérios de Aceitação – DoD:**
- `GET /navigation-nodes/tree` retorna a árvore completa de nós com status 200.
- `GET /navigation-nodes/:slug` retorna o nó correspondente ou 404 se não encontrado.
- Respostas seguem o contrato documentado no Swagger.
- Rotas sem autenticação requerida para o perfil Aluno.
- Testes unitários de RF01 (TESTE-01.1) passando.

---

### RF02 – Repositório de conhecimento (endpoint GET)

**User Story:**
Como aluno, quero consultar o repositório de conhecimento pelo chatbot para receber respostas com evidência documental.

**Critérios de Aceitação – DoD:**
- Endpoint de consulta retorna resposta e trecho de evidência correspondente ao nó navegado.
- Metadados da fonte (documento, página, seção) presentes no retorno.
- Resposta segue o contrato documentado no Swagger.
- Teste unitário de RF02 (TESTE-01.2) passando.

---

### RF03 / RF09 – Autenticação e perfis de usuário

**User Story:**
Como Administrador ou Secretária Acadêmica, quero fazer login com e-mail e senha para acessar as funcionalidades restritas do sistema.

**Critérios de Aceitação – DoD:**
- `POST /auth/login` retorna JWT com id, role e expiração para credenciais válidas.
- Credenciais inválidas retornam 401 com mensagem genérica (sem revelar qual campo está errado).
- Senha armazenada com hash bcrypt — nenhuma senha em texto puro no banco.
- JWT secret carregado exclusivamente via variável de ambiente.
- Testes unitários de RF09 (TESTE-02.1 e TESTE-02.2) passando.

---

### RF10 / RF11 – RBAC e proteção de rotas

**User Story:**
Como sistema, preciso verificar token e papel do usuário em cada requisição protegida para que apenas perfis autorizados acessem rotas restritas.

**Critérios de Aceitação – DoD:**
- Requisição sem token retorna 401.
- Requisição com token de role incorreta retorna 403.
- Token expirado retorna 401.
- Todas as rotas administrativas protegidas pelos middlewares de autenticação e autorização.
- Aluno acessa rotas públicas sem token.

---

### RF04 – Gestão de conteúdo — endpoints GET (Administrador)

**User Story:**
Como administrador, quero listar e consultar nós, usuários e logs pela API para ter visibilidade sobre o conteúdo do sistema.

**Critérios de Aceitação – DoD:**
- `GET /navigation-nodes`, `GET /users`, `GET /logs` retornam listas paginadas com status 200.
- `GET /users/:id` e `GET /navigation-nodes/:id` retornam o recurso ou 404.
- Todos os endpoints protegidos por role de Administrador.
- Respostas seguem os contratos documentados no Swagger.

---

### RF06 – Gestão de perguntas — endpoints GET (Secretária Acadêmica)

**User Story:**
Como Secretária Acadêmica, quero listar e consultar as perguntas recebidas para organizar e priorizar os atendimentos.

**Critérios de Aceitação – DoD:**
- `GET /questions` retorna lista de perguntas com status 200.
- `GET /questions/:id` retorna a pergunta ou 404 se não encontrada.
- Endpoints protegidos por role de Secretária Acadêmica.
- Respostas seguem o contrato documentado no Swagger.

---

### ARQ-01 – Diagrama de Casos de Uso

**User Story:**
Como avaliador, quero o diagrama de casos de uso entregue na Sprint 1 para que os atores e fluxos do sistema estejam documentados.

**Critérios de Aceitação – DoD:**
- Diagrama inclui todos os atores: Aluno, Secretária Acadêmica, Administrador e Sistema de Autenticação.
- Todos os casos de uso do backlog representados com relacionamentos `<<include>>` e `<<extend>>` corretos.
- Arquivo fonte e imagem exportada commitados em `/docs/uml`.
- Revisado e aprovado por ao menos dois membros do time.

---

### TESTE-01 / TESTE-02 – Testes unitários da Sprint 1

**User Story:**
Como dev, quero testes unitários dos fluxos de navegação, consulta ao repositório, login e validação de token passando para garantir a confiabilidade do backend.

**Critérios de Aceitação – DoD:**
- TESTE-01.1: Teste de RF01 (navegar por menus) passando — cenários de sucesso e nó não encontrado.
- TESTE-01.2: Teste de RF02 (consultar repositório) passando — retorno com evidência e sem evidência.
- TESTE-02.1: Teste de RF09 (autenticar) passando — credenciais válidas e inválidas.
- TESTE-02.2: Teste de RF11 (validar token) passando — token válido, inválido e expirado.
- Todos os testes rodam via `npm test` no container de backend sem dependência do banco real.
- Nenhum teste falhando ao final da sprint.

---

## Sprint 2 — Rotas Push, Logs de Navegação e Diagrama de Classes

---

### RF01 – Navegação conversacional (endpoints POST, PUT, PATCH, DELETE)

**User Story:**
Como administrador, quero inserir, editar, ativar/desativar e remover nós de navegação via API para gerenciar o conteúdo do chatbot.

**Critérios de Aceitação – DoD:**
- `POST /navigation-nodes` cria nó e retorna 201 com o recurso criado.
- `PUT /navigation-nodes/:id` atualiza e retorna 200.
- `PATCH /navigation-nodes/:id/status` ativa ou desativa o nó e retorna 200.
- `DELETE /navigation-nodes/:id` remove o nó ou retorna 409 se houver filhos vinculados.
- Todos os endpoints protegidos por role de Administrador.
- Seed com dados do cliente executado e validado no ambiente de desenvolvimento.
- Respostas seguem os contratos documentados no Swagger.

---

### RF04 – Gestão de usuários (endpoints POST, PUT, DELETE)

**User Story:**
Como administrador, quero inserir, editar e remover usuários do perfil Secretária Acadêmica para manter o controle de acessos completo.

**Critérios de Aceitação – DoD:**
- `POST /users` cria usuário com senha hasheada e retorna 201.
- `PUT /users/:id` atualiza dados do usuário e retorna 200.
- `DELETE /users/:id` remove o usuário e retorna 204.
- E-mail duplicado retorna 409.
- Todos os endpoints protegidos por role de Administrador.

---

### RF04 – Gestão de documentos oficiais (endpoints POST, PUT)

**User Story:**
Como administrador, quero inserir e atualizar documentos oficiais no repositório para manter as evidências documentais atualizadas.

**Critérios de Aceitação – DoD:**
- `POST /documents` cria documento com chunks e retorna 201.
- `PUT /documents/:id` atualiza documento e retorna 200.
- Metadados (fonte, página, seção) persistidos corretamente.
- Endpoints protegidos por role de Administrador.

---

### RF05 – Encaminhamento de pergunta à secretaria

**User Story:**
Como aluno, quero enviar minha dúvida com meu e-mail institucional ao final da navegação para que a secretaria possa me responder.

**Critérios de Aceitação – DoD:**
- `POST /questions` cria a pergunta com status `em_aberto` e retorna 201.
- Campos ausentes ou e-mail inválido retornam 400 com mensagem descritiva.
- Pergunta associada à sessão de navegação correspondente.
- Endpoint público (sem autenticação requerida para o Aluno).
- Teste unitário de RF05 (TESTE-03.1) passando.

---

### RF06 – Gestão de perguntas (endpoints PATCH)

**User Story:**
Como Secretária Acadêmica, quero atualizar o status e vincular responsável a cada pergunta para que o controle de atendimentos seja rastreável.

**Critérios de Aceitação – DoD:**
- `PATCH /questions/:id/status` atualiza status para `em_aberto` ou `respondida` e retorna 200.
- `PATCH /questions/:id/assign` vincula a Secretária responsável e retorna 200.
- Status inválido retorna 400.
- Pergunta não encontrada retorna 404.
- Endpoints protegidos por role de Secretária Acadêmica.
- Testes unitários de RF06 (TESTE-04.1 e TESTE-04.2) passando.

---

### RF07 – Avaliação de satisfação (endpoint POST)

**User Story:**
Como sistema, preciso receber e armazenar a avaliação de satisfação do aluno ao final do atendimento para medir a qualidade do serviço.

**Critérios de Aceitação – DoD:**
- `POST /sessions/:id/satisfaction` persiste a avaliação e retorna 201.
- Segunda avaliação na mesma sessão retorna 409.
- Valor inválido retorna 400.
- Endpoint público (sem autenticação requerida para o Aluno).
- Teste unitário de RF07 (TESTE-03.2) passando.

---

### RF08 – Registro de logs de navegação

**User Story:**
Como sistema, preciso registrar e atualizar o log de navegação de cada sessão para que o fluxo completo de atendimento seja rastreável.

**Critérios de Aceitação – DoD:**
- `POST /logs` cria sessão de log com session_id e data/hora e retorna 201.
- `PATCH /logs/:sessionId/navigation` atualiza o fluxo de nós percorridos e retorna 200.
- `PATCH /logs/:sessionId/question` associa a pergunta à sessão e retorna 200.
- Session_id inexistente retorna 404.
- Endpoint público (sem autenticação requerida para o Aluno).
- Teste unitário de RF08 (TESTE-03.3) passando.

---

### Frontend – Interface do Chatbot

**User Story:**
Como aluno, quero interagir com uma interface de chatbot clara e responsiva para navegar pelos menus em qualquer dispositivo.

**Critérios de Aceitação – DoD:**
- Chatbot exibe mensagem de boas-vindas e opções do nó raiz ao carregar.
- Seleção de opção avança para o próximo nó corretamente, consumindo `GET /navigation-nodes/:slug`.
- Resposta final exibe texto e trecho de evidência documental.
- Formulário de envio de pergunta funcional (texto + e-mail, com validação de campos).
- Layout responsivo funcionando em mobile (≥ 375px), tablet e desktop.
- Estado de carregamento e mensagem de erro exibidos corretamente.

---

### Frontend – Autenticação

**User Story:**
Como usuário autenticado, quero uma tela de login para acessar o painel administrativo com segurança.

**Critérios de Aceitação – DoD:**
- Tela de login funcional consumindo `POST /auth/login`.
- Token armazenado conforme estratégia definida na DoR.
- Credenciais inválidas exibem mensagem de erro sem revelar qual campo está incorreto.
- Rotas do painel redirecionam para login quando não autenticado.

---

### ARQ-02 – Diagrama de Classes

**User Story:**
Como avaliador, quero o diagrama de classes entregue na Sprint 2 para que a estrutura do código backend fique documentada.

**Critérios de Aceitação – DoD:**
- Diagrama cobre todas as entidades, services e controllers do backend.
- Atributos, tipos e relacionamentos consistentes com o código implementado.
- Arquivo fonte e imagem exportada commitados em `/docs/uml`.
- Revisado e aprovado por ao menos dois membros do time.

---

### TESTE-03 / TESTE-04 – Testes unitários da Sprint 2

**User Story:**
Como dev, quero testes unitários dos fluxos de envio de pergunta, satisfação, logs e gestão de perguntas passando para garantir que as rotas push funcionam corretamente.

**Critérios de Aceitação – DoD:**
- TESTE-03.1: Teste de RF05 (enviar pergunta) passando — campos válidos, e-mail inválido e campos ausentes.
- TESTE-03.2: Teste de RF07 (registrar satisfação) passando — avaliação válida, duplicada e valor inválido.
- TESTE-03.3: Teste de RF08 (registrar log) passando — criação, atualização de navegação e associação de pergunta.
- TESTE-04.1: Teste de RF06 (listar perguntas) passando — listagem com e sem filtro de status.
- TESTE-04.2: Teste de RF06 (atualizar status) passando — status válido, inválido e pergunta não encontrada.
- Todos os testes das sprints anteriores continuam passando (sem regressão).
- Nenhum teste falhando ao final da sprint.

---

## Sprint 3 — Painel Administrativo, Documentação e Diagrama de Sequência

---

### Frontend – Painel Administrativo

**User Story:**
Como administrador, quero gerenciar nós, usuários e logs por uma interface visual para que alterações não exijam acesso direto ao banco.

**Critérios de Aceitação – DoD:**
- Tela de CRUD de nós de navegação funcional: criar, editar, ativar/desativar e remover nós.
- Confirmação de exclusão exibida antes de remover um nó.
- Tela de gerenciamento de usuários funcional: criar e remover usuários do perfil Secretária Acadêmica.
- Tela de logs exibe lista de sessões com fluxo, pergunta, satisfação, data e horário.
- Todas as telas acessíveis apenas para usuários autenticados com role Administrador.
- Layout responsivo e consistente com a identidade visual do projeto.

---

### Frontend – Painel da Secretária Acadêmica

**User Story:**
Como Secretária Acadêmica, quero ver as perguntas e atualizar seus status pela interface para que o atendimento seja organizado.

**Critérios de Aceitação – DoD:**
- Tela de listagem exibe todas as perguntas com texto, e-mail, status e data.
- Filtro por status (`em_aberto` / `respondida`) funcional.
- Ação de atualização de status funcional, consumindo `PATCH /questions/:id/status`.
- Tela acessível apenas para usuários com role Secretária Acadêmica.

---

### RF07 – Componente de satisfação no frontend

**User Story:**
Como aluno, quero indicar se fui bem atendido ao final da interação para que o laboratório meça a qualidade do autoatendimento.

**Critérios de Aceitação – DoD:**
- Componente de satisfação exibido após a resposta final do chatbot.
- Botões "Gostei" e "Não gostei" funcionais, consumindo `POST /sessions/:id/satisfaction`.
- Confirmação visual exibida após o registro da avaliação.
- Segunda tentativa de avaliação na mesma sessão tratada com mensagem amigável.

---

### RNF07 / RNF03 – Documentação do repositório e técnica

**User Story:**
Como avaliador ou novo colaborador, quero documentação completa no repositório para entender o sistema e executá-lo sem auxílio.

**Critérios de Aceitação – DoD:**
- README raiz contém: propósito do projeto, pré-requisitos, instruções de execução e estrutura do projeto.
- README de `/backend` contém: arquitetura, descrição dos endpoints e instrução de testes.
- README de `/frontend` contém: estrutura de componentes e instrução de execução isolada.
- Endpoints documentados no Swagger, acessíveis via `GET /api-docs`.
- Modelo de dados (MER/DER) e diagramas UML das três sprints presentes em `/docs`.
- Nenhum dado sensível (senha, chave, token) exposto no repositório.

---

### ARQ-03 – Diagrama de Sequência

**User Story:**
Como avaliador, quero o diagrama de sequência entregue na Sprint 3 para que o fluxo de comunicação entre frontend, backend e banco fique documentado.

**Critérios de Aceitação – DoD:**
- Diagrama cobre os quatro fluxos definidos na DoR: navegação do aluno, login, envio de pergunta e registro de log.
- Participantes corretos: Browser, Frontend React, Backend Node.js, PostgreSQL e Sistema de Autenticação.
- Mensagens síncronas e assíncronas corretamente representadas.
- Arquivo fonte e imagem exportada commitados em `/docs/uml`.
- Revisado e aprovado por ao menos dois membros do time.

---

### TESTE-05 – Testes unitários da Sprint 3

**User Story:**
Como dev, quero testes unitários dos fluxos administrativos do RF04 passando para garantir que o Administrador opera corretamente sobre documentos, nós, usuários e logs.

**Critérios de Aceitação – DoD:**
- TESTE-05.1: Teste de RF04 (gerenciar documentos) passando — inserção, atualização e validação de campos.
- TESTE-05.2: Teste de RF04 (gerenciar nós) passando — CRUD completo e validação de filhos antes do DELETE.
- TESTE-05.3: Teste de RF04 (gerenciar usuários) passando — criação com hash, e-mail duplicado e remoção.
- TESTE-05.4: Teste de RF04 (visualizar logs) passando — listagem completa e acesso restrito a Administrador.
- Todos os testes das sprints anteriores continuam passando (sem regressão).
- Cobertura total de testes unitários documentada e revisada pelo time.
- Nenhum teste falhando ao final da sprint.
