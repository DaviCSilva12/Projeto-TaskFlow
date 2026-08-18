# TaskFlow

API REST para gerenciamento de tarefas, desenvolvida com Laravel e PHP. Permite que usuários se cadastrem, façam login e gerenciem suas próprias tarefas através de operações CRUD completas, com autenticação via token (Laravel Sanctum).

## Tecnologias utilizadas

- **PHP 8.4** / **Laravel 11**
- **MySQL** — banco de dados relacional
- **Laravel Sanctum** — autenticação via API token
- **Docker** e **Docker Compose** — containerização do ambiente
- **Postman** — testes manuais dos endpoints

## Funcionalidades

- Cadastro e login de usuários
- Autenticação via Bearer Token
- CRUD completo de tarefas (criar, listar, visualizar, atualizar, excluir)
- Isolamento de dados: cada usuário só acessa suas próprias tarefas
- Logout com invalidação de token

## Como rodar o projeto

### Pré-requisitos
- Docker e Docker Compose instalados

### Passos

1. Clone o repositório:
```bash
git clone https://github.com/DaviCSilva12/Projeto-TaskFlow.git
cd Projeto-TaskFlow
```

2. Copie o arquivo de ambiente de exemplo:
```bash
cp backend/.env.example backend/.env
```
Edite `backend/.env` e configure as variáveis do banco:
```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=taskflow
DB_USERNAME=taskflow
DB_PASSWORD=secret
```

3. Suba os containers:
```bash
docker-compose up -d --build
```

4. Rode as migrations:
```bash
docker exec -it taskflow_backend php artisan migrate
```

5. A API estará disponível em `http://localhost:8000`.

## Endpoints da API

### Autenticação (públicos)

| Método | Rota | Descrição |
|---|---|---|
| POST | `/api/register` | Cria um novo usuário |
| POST | `/api/login` | Autentica e retorna um token |

### Tarefas (protegidos — exigem Bearer Token)

| Método | Rota | Descrição |
|---|---|---|
| GET | `/api/tasks` | Lista as tarefas do usuário logado |
| POST | `/api/tasks` | Cria uma nova tarefa |
| GET | `/api/tasks/{id}` | Exibe uma tarefa específica |
| PUT/PATCH | `/api/tasks/{id}` | Atualiza uma tarefa |
| DELETE | `/api/tasks/{id}` | Exclui uma tarefa |
| POST | `/api/logout` | Invalida o token atual |

### Exemplo de requisição — criar tarefa

```json
POST /api/tasks
Authorization: Bearer {seu_token}

{
  "title": "Estudar Laravel",
  "description": "Terminar o CRUD do TaskFlow",
  "status": "pending",
  "due_date": "2026-08-20"
}
```

## Estrutura do projeto

```
TaskFlow/
├── backend/           # Aplicação Laravel
│   ├── app/
│   │   ├── Http/Controllers/
│   │   └── Models/
│   ├── database/migrations/
│   └── routes/api.php
├── docker/backend/    # Dockerfile do backend
└── docker-compose.yml
```

## Próximos passos

- [ ] Frontend em React
- [ ] Deploy em Google Cloud Platform com Kubernetes
- [ ] Testes automatizados (PHPUnit)

## Autor

Davi — projeto desenvolvido como estudo de Laravel, Docker e arquitetura de APIs REST.