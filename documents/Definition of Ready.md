# Definition of Ready — Autoatendimento Secretaria Acadêmica FATEC Jacareí
**Projeto ABP 2026-1 · 2º DSM**

Uma tarefa só pode entrar em sprint quando todos os critérios abaixo estiverem atendidos.

---

## Sprint 1 — Base do Backend e Diagrama de Casos de Uso

### INF-01 – Padronização do ambiente de desenvolvimento
**User Story:** Como dev, quero ter o ambiente de desenvolvimento padronizado para que todos os membros trabalhem com as mesmas versões e configurações.

**Critérios de Aceitação – DoR:**
- Versão do Node.js definida e documentada no `README` raiz.
- Docker e Docker Compose com versões mínimas definidas e documentadas.
- Repositório criado, com branch padrão, política de branches e `.gitignore` configurados.
- Sem dependência de configuração individual de membro que bloqueie o início do desenvolvimento.

### INF-02 – Configuração do repositório e TypeScript
**User Story:** Como dev, quero TypeScript configurado em backend e frontend para que o código tenha tipagem estática e menos erros em tempo de execução.

**Critérios de Aceitação – DoR:**
- Estrutura de pastas (`/frontend`, `/backend`, `/docs`) definida e aprovada pelo time.
- Arquivo `tsconfig.json` com configurações base definidas para backend e frontend.
- Padrão de lint (ESLint) e formatação (Prettier) definidos e documentados.
- Dependências iniciais (`express`, `prisma`, `react`, `vite`) listadas e versões fixadas.

### INF-03 – Containerização e orquestração
**User Story:** Como dev, quero subir todo o ambiente com um único comando para que qualquer membro ou avaliador execute o projeto facilmente.

**Critérios de Aceitação – DoR:**
- Três containers definidos: PostgreSQL, Backend e Frontend.
- Variáveis de ambiente mapeadas e arquivo `.env.example` criado.
- Portas de cada container definidas e documentadas.
- Estratégia de healthcheck do PostgreSQL definida antes do backend subir.
- Sem dependência de configuração manual além do `.env`.

### BD-01 – Modelagem e criação do banco de dados
**User Story:** Como dev, quero o banco de dados modelado e as migrations rodando para que as tabelas estejam prontas para uso no backend.

**Critérios de Aceitação – DoR:**
- MER/DER aprovado pelo time com todas as entidades, atributos e relacionamentos.
- Enums do domínio definidos (roles, status de pergunta, tipo de satisfação).
- Nomes de tabelas e colunas padronizados (snake_case) e aprovados.
- ORM (Prisma) escolhido e configurado com string de conexão via variável de ambiente.
- Seed inicial com dados do cliente mapeado e aprovado.

### RF01 – Navegação conversacional (endpoints GET)
**User Story:** Como aluno, quero que o chatbot carregue os menus e avance ao selecionar uma opção para que a navegação seja fluida e responsiva.

**Critérios de Aceitação – DoR:**
- Estrutura da árvore de nós de navegação definida (id, label, parent_id, resposta, evidência, slug).
- Endpoint `/tree` e `/:slug` com contratos de request/response documentados.
- Dados de seed do cliente revisados e aprovados para popular os nós iniciais.
- Sem pendência de modelagem de banco que bloqueie a implementação dos endpoints.

### RF02 – Repositório de conhecimento (endpoint GET)
**User Story:** Como aluno, quero consultar o repositório de conhecimento pelo chatbot para receber respostas com evidência documental.

**Critérios de Aceitação – DoR:**
- Estrutura de trechos indexados (chunks) definida no banco (documento, página, seção, texto).
- Contrato do endpoint de consulta documentado (filtros, retorno esperado).
- Ao menos um documento oficial de referência disponível para validação durante o desenvolvimento.

### RF03 / RF09 – Autenticação e perfis de usuário
**User Story:** Como Administrador ou Secretária Acadêmica, quero fazer login com e-mail e senha para acessar as funcionalidades restritas do sistema.

**Critérios de Aceitação – DoR:**
- Perfis definidos: Aluno (público), Secretária Acadêmica (autenticado), Administrador (autenticado).
- Contrato do endpoint `POST /auth/login` documentado (body, retorno JWT, erros).
- Campos do JWT definidos: id do usuário, role e tempo de expiração.
- Algoritmo de hash de senha definido (bcrypt) e fator de custo aprovado.
- Variável de ambiente para o JWT secret definida no `.env.example`.

### RF10 / RF11 – RBAC e proteção de rotas
**User Story:** Como sistema, preciso verificar token e papel do usuário em cada requisição protegida para que apenas perfis autorizados acessem rotas restritas.

**Critérios de Aceitação – DoR:**
- Mapeamento de roles × rotas definido e aprovado pelo time.
- Comportamento de erro documentado (401 para não autenticado, 403 para não autorizado).
- Formato do header `Authorization: Bearer <token>` definido e padronizado.

### RF06 – Gestão de perguntas — endpoints GET (Secretária Acadêmica)
**User Story:** Como Secretária Acadêmica, quero listar e consultar as perguntas recebidas para organizar e priorizar os atendimentos.

**Critérios de Aceitação – DoR:**
- Contrato dos endpoints `GET /questions` e `GET /questions/:id` documentado.
- Proteção por role de Secretária Acadêmica definida.
- Campos de retorno definidos (id, texto, e-mail, status, data de criação).

### ARQ-01 – Diagrama de Casos de Uso
**User Story:** Como avaliador, quero o diagrama de casos de uso entregue na Sprint 1 para que os atores e fluxos do sistema estejam visualmente documentados.

**Critérios de Aceitação – DoR:**
- Atores identificados e aprovados: Aluno, Secretária Acadêmica, Administrador e Sistema de Autenticação.
- Todos os casos de uso do backlog mapeados e revisados pelo time.
- Ferramenta de modelagem definida (ex.: PlantUML, Draw.io, Astah).
- Formato de entrega definido (imagem + arquivo fonte).

### TESTE-02 – Testes unitários: Autenticação
**User Story:** Como dev, quero testes unitários do fluxo de login e validação de token para garantir que a autenticação funciona conforme esperado.

**Critérios de Aceitação – DoR:**
- Jest configurado e rodando no container de backend.
- Escopo de cada teste definido: cenários de sucesso e falha para `POST /auth/login` e para validação de token.
- Mocks de banco de dados definidos (sem dependência do PostgreSQL real nos testes unitários).
- Nomenclatura de arquivos de teste padronizada (`*.spec.ts`).

---

## Sprint 2 — Rotas Push, Logs de Navegação e Diagrama de Classes

### RF01 – Navegação conversacional (endpoints POST, PUT, PATCH, DELETE)
**User Story:** Como administrador, quero inserir, editar, ativar/desativar e remover nós de navegação via API para gerenciar o conteúdo do chatbot sem alterar código.

**Critérios de Aceitação – DoR:**
- Contratos dos endpoints POST, PUT, PATCH e DELETE de nós documentados.
- Regra de validação de filhos antes do DELETE definida e aprovada.
- Campos obrigatórios e opcionais de cada endpoint documentados.
- Proteção por role de Administrador confirmada para todas as rotas de escrita.

### RF04 – Gestão de conteúdo (Administrador) – endpoints GET, POST, PUT, DELETE
**User Story:** Como administrador, quero listar, criar, editar e remover usuários; gerenciar documentos oficiais; e visualizar logs.

**Critérios de Aceitação – DoR:**
- Contratos dos endpoints GET de nós, usuários e logs documentados (listagem, busca por ID, paginação).
- Contratos dos endpoints POST, PUT e DELETE de usuários documentados (validação de e-mail único, senha mínima).
- Contratos dos endpoints POST e PUT de documentos oficiais documentados.
- Proteção por role de Administrador confirmada para todos esses endpoints.
- Regras de negócio: apenas Administrador pode criar/remover usuários; e-mail duplicado deve ser tratado.

### RF05 – Encaminhamento de pergunta à secretaria
**User Story:** Como aluno, quero enviar minha dúvida com meu e-mail institucional ao final da navegação para que a secretaria possa me responder.

**Critérios de Aceitação – DoR:**
- Campos obrigatórios definidos: texto da dúvida e e-mail institucional.
- Validação de formato de e-mail definida.
- Contrato do endpoint `POST /questions` documentado (body, retorno, erros).
- Status inicial da pergunta definido (ex.: `em_aberto`).

### RF06 – Gestão de perguntas (endpoints PATCH)
**User Story:** Como Secretária Acadêmica, quero atualizar o status e vincular responsável a cada pergunta para que o controle de atendimentos seja rastreável.

**Critérios de Aceitação – DoR:**
- Valores válidos de status definidos e aprovados: `em_aberto`, `respondida`.
- Contrato dos endpoints `PATCH /questions/:id/status` e `PATCH /questions/:id/assign` documentado.
- Regra de autorização confirmada: apenas Secretária Acadêmica pode alterar status.

### RF07 – Avaliação de satisfação (endpoint POST)
**User Story:** Como sistema, preciso receber e armazenar a avaliação de satisfação do aluno ao final do atendimento para medir a qualidade do serviço.

**Critérios de Aceitação – DoR:**
- Valores válidos de satisfação definidos: `gostei`, `nao_gostei`.
- Contrato do endpoint `POST /sessions/:id/satisfaction` documentado.
- Regra definida: apenas uma avaliação por sessão é permitida.

### RF08 – Registro de logs de navegação
**User Story:** Como sistema, preciso registrar e atualizar o log de navegação de cada sessão para que o fluxo completo de atendimento seja rastreável.

**Critérios de Aceitação – DoR:**
- Estrutura do log definida: session_id, fluxo de nós percorridos, id da pergunta, id da satisfação, data/hora.
- Contratos dos endpoints `POST /logs`, `PATCH /logs/:sessionId/navigation` e `PATCH /logs/:sessionId/question` documentados.
- Estratégia de identificação de sessão definida (ex.: UUID gerado no frontend).

### RF09.2 – Recuperação de senha
**User Story:** Como usuário, quero recuperar minha senha caso eu a esqueça para não perder o acesso ao sistema.

**Critérios de Aceitação – DoR:**
- Fluxo definido: solicitação de reset (`POST /auth/forgot-password`), envio de token por e-mail, formulário de nova senha (`POST /auth/reset-password`).
- Contratos dos endpoints documentados.
- Validade do token de recuperação definida (ex.: 1 hora).

### INF-03 – Deploy da aplicação
**User Story:** Como equipe, queremos a aplicação em um ambiente acessível para validação do cliente.

**Critérios de Aceitação – DoR:**
- Plataforma de deploy definida (ex.: Render, Vercel, Railway, AWS).
- Variáveis de ambiente de produção mapeadas e aprovadas.
- Estratégia de CI/CD mínima definida (ex.: deploy automático a partir da branch `main`).

### Frontend – Interface do Chatbot
**User Story:** Como aluno, quero interagir com uma interface de chatbot clara e responsiva para navegar pelos menus em qualquer dispositivo.

**Critérios de Aceitação – DoR:**
- Mockup ou wireframe da interface do chatbot aprovado pelo time.
- Breakpoints de responsividade definidos (mobile, tablet, desktop).
- Comportamento de scroll automático, estado de carregamento e tratamento de erro definidos.
- Identidade visual (cores, tipografia) definida antes do início do desenvolvimento.
- Contrato da API de nós revisado e disponível para consumo no frontend.

### Frontend – Autenticação
**User Story:** Como usuário autenticado, quero uma tela de login para acessar o painel administrativo com segurança.

**Critérios de Aceitação – DoR:**
- Mockup da tela de login aprovado.
- Comportamento de erro de credenciais inválidas definido (mensagem, não expor qual campo está errado).
- Estratégia de armazenamento do token no frontend definida (ex.: httpOnly cookie ou localStorage com considerações de segurança).
- Rotas protegidas mapeadas e comportamento de redirecionamento definido.

### ARQ-02 – Diagrama de Classes
**User Story:** Como avaliador, quero o diagrama de classes entregue na Sprint 2 para que a estrutura do código backend fique documentada.

**Critérios de Aceitação – DoR:**
- Todas as entidades do banco mapeadas para classes/interfaces TypeScript.
- Relacionamentos entre classes revisados e aprovados pelo time.
- Ferramenta de modelagem definida e consistente com a usada na Sprint 1.

### TESTE-01 / TESTE-03 / TESTE-04 – Testes unitários da Sprint 2
**User Story:** Como dev, quero testes unitários dos fluxos de navegação, repositório, envio de pergunta, satisfação, logs e gestão de perguntas.

**Critérios de Aceitação – DoR:**
- **TESTE-01:** Escopo definido para RF01 (navegação) e RF02 (repositório) – cenários de sucesso e falha.
- **TESTE-03:** Escopo definido para RF05 (envio de pergunta), RF07 (satisfação) e RF08 (log).
- **TESTE-04:** Escopo definido para RF06 (listagem e atualização de status).
- Mocks das dependências (banco, e-mail) definidos.
- Cobertura mínima de cada service testado definida e aprovada pelo time.

---

## Sprint 3 — Painel Administrativo, Documentação e Diagrama de Sequência

### Frontend – Painel Administrativo
**User Story:** Como administrador, quero gerenciar nós de navegação, usuários e visualizar logs por uma interface visual para que alterações não exijam acesso direto ao banco.

**Critérios de Aceitação – DoR:**
- Mockups das telas de CRUD de nós, gerenciamento de usuários e visualização de logs aprovados.
- Fluxo de criação, edição e remoção de nós definido (incluindo confirmação de exclusão).
- Todos os endpoints de backend necessários implementados e disponíveis para consumo.
- Comportamento de feedback visual (sucesso, erro, carregamento) definido para cada ação.

### Frontend – Painel da Secretária Acadêmica
**User Story:** Como Secretária Acadêmica, quero ver as perguntas recebidas e atualizar seus status pela interface para que o atendimento seja organizado.

**Critérios de Aceitação – DoR:**
- Mockup da tela de listagem e atualização de status aprovado.
- Filtro por status (em aberto / respondida) definido e aprovado.
- Endpoint `PATCH /questions/:id/status` implementado e disponível.

### RF07 – Componente de satisfação no frontend
**User Story:** Como aluno, quero indicar se fui bem atendido ao final da interação para que o laboratório meça a qualidade do autoatendimento.

**Critérios de Aceitação – DoR:**
- Posição do componente no fluxo do chatbot definida (após resposta final).
- Design do componente (botões "Gostei" / "Não gostei") aprovado.
- Endpoint `POST /sessions/:id/satisfaction` implementado e disponível.

### RNF07 / RNF03 – Documentação do repositório e técnica
**User Story:** Como avaliador ou novo colaborador, quero documentação completa no repositório para entender o sistema e executá-lo sem auxílio.

**Critérios de Aceitação – DoR:**
- Estrutura mínima dos READMEs definida: propósito, pré-requisitos, instruções de execução, variáveis de ambiente.
- Endpoints da API documentados no Swagger e revisados pelo time.
- Diagramas UML das Sprints 1 e 2 finalizados e disponíveis para inclusão na documentação.

### ARQ-03 – Diagrama de Sequência
**User Story:** Como avaliador, quero o diagrama de sequência entregue na Sprint 3 para que o fluxo de comunicação entre frontend, backend e banco fique documentado.

**Critérios de Aceitação – DoR:**
- Fluxos a serem diagramados definidos e aprovados: navegação do aluno, login, envio de pergunta e registro de log.
- Participantes do diagrama definidos: Browser, Frontend React, Backend Node.js, PostgreSQL, Sistema de Autenticação.
- Ferramenta de modelagem definida e consistente com as sprints anteriores.

### TESTE-05 – Testes unitários da Sprint 3
**User Story:** Como dev, quero testes unitários dos fluxos administrativos do RF04 para garantir que o Administrador opera corretamente sobre documentos, nós, usuários e logs.

**Critérios de Aceitação – DoR:**
- Escopo de cada teste definido: cenários de sucesso e falha para os quatro casos de uso do Administrador.
- Mocks das dependências atualizados para cobrir os novos services da Sprint 3.
- Todos os testes das sprints anteriores passando sem regressão antes do início dos novos testes.