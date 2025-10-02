text
<div align="center">

# 🍽️ Prato Mágico

### Sistema de Gestão de Pedidos para Restaurantes

[![Node.js](https://img.shields.io/badge/Node.js-20.x-green?logo=node.js)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue?logo=typescript)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue?logo=postgresql)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue?logo=docker)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## 📖 Sobre o Projeto

O **Prato Mágico** é uma solução completa para automatizar e otimizar o gerenciamento de pedidos em restaurantes[web:7]. Desenvolvido com arquitetura limpa e princípios SOLID, o sistema permite o cadastro de pratos no menu, criação de pedidos e acompanhamento do status em tempo real através de uma interface web responsiva[web:5][web:10].

### 🎯 Propósito

Resolver os principais desafios enfrentados por restaurantes na gestão manual de pedidos: erros de comunicação, atrasos na entrega e dificuldade no controle financeiro[web:2]. A solução centraliza informações e automatiza processos críticos como cálculo de valores e rastreamento de status[web:7].

### ✨ Principais Funcionalidades

- ✅ **CRUD Completo de Pratos** - Cadastro, edição, listagem e exclusão soft delete
- ✅ **Gerenciamento de Pedidos** - Criação e acompanhamento com status em tempo real
- ✅ **Relacionamento N:N** - Múltiplos pratos por pedido com controle de quantidade
- ✅ **Categorização Inteligente** - Bebidas, pratos principais, sobremesas e entradas
- ✅ **Cálculo Automático** - Valor total computado dinamicamente
- ✅ **Controle de Status** - Fluxo validado: RECEBIDO → EM_PREPARO → PRONTO → ENTREGUE
- ✅ **Auditoria Completa** - Timestamps automáticos e histórico de mudanças

---

## 🏗️ Arquitetura

O projeto segue os princípios de **Clean Architecture** com separação clara de responsabilidades[web:2][web:9]:

src/
├── presentation/ # Controllers (recebem requisições HTTP)
├── application/ # Use Cases e Services (regras de negócio)
├── domain/ # Entidades e Value Objects (lógica de domínio)
└── infrastructure/ # Repositórios, DB e adaptadores externos

text

### 🎨 Princípios SOLID Aplicados

| Princípio | Aplicação |
|-----------|-----------|
| **SRP** | Cada service tem uma única responsabilidade (DishService, OrderService, OrderStatusService) |
| **OCP** | Estratégias extensíveis para cálculo de preços (descontos, taxas) sem modificar código existente |
| **LSP** | Todos os repositórios implementam interface base sem quebrar contratos |
| **ISP** | Interfaces segregadas (IDishReader, IDishWriter) ao invés de uma única interface |
| **DIP** | Controllers dependem de abstrações (interfaces), não de classes concretas |

---

## 🚀 Tecnologias

### Backend
- **[Node.js](https://nodejs.org/)** v20+ - Runtime JavaScript
- **[TypeScript](https://www.typescriptlang.org/)** v5+ - Superset com tipagem estática
- **[Express.js](https://expressjs.com/)** - Framework web minimalista
- **[TypeORM](https://typeorm.io/)** - ORM com suporte a Active Record e Data Mapper
- **[PostgreSQL](https://www.postgresql.org/)** v15 - Banco de dados relacional
- **[Docker](https://www.docker.com/)** + **[Docker Compose](https://docs.docker.com/compose/)** - Containerização e orquestração

### Frontend
- **[React](https://react.dev/)** v18+ com TypeScript
- **[React Router](https://reactrouter.com/)** v6 - Roteamento
- **[React Query](https://tanstack.com/query)** - Gerenciamento de estado de servidor
- **[React Hook Form](https://react-hook-form.com/)** + **[Zod](https://zod.dev/)** - Validação de formulários
- **[TailwindCSS](https://tailwindcss.com/)** - Estilização com utility-first

### Ferramentas de Desenvolvimento
- **[Jest](https://jestjs.io/)** + **[Supertest](https://github.com/ladjs/supertest)** - Testes unitários e de integração
- **[Swagger UI](https://swagger.io/tools/swagger-ui/)** - Documentação interativa da API
- **[pgAdmin](https://www.pgadmin.org/)** - Interface gráfica para PostgreSQL
- **[ESLint](https://eslint.org/)** + **[Prettier](https://prettier.io/)** - Linting e formatação de código

---

## 📋 Pré-requisitos

Antes de começar, certifique-se de ter instalado[web:7][web:10]:

- **[Git](https://git-scm.com/)** v2.30+
- **[Node.js](https://nodejs.org/)** v18+ e npm/yarn
- **[Docker](https://www.docker.com/)** v20+
- **[Docker Compose](https://docs.docker.com/compose/)** v2+

---

## ⚙️ Instalação e Configuração

### 1️⃣ Clonar o Repositório

Clone o projeto
git clone https://github.com/seu-usuario/prato-magico.git

Entre no diretório
cd prato-magico

text

### 2️⃣ Configurar Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto baseado no `.env.example`:

Backend
NODE_ENV=development
PORT=3000

Database
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_DATABASE=prato_magico

pgAdmin (opcional)
PGADMIN_EMAIL=admin@admin.com
PGADMIN_PASSWORD=admin

text

### 3️⃣ Instalar Dependências

Backend
npm install

Frontend (se estiver em monorepo)
cd frontend
npm install

text

### 4️⃣ Subir o Banco de Dados com Docker

Inicia PostgreSQL e pgAdmin em containers
docker-compose up -d

Verificar se os containers estão rodando
docker ps

text

**Acessar pgAdmin:**
- URL: `http://localhost:5050`
- Email: `admin@admin.com`
- Senha: `admin`

### 5️⃣ Executar Migrations

Cria as tabelas no banco de dados
npm run migration:run

text

### 6️⃣ Iniciar o Servidor

Ambiente de desenvolvimento
npm run dev

Ambiente de produção
npm run build
npm start

text

O servidor estará disponível em `http://localhost:3000`[web:10].

### 7️⃣ Acessar Documentação da API

Após iniciar o servidor, acesse:
- **Swagger UI**: `http://localhost:3000/api-docs`

---

## 🔗 Endpoints da API

### Pratos (Dishes)

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `POST` | `/api/v1/dishes` | Criar novo prato |
| `GET` | `/api/v1/dishes` | Listar pratos (paginado) |
| `GET` | `/api/v1/dishes/:id` | Obter detalhes de um prato |
| `PUT` | `/api/v1/dishes/:id` | Atualizar prato existente |
| `DELETE` | `/api/v1/dishes/:id` | Excluir prato (soft delete) |

### Pedidos (Orders)

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `POST` | `/api/v1/orders` | Criar novo pedido |
| `GET` | `/api/v1/orders` | Listar pedidos (paginado) |
| `GET` | `/api/v1/orders/:id` | Obter detalhes de um pedido |
| `PATCH` | `/api/v1/orders/:id/status` | Atualizar status do pedido |

**Exemplo de Requisição:**

Criar um novo prato
curl -X POST http://localhost:3000/api/v1/dishes
-H "Content-Type: application/json"
-d '{
"name": "Feijoada Completa",
"description": "Feijoada tradicional com acompanhamentos",
"price": 45.90,
"category": "prato principal"
}'

text

---

## 🐳 Docker e PostgreSQL

### Estrutura do docker-compose.yml

version: '3.8'

services:
postgres:
image: postgres:15-alpine
container_name: prato_magico_db
restart: always
environment:
POSTGRES_USER: ${DB_USERNAME}
POSTGRES_PASSWORD: ${DB_PASSWORD}
POSTGRES_DB: ${DB_DATABASE}
ports:
- "${DB_PORT}:5432"
volumes:
- postgres_data:/var/lib/postgresql/data

pgadmin:
image: dpage/pgadmin4:latest
container_name: prato_magico_pgadmin
restart: always
environment:
PGADMIN_DEFAULT_EMAIL: ${PGADMIN_EMAIL}
PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_PASSWORD}
ports:
- "5050:80"
depends_on:
- postgres

volumes:
postgres_data:

text

### Comandos Úteis do Docker

Subir todos os serviços
docker-compose up -d

Ver logs dos containers
docker-compose logs -f

Parar todos os serviços
docker-compose down

Parar e remover volumes (apaga dados do banco)
docker-compose down -v

Reconstruir imagens
docker-compose build --no-cache

Acessar o terminal do PostgreSQL
docker exec -it prato_magico_db psql -U postgres -d prato_magico

text

### Conectar ao PostgreSQL no pgAdmin

1. Acesse `http://localhost:5050`
2. Faça login com as credenciais configuradas
3. Clique em **Add New Server**
4. Configure:
   - **Name**: Prato Mágico DB
   - **Host**: postgres (nome do serviço no Docker)
   - **Port**: 5432
   - **Username**: postgres
   - **Password**: postgres

---

## 🌿 Git Flow

Este projeto segue o modelo de **Git Flow** para organização de branches e versionamento[web:1][web:2].

### Estrutura de Branches

| Branch | Descrição | Exemplo |
|--------|-----------|---------|
| `main` | Código em produção (sempre estável) | - |
| `develop` | Branch de desenvolvimento (integração) | - |
| `feature/*` | Novas funcionalidades | `feature/add-dish-filter` |
| `bugfix/*` | Correções de bugs em desenvolvimento | `bugfix/fix-order-calculation` |
| `hotfix/*` | Correções urgentes em produção | `hotfix/fix-critical-crash` |
| `release/*` | Preparação para nova versão | `release/v1.2.0` |

### Fluxo de Trabalho

#### 1. Criar Nova Feature

Atualizar develop
git checkout develop
git pull origin develop

Criar branch de feature
git checkout -b feature/nome-da-feature

Fazer commits
git add .
git commit -m "feat: adiciona filtro de pratos por categoria"

Push para o repositório
git push origin feature/nome-da-feature

text

#### 2. Finalizar Feature

Voltar para develop
git checkout develop

Merge da feature (usando --no-ff para preservar histórico)
git merge --no-ff feature/nome-da-feature

Push para origin
git push origin develop

Deletar branch local
git branch -d feature/nome-da-feature

Deletar branch remota
git push origin --delete feature/nome-da-feature

text

#### 3. Criar Release

Criar branch de release a partir de develop
git checkout -b release/v1.2.0 develop

Fazer ajustes finais (atualizar versão, changelog, etc)
git commit -m "chore: bump version to 1.2.0"

Merge na main
git checkout main
git merge --no-ff release/v1.2.0

Criar tag
git tag -a v1.2.0 -m "Release version 1.2.0"

Merge de volta em develop
git checkout develop
git merge --no-ff release/v1.2.0

Push
git push origin main develop --tags
git branch -d release/v1.2.0

text

#### 4. Hotfix em Produção

Criar hotfix a partir de main
git checkout -b hotfix/fix-critical-bug main

Corrigir o problema
git commit -m "fix: corrige cálculo de preço total"

Merge na main
git checkout main
git merge --no-ff hotfix/fix-critical-bug
git tag -a v1.2.1 -m "Hotfix 1.2.1"

Merge de volta em develop
git checkout develop
git merge --no-ff hotfix/fix-critical-bug

Push
git push origin main develop --tags
git branch -d hotfix/fix-critical-bug

text

### Convenção de Commits

Seguimos o padrão **[Conventional Commits](https://www.conventionalcommits.org/)**[web:2]:

<tipo>(<escopo>): <descrição>

[corpo opcional]

[rodapé opcional]

text

**Tipos principais:**
- `feat`: Nova funcionalidade
- `fix`: Correção de bug
- `docs`: Mudanças na documentação
- `style`: Formatação de código (sem mudança lógica)
- `refactor`: Refatoração de código
- `test`: Adição ou correção de testes
- `chore`: Tarefas de build, configuração, etc

**Exemplos:**

git commit -m "feat(orders): adiciona endpoint de listagem de pedidos"
git commit -m "fix(dishes): corrige validação de preço negativo"
git commit -m "docs(readme): atualiza instruções de instalação"
git commit -m "refactor(services): aplica princípio DIP em OrderService"

text

---

## 🗄️ Modelagem do Banco de Dados

### Diagrama ER

┌─────────────────┐ ┌──────────────────┐ ┌─────────────────┐
│ Dishes │ │ Orders_Dishes │ │ Orders │
├─────────────────┤ ├──────────────────┤ ├─────────────────┤
│ id (PK) │────────<│ dish_id (FK) │>────────│ id (PK) │
│ name │ │ order_id (FK) │ │ status │
│ description │ │ quantity │ │ total_price │
│ price │ │ unit_price │ │ created_at │
│ category │ └──────────────────┘ │ updated_at │
│ is_active │ └─────────────────┘
│ created_at │
│ updated_at │
└─────────────────┘

text

### Tabelas

#### `dishes`

| Campo | Tipo | Restrições | Descrição |
|-------|------|-----------|-----------|
| `id` | UUID | PK | Identificador único |
| `name` | VARCHAR(100) | NOT NULL | Nome do prato |
| `description` | VARCHAR(500) | NULL | Descrição detalhada |
| `price` | DECIMAL(10,2) | NOT NULL, > 0 | Preço unitário |
| `category` | ENUM | NOT NULL | bebida, prato principal, sobremesa, entrada |
| `is_active` | BOOLEAN | DEFAULT true | Status de ativação |
| `created_at` | TIMESTAMP | NOT NULL | Data de criação |
| `updated_at` | TIMESTAMP | NOT NULL | Data de atualização |

#### `orders`

| Campo | Tipo | Restrições | Descrição |
|-------|------|-----------|-----------|
| `id` | UUID | PK | Identificador único |
| `status` | ENUM | NOT NULL | RECEBIDO, EM_PREPARO, PRONTO, ENTREGUE |
| `total_price` | DECIMAL(10,2) | NOT NULL | Valor total do pedido |
| `created_at` | TIMESTAMP | NOT NULL | Data de criação |
| `updated_at` | TIMESTAMP | NOT NULL | Data de atualização |

#### `orders_dishes` (Tabela de Junção)

| Campo | Tipo | Restrições | Descrição |
|-------|------|-----------|-----------|
| `dish_id` | UUID | FK, PK | Referência ao prato |
| `order_id` | UUID | FK, PK | Referência ao pedido |
| `quantity` | INTEGER | NOT NULL, > 0 | Quantidade do prato |
| `unit_price` | DECIMAL(10,2) | NOT NULL | Preço unitário no momento do pedido |

---

## 🧪 Testes

Rodar todos os testes
npm test

Testes com coverage
npm run test:coverage

Testes em modo watch
npm run test:watch

Testes de integração
npm run test:integration

text

### Estrutura de Testes

tests/
├── unit/ # Testes unitários de services e entidades
├── integration/ # Testes de API end-to-end
└── mocks/ # Mocks e fixtures

text

---

## 🎨 Identidade Visual

### Paleta de Cores

| Cor | Hex | Uso |
|-----|-----|-----|
| Primária | `#FF6B35` | CTAs, destaques |
| Secundária | `#004E89` | Navegação, headers |
| Sucesso | `#06D6A0` | Confirmações |
| Erro | `#EF476F` | Alertas, validações |
| Neutro Escuro | `#2B2D42` | Textos principais |
| Neutro Claro | `#F7F7F7` | Backgrounds |

### Tipografia

- **Primary**: Inter (títulos e interface)
- **Secondary**: Roboto (corpo de texto)

---

## 📦 Deploy

### Backend (Node.js)

Build da aplicação
npm run build

Iniciar em produção
NODE_ENV=production npm start

text

### Frontend (React)

Build otimizado
npm run build

Arquivos gerados em /dist ou /build
text

**Plataformas recomendadas:**
- Backend: Railway, Render, Fly.io, AWS
- Frontend: Vercel, Netlify, Cloudflare Pages
- Database: Neon, Supabase, Railway

---


## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes[web:7].

---

## 📚 Recursos Adicionais

- [Documentação do TypeORM](https://typeorm.io/)
- [Guia do Express.js](https://expressjs.com/)
- [React Documentation](https://react.dev/)
- [Docker Documentation](https://docs.docker.com/)
- [Git Flow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)

---

<div align="center">

**[⬆ Voltar ao topo](#-prato-mágico)**

</div>
