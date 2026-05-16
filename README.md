# ABP – Aprendizagem Baseada em Projetos  

<p align="center">  
  <img src="./documents/images/devmaster.jpg"  
       alt="Devmaster"  
       style="max-width: 160px; 
       width: 60%; 
       height: auto;
       border-radius:50%"
       >  
</p>  

<p align="center">  
  <a href="#-descrição-do-projeto">Sobre o Projeto</a> |  
  <a href="#-entregas-de-sprints">Entrega de Sprints</a> |  
  <a href="#-documentação">Documentação</a> |  
  <!-- <a href="#-protótipo-no-figma">Protótipo</a> |   -->
  <a href="#equipe">Nossa Equipe</a>  
</p>  

---
# Main repository  

Este repositório tem como objetivo documentar e centralizar as informações principais do projeto **ABP 2026 - 1º semestre**.

O projeto está dividido em dois repositórios principais: um para o **backend** e outro para o **frontend**.

## Repositórios do projeto  

### Backend  

Repositório responsável pela API, regras de negócio, banco de dados, autenticação e demais serviços do sistema.

[backend_abp_autoatendimento](https://github.com/devmaster-organizations/backend_abp_autoatendimento)

### Frontend  

Repositório responsável pela interface web da aplicação, telas, componentes visuais e integração com a API.

[frontend_abp_autoatentimento](https://github.com/devmaster-organizations/frontend_abp_autoatentimento)

## Estrutura geral  

```txt
infra-autoatendimento/       <- este repositório
├── backend/                 <- submodule: backend_abp_autoatendimento (main)
├── frontend/                <- submodule: frontend_abp_autoatentimento (main)
├── infra/
│   └── frontend.Dockerfile
├── docker-compose.yml
└── README.md
```

## Como clonar

Clone o repositório **com os submodules** para que `backend/` e `frontend/` sejam baixados automaticamente:

```bash
git clone --recurse-submodules https://github.com/devmaster-organizations/infra-autoatendimento.git
```

Se você já clonou sem submodules, inicialize-os com:

```bash
git submodule update --init --recursive
```

## Como subir o ambiente local

```bash
docker compose up --build
```

Serviços disponíveis após o up:

| Serviço   | URL                    |
|-----------|------------------------|
| Frontend  | http://localhost:3000  |
| API       | http://localhost:3001  |
| PgAdmin   | http://localhost:5050  |
| Postgres  | localhost:5433         |

## Como atualizar frontend ou backend após um merge na main

Os submodules são **fixados em um commit específico**, não em uma branch "ao vivo".  
Isso significa que um merge na `main` do frontend **não atualiza automaticamente** este repositório.

Para puxar a versão mais recente de um submodule:

```bash
# Atualizar o frontend para o commit mais recente da main
cd frontend
git pull origin main
cd ..
git add frontend
git commit -m "chore: bump frontend to latest main"
git push

# O mesmo vale para o backend
cd backend
git pull origin main
cd ..
git add backend
git commit -m "chore: bump backend to latest main"
git push
```

Para atualizar **todos os submodules de uma vez**:

```bash
git submodule update --remote --merge
git add .
git commit -m "chore: bump submodules to latest main"
git push
```

> Depois que alguém fizer esse update e o repo principal for atualizado,
> um simples `git pull` aqui já trará a nova referência do submodule.

--- 

## 📌 Descrição do projeto  

Este projeto está sendo desenvolvido como atividade do **2º semestre do curso de Desenvolvimento de Software Multiplataforma da Fatec Jacareí**.  

O projeto, intitulado "Aplicação Web para Autoatendimento da Secretaria Académica da Fatec Jacareí", consiste no desenvolvimento de uma aplicação baseada num chatbot conversacional para mitigar a sobrecarga operacional da secretaria.  

---

## 🎯 Objetivo do sistema:

O objetivo central do sistema é desenvolver uma aplicação web de autoatendimento para a Secretaria Académica da Fatec Jacareí, utilizando um modelo de chatbot conversacional.  

Os propósitos específicos desta solução incluem:  

- **Redução da sobrecarga operacional:** Mitigar o volume de dúvidas recorrentes que geram atrasos e inconsistências no atendimento da secretaria, especialmente em períodos críticos como rematrículas e exames.  

- **Guia estruturado ao utilizador:** Conduzir os alunos e interessados externos através de uma árvore de navegação com menus e perguntas guiadas, além de permitir consultas diretas.  

- **Padronização da informação:** Fornecer respostas objetivas e verificáveis, baseadas em documentos oficiais (como o Regulamento Geral das Fatecs e Calendário Académico), garantindo a confiabilidade e a rastreabilidade dos dados.  

- **Apoio documental:** Apresentar, quando aplicável, trechos de evidências extraídos diretamente das normas vigentes da instituição.  

- **Intermediação de dúvidas complexas:** Permitir que, caso a dúvida não seja resolvida pela navegação, o utilizador envie a pergunta diretamente à secretaria através do sistema.  

---
## 📅 Entregas de Sprints  
As entregas seguem o cronograma definido com o cliente. Cada sprint gera um relatório e backlog detalhado.  

<div align="center">  

| Sprint | Entrega       | Status | Relatório |  
|------: |---------------|:------:|:------------------------------------------:|  
| 1      | 📅 04/05/2026 | ✅      | [Ver Backlog](./documents/Sprint1.md) |  
| 2      | 📅 25/05/2026 | 🚧    | [Ver Backlog](./documents/Sprint2.md) |  
| 3      | 📅 --/--/---- | `—`    | [Ver Backlog](./documents/Sprint3.md) |  

</div>  

**Legenda:**  
- ✅ **Finalizada**  
- 🚧 **Em Progresso**  
- `—` **Não iniciado**  

---  

## 📑 Documentação  

- **Backlog do Produto:** [Acesse aqui](./documents/product_backlog-v2.md)  
  Lista de requisitos funcionais e não funcionais, organizados em **User Stories**, conforme o desafio da Secretaria Acadêmica.   
  
- **Backlog do Produto - mapa:** [Acesse aqui](./documents/product_backlop_map.md)  

- **Modelagem do Banco de Dados:** [Acesse aqui](./documents/modelagem_bd.md)  
  Estrutura de entidades e relacionamentos para suportar navegação, perguntas e respostas.  
  
- **Definition of Ready (DoR):** [Acesse aqui](./documents/Definition%20of%20Ready.md)  
  Critérios que definem quando uma *user story* está pronta para entrar em sprint.  
  
- **Definition of Done (DoD):** [Acesse aqui](./documents/Definition%20of%20Done%20.md)  
  Critérios que garantem qualidade e conclusão das tarefas.  
  
- **Diagramas UML:** [Acesse aqui](./documents/uml.md)  
  Casos de uso, classes, sequência e componentes, representando o fluxo do chatbot e gestão de conteúdo.  
  
---

## 📍 Focal Point  
- Focal Point: Prof. André Olímpio  
- Kick-off: 27/03/2026  


## 👨‍💻Equipe 

| Nome | Função | GitHub |Portfólio|
|------|--------|--------|--------|
| Victor Ramos | Scrum Master | [Github](https://github.com/victorramos887/victorramos887) | [Portfólio](https://fatec-jacarei-dsm-portfolio.github.io/ra2581392523037/) |
| Ricardo Ladeira | Product Owner | [Github](https://github.com/rladeiraFatec) | [Portfólio](https://fatec-jacarei-dsm-portfolio.github.io/ra2581392523010) |
| Caio Julião | Desenvolvedor | [Github](https://github.com/caiao93guitar) | [Portfólio](https://fatec-jacarei-dsm-portfolio.github.io/ra2581392523008 ) |
| Jocelio Gomes Silva | Desenvolvedor | [Github](https://github.com/Git-Jocelio) | [Portfólio](https://fatec-jacarei-dsm-portfolio.github.io/ra2581392523040) | 
| Lucas dos Santos Ribeiro | Desenvolvedor | [Github](https://github.com/LucassantosR25) | [Portfólio](https://fatec-jacarei-dsm-portfolio.github.io/ra2581392523004/) |
| Luis Gustavo | Desenvolvedor | [Github](https://github.com/LuisGustavo9) | [Portfólio](https://fatec-jacarei-dsm-portfolio.github.io/ra2581392523041) |


