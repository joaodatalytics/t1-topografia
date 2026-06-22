# WeekPlanner 📅

Aplicação web de planejamento semanal e gestão de tarefas com visualização por membros da equipe.

## Stack

| Camada      | Tecnologia            |
|-------------|----------------------|
| Frontend    | HTML5 · CSS Grid · Vanilla JS |
| Backend     | Python 3.12 + FastAPI |
| Banco       | PostgreSQL 16         |
| Infra       | Docker + Docker Compose |

---

## Início rápido — com Docker (recomendado)

```bash
# 1. Clone / extraia o projeto
cd weekplanner

# 2. Suba tudo
docker compose up --build

# 3. Acesse
open http://localhost        # Frontend
open http://localhost:8000/docs  # Swagger UI da API
```

O PostgreSQL é inicializado automaticamente com o schema e seed data.

---

## Início rápido — sem Docker

### Backend

```bash
cd backend
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# Configure o banco
export DATABASE_URL="postgresql://user:pass@localhost:5432/weekplanner"
# OU use SQLite para testes rápidos (edite main.py linha DATABASE_URL)

uvicorn main:app --reload --port 8000
```

### Banco (PostgreSQL)

```bash
psql -U postgres
CREATE DATABASE weekplanner;
\c weekplanner
\i database/schema.sql
```

### Frontend

```bash
# Modo mock (sem backend) — apenas abra no browser
open frontend/index.html

# Com backend real — edite script.js:
# const USE_MOCK = false;
# const API_BASE = 'http://localhost:8000';

# Ou sirva com qualquer servidor estático:
cd frontend && python -m http.server 3000
```

---

## Estrutura do Projeto

```
weekplanner/
├── database/
│   └── schema.sql          # DDL + seed data
├── backend/
│   ├── main.py             # FastAPI + SQLAlchemy
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/
│   ├── index.html          # Estrutura semântica
│   ├── style.css           # CSS Grid + design system
│   └── script.js           # Vanilla JS (mock + fetch)
├── docker/
│   └── nginx.conf          # Reverse proxy
└── docker-compose.yml
```

---

## Endpoints da API

| Método | Rota             | Descrição                        |
|--------|------------------|----------------------------------|
| GET    | /users           | Lista todos os membros           |
| POST   | /users           | Cria um novo membro              |
| GET    | /tasks           | Lista tarefas (com filtros)      |
| POST   | /tasks           | Cria nova tarefa                 |
| GET    | /tasks/{id}      | Detalhe de uma tarefa            |
| PUT    | /tasks/{id}      | Atualiza tarefa ou status        |
| DELETE | /tasks/{id}      | Remove uma tarefa                |

**Filtros disponíveis em GET /tasks:**
```
?dia=1&turno=manha&status=a_fazer&user_id=2
```

---

## Modelo de Dados

```
users: id, nome, email, avatar, cor, criado_em
tasks: id, titulo, descricao, dia_da_semana (1-7),
       turno (manha|tarde|noite),
       status (a_fazer|em_andamento|concluido),
       user_id, criado_em, atualizado_em
```

---

## Para deploy em AWS EC2

```bash
# Na instância
sudo apt update && sudo apt install docker.io docker-compose -y
git clone <repo> && cd weekplanner

# Edite as variáveis de ambiente em docker-compose.yml
docker compose up -d

# Configure Security Groups para liberar portas 80 e 443
```
