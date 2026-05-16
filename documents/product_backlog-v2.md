# Product Backlog — Autoatendimento Secretaria Acadêmica FATEC Jacareí
**Projeto ABP 2026-1 · 2º DSM · Focal Point: Prof. André Olímpio**

---

## Sprint 1 — Base do Backend e Diagrama de Casos de Uso

| Requisito | Tarefa | User Story |
|-----------|--------|------------|
| INF-01 – Configuração do repositório e ambiente | INF-01.1 – Configurar repositório, estrutura de pastas e TypeScript | Como dev, quero um repositório estruturado com TypeScript configurado para que todos os membros codifiquem de forma padronizada e sem conflitos. |
| INF-01 – Configuração do repositório e ambiente | INF-01.2 – Configurar Docker Compose com containers PostgreSQL, Backend e Frontend | Como dev, quero subir todo o ambiente com um único comando para que qualquer membro ou avaliador execute o projeto facilmente. |
| BD-01 – Modelagem e criação do banco de dados (RP03) | BD-01.1 – Criar diagrama MER/DER do banco de dados | Como equipe, queremos o modelo entidade-relacionamento definido para que a implementação das tabelas seja guiada e consistente. |
| BD-01 – Modelagem e criação do banco de dados (RP03) | BD-01.2 – Criar extensão pgcrypto, enums do domínio e tabela `users` com migration | Como dev, quero os tipos, extensões e tabela de usuários criados no banco para que os perfis de Administrador e Secretária Acadêmica sejam persistidos com segurança. |
| BD-01 – Modelagem e criação do banco de dados (RP03) | BD-01.3 – Criar tabela e migration de `navigation_nodes` | Como dev, quero a tabela de nós de navegação no banco para que o chatbot consulte menus e submenus armazenados dinamicamente. |
| BD-01 – Modelagem e criação do banco de dados (RP03) | BD-01.4 – Criar tabelas de `questions`, `interaction_logs` e `satisfaction_ratings` | Como dev, quero as tabelas de perguntas, logs e satisfação criadas para que as interações dos alunos sejam registradas corretamente. |
| BD-01 – Modelagem e criação do banco de dados (RP03) | BD-01.5 – Mapear enums, índices e `updated_at` automático no ORM (Prisma) | Como dev, quero o ORM refletindo a estrutura real do banco para que as consultas sejam seguras e tipadas. |
| RF01 – Navegação conversacional | RF01.1 – Criar endpoints GET de navegação (`/tree` e `/:slug`) | Como aluno, quero que o chatbot carregue os menus e avance para o próximo nó ao selecionar uma opção para que a navegação seja fluida e responsiva. |
| RF02 – Repositório de conhecimento | RF02.1 – Criar endpoint GET de consulta ao repositório de conhecimento | Como aluno, quero consultar o repositório de conhecimento pelo chatbot para que eu receba respostas padronizadas com evidência documental. |
| RF03 / RF09 – Perfis de usuário e Autenticação | RF03.1 – Criar endpoint `POST /auth/login` com geração de JWT (id, role, expiração) | Como Administrador ou Secretária Acadêmica, quero fazer login com e-mail e senha para acessar as funcionalidades restritas do sistema. |
| RF03 / RF09 – Perfis de usuário e Autenticação | RF03.2 – Implementar hash de senha com bcrypt e variáveis de ambiente para chaves sensíveis | Como sistema, preciso armazenar senhas com hash seguro e chaves em variáveis de ambiente para que credenciais não fiquem expostas. |
| RF10 / RF11 – RBAC e Proteção de rotas | RF10.1 – Criar middlewares de autenticação JWT e autorização por papel (role) | Como sistema, preciso validar o token e o papel do usuário em cada requisição protegida para que apenas perfis autorizados acessem as rotas restritas. |
| RF06 – Gestão de perguntas (Secretária Acadêmica) | RF06.1 – Criar endpoints GET de perguntas (listagem e busca por ID) | Como Secretária Acadêmica, quero listar e consultar as perguntas recebidas para que eu possa organizar e priorizar os atendimentos. |
| INF-02 – Ferramentas de desenvolvimento | INF-02.1 – Conectar Swagger ao backend e configurar Jest | Como dev, quero a documentação automática de endpoints e o ambiente de testes configurado para que a API seja consultável e testável desde o início. |
| ARQ-01 – Modelagem UML (RNF04) | ARQ-01.1 – Criar e entregar Diagrama de Casos de Uso | Como avaliador, quero o diagrama de casos de uso entregue na Sprint 1 para que os requisitos funcionais e os atores do sistema estejam visualmente documentados. |
| TESTE-02 – Testes unitários: Autenticação | TESTE-02.1 – Teste unitário de RF09: Autenticar-se no sistema | Como dev, quero um teste unitário do fluxo de login para que eu garanta que apenas credenciais válidas geram um token JWT. |
| TESTE-02 – Testes unitários: Autenticação | TESTE-02.2 – Teste unitário de RF11: Validar token de acesso | Como dev, quero um teste unitário da validação do token para que eu garanta que requisições com token inválido ou expirado são rejeitadas. |

---

## Sprint 2 — Rotas Push, Logs de Navegação e Diagrama de Classes

| Requisito | Tarefa | User Story |
|-----------|--------|------------|
| RF04 – Gestão de conteúdo (Administrador) | RF04.1 – Criar endpoints GET de nós de navegação (listagem e busca por ID) | Como administrador, quero listar e consultar os nós de navegação pela API para que eu possa visualizar o conteúdo do chatbot. |
| RF04 – Gestão de conteúdo (Administrador) | RF04.2 – Criar endpoints GET de usuários (listagem e busca por ID) | Como administrador, quero listar e consultar os usuários cadastrados para que eu tenha controle sobre quem tem acesso ao sistema. |
| RF04 – Gestão de conteúdo (Administrador) | RF04.3 – Criar endpoint GET de logs de navegação (listagem administrativa) | Como administrador, quero consultar todos os logs de atendimento pela API para que seja possível monitorar o uso do sistema. |
| RF01 – Navegação conversacional | RF01.2 – Criar endpoints POST e PUT de nós de navegação (cadastro e edição) | Como administrador, quero inserir e editar nós de navegação via API para que o conteúdo do chatbot possa ser gerenciado sem alterar código. |
| RF01 – Navegação conversacional | RF01.3 – Criar endpoints PATCH de status e DELETE de nós de navegação | Como administrador, quero ativar, desativar e remover nós de navegação para que o conteúdo desatualizado não apareça para os alunos. |
| RF01 – Navegação conversacional | RF01.4 – Popular banco com seed dos dados iniciais fornecidos pelo cliente | Como aluno, quero que o chatbot já tenha as respostas sobre DSM, Geoprocessamento e MARH disponíveis para que o MVP seja funcional desde o primeiro acesso. |
| RF04 – Gestão de conteúdo (Administrador) | RF04.4 – Criar endpoints POST, PUT e DELETE de usuários | Como administrador, quero inserir, editar e remover usuários do perfil Secretária Acadêmica para que o controle de acessos seja completo. |
| RF04 – Gestão de conteúdo (Administrador) | RF04.5 – Criar endpoints POST e PUT de documentos oficiais | Como administrador, quero inserir e atualizar documentos oficiais no repositório para que as evidências documentais exibidas no chatbot estejam sempre atualizadas. |
| RF09 – Autenticação e Recuperação | RF09.2 – Implementar fluxo de recuperação de senha | Como usuário, quero recuperar minha senha caso eu a esqueça para que eu não perca o acesso ao sistema. |
| INF-03 – Deploy | INF-03.1 – Realizar o deploy da aplicação (Frontend e Backend) | Como equipe, queremos a aplicação em um ambiente acessível para validação do cliente. |
| RF05 – Encaminhamento de pergunta à secretaria | RF05.1 – Criar endpoint `POST /questions` (texto da dúvida e e-mail institucional) | Como aluno, quero enviar minha dúvida com meu e-mail institucional ao final da navegação para que a secretaria possa me responder. |
| RF06 – Gestão de perguntas (Secretária Acadêmica) | RF06.2 – Criar endpoint `PATCH /questions/:id/status` (em aberto / respondida) | Como Secretária Acadêmica, quero atualizar o status de cada pergunta para que o controle de atendimentos seja rastreável. |
| RF06 – Gestão de perguntas (Secretária Acadêmica) | RF06.3 – Criar endpoint `PATCH /questions/:id/assign` (vincular responsável) | Como Secretária Acadêmica, quero ser vinculada como responsável por uma pergunta para que fique claro quem está tratando cada solicitação. |
| RF07 – Avaliação de satisfação | RF07.1 – Criar endpoint `POST /sessions/:id/satisfaction` (Gostei / Não gostei) | Como sistema, preciso receber e armazenar a avaliação de satisfação do aluno ao final do atendimento para que a qualidade do serviço possa ser medida. |
| RF08 – Registro de logs de navegação | RF08.1 – Criar endpoint `POST /logs` (abertura de log de interação) | Como sistema, preciso registrar o início de cada sessão de navegação para que o fluxo completo de atendimento seja rastreável. |
| RF08 – Registro de logs de navegação | RF08.2 – Criar endpoint `PATCH /logs/:sessionId/navigation` (atualizar fluxo de navegação) | Como sistema, preciso atualizar o log a cada passo do aluno no chatbot para que o caminho percorrido fique registrado integralmente. |
| RF08 – Registro de logs de navegação | RF08.3 – Criar endpoint `PATCH /logs/:sessionId/question` (associar solicitação à sessão) | Como sistema, preciso vincular a pergunta enviada à sessão de navegação correspondente para que o log de atendimento seja completo. |
| Frontend – Interface do Chatbot (RP01 / RNF01) | FE-01.1 – Criar layout e componente de chat (bolhas, opções, scroll automático) | Como aluno, quero interagir com uma interface de chatbot clara e responsiva para que a navegação pelos menus seja intuitiva em qualquer dispositivo. |
| Frontend – Interface do Chatbot (RP01 / RNF01) | FE-01.2 – Implementar fluxo de navegação no frontend consumindo a API de nós | Como aluno, quero que minhas escolhas no chatbot me levem ao próximo menu automaticamente para que eu chegue à informação sem recarregar a página. |
| Frontend – Interface do Chatbot (RP01 / RNF01) | FE-01.3 – Implementar exibição de trecho de evidência documental ao final da navegação | Como aluno, quero ver o trecho do documento oficial que embasa a resposta do bot para que eu confie na informação recebida. |
| Frontend – Interface do Chatbot (RP01 / RNF01) | FE-01.4 – Implementar formulário de envio de pergunta à secretaria (texto + e-mail) | Como aluno, quero preencher meu e-mail e minha dúvida diretamente no chatbot para que o envio seja simples e integrado à navegação. |
| Frontend – Autenticação (RP01) | FE-02.1 – Criar tela de login para Administrador e Secretária Acadêmica | Como usuário autenticado, quero uma tela de login para que eu acesse o painel administrativo com segurança. |
| Frontend – Autenticação (RP01) | FE-02.2 – Implementar proteção de rotas no frontend (redirecionar não autenticados) | Como sistema, preciso redirecionar usuários não autenticados que tentem acessar o painel para que as rotas administrativas sejam protegidas também no frontend. |
| ARQ-02 – Modelagem UML (RNF04) | ARQ-02.1 – Criar e entregar Diagrama de Classes | Como avaliador, quero o diagrama de classes entregue na Sprint 2 para que a estrutura do código backend fique documentada e compreensível. |
| TESTE-01 – Testes unitários: Aluno | TESTE-01.1 – Teste unitário de RF01: Navegar por menus conversacionais | Como dev, quero um teste unitário do fluxo de navegação para que eu garanta que o aluno consegue percorrer a árvore de menus sem erros. |
| TESTE-01 – Testes unitários: Aluno | TESTE-01.2 – Teste unitário de RF02: Consultar repositório de conhecimento | Como dev, quero um teste unitário da consulta ao repositório para que eu garanta que as respostas retornadas correspondem ao nó navegado. |
| TESTE-03 – Testes unitários: Aluno | TESTE-03.1 – Teste unitário de RF05: Enviar pergunta à secretaria | Como dev, quero um teste unitário do envio de pergunta para que eu garanta que texto e e-mail são validados e persistidos corretamente. |
| TESTE-03 – Testes unitários: Aluno | TESTE-03.2 – Teste unitário de RF07: Registrar avaliação de satisfação | Como dev, quero um teste unitário do registro de satisfação para que eu garanta que a avaliação do aluno é gravada ao final de cada sessão. |
| TESTE-03 – Testes unitários: Aluno | TESTE-03.3 – Teste unitário de RF08: Registrar log de navegação | Como dev, quero um teste unitário do registro de log para que eu garanta que o fluxo completo de navegação do aluno é persistido corretamente. |
| TESTE-04 – Testes unitários: Secretária Acadêmica | TESTE-04.1 – Teste unitário de RF06: Listar perguntas recebidas | Como dev, quero um teste unitário da listagem de perguntas para que eu garanta que a Secretária visualiza apenas as solicitações que lhe competem. |
| TESTE-04 – Testes unitários: Secretária Acadêmica | TESTE-04.2 – Teste unitário de RF06: Atualizar status de pergunta | Como dev, quero um teste unitário da atualização de status para que eu garanta que apenas os valores válidos (em aberto / respondida) são aceitos. |

---

## Sprint 3 — Painel Administrativo, Documentação e Diagrama de Sequência

| Requisito | Tarefa | User Story |
|-----------|--------|------------|
| RF07 – Avaliação de satisfação | RF07.2 – Implementar componente de avaliação de satisfação no chatbot | Como aluno, quero indicar se fui bem atendido ao final da interação para que o laboratório saiba se o autoatendimento está funcionando. |
| Frontend – Painel Administrativo (RP01 / RNF01) | FE-03.1 – Criar tela de CRUD de nós de navegação no painel admin | Como administrador, quero gerenciar os menus do chatbot por uma interface visual para que alterações de conteúdo não exijam acesso direto ao banco de dados. |
| Frontend – Painel Administrativo (RP01 / RNF01) | FE-03.2 – Criar tela de gerenciamento de usuários no painel admin | Como administrador, quero criar e remover usuários do perfil Secretária Acadêmica pela interface para que o controle de acessos seja simples e auditável. |
| Frontend – Painel Administrativo (RP01 / RNF01) | FE-03.3 – Criar tela de visualização de logs de navegação no painel admin | Como administrador, quero visualizar os logs de atendimento na interface para que eu identifique padrões de uso e possíveis falhas no fluxo do chatbot. |
| Frontend – Painel da Secretária (RP01 / RNF01) | FE-04.1 – Criar tela de listagem e atualização de status de perguntas | Como Secretária Acadêmica, quero ver todas as perguntas recebidas e atualizar seus status pela interface para que o atendimento seja organizado sem acesso à API. |
| RNF07 – Documentação do repositório | RNF07.1 – Escrever README principal na raiz do repositório | Como avaliador ou novo colaborador, quero um README claro na raiz do projeto para que eu entenda o propósito do sistema e saiba como executá-lo. |
| RNF07 – Documentação do repositório | RNF07.2 – Escrever README específico das pastas `/frontend` e `/backend` | Como dev, quero documentação específica em cada subprojeto para que seja possível entender e executar cada parte de forma independente. |
| RNF03 – Documentação técnica | RNF03.1 – Documentar modelo de dados, descrição da arquitetura e instruções de execução | Como avaliador, quero a documentação técnica completa no repositório para que o projeto atenda integralmente ao requisito RNF03. |
| RNF03 – Documentação técnica | RNF03.2 – Documentar rotas e endpoints da API (via Swagger e Markdown) | Como avaliador ou dev externo, quero os endpoints documentados para que seja possível integrar ou avaliar a API sem precisar ler o código-fonte. |
| ARQ-03 – Modelagem UML (RNF04) | ARQ-03.1 – Criar e entregar Diagrama de Sequência | Como avaliador, quero o diagrama de sequência entregue na Sprint 3 para que o fluxo de comunicação entre frontend, backend e banco fique explícito e documentado. |
| TESTE-05 – Testes unitários: Administrador | TESTE-05.1 – Teste unitário de RF04: Gerenciar documentos oficiais | Como dev, quero um teste unitário do gerenciamento de documentos para que eu garanta que apenas o Administrador consegue inserir, editar e remover documentos. |
| TESTE-05 – Testes unitários: Administrador | TESTE-05.2 – Teste unitário de RF04: Gerenciar nós de navegação | Como dev, quero um teste unitário do CRUD de nós para que eu garanta que a árvore de navegação é manipulada corretamente e sem inconsistências. |
| TESTE-05 – Testes unitários: Administrador | TESTE-05.3 – Teste unitário de RF04: Gerenciar usuários da secretaria | Como dev, quero um teste unitário do CRUD de usuários para que eu garanta que apenas o Administrador cria, edita e remove usuários do perfil Secretária. |
| TESTE-05 – Testes unitários: Administrador | TESTE-05.4 – Teste unitário de RF04: Visualizar logs de navegação | Como dev, quero um teste unitário da visualização de logs para que eu garanta que o Administrador acessa todos os registros de atendimento sem restrição indevida. |
    