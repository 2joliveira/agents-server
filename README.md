# NLW Agents

API desenvolvida durante um evento da Rocketseat, com foco em processamento de linguagem natural e inteligência artificial. A aplicação recebe áudios enviados pelo front-end, realiza a transcrição automática e armazena os dados em um banco de dados. Utilizando embeddings e o modelo Gemini, do Google, a API interpreta perguntas feitas pelos usuários e busca, de forma contextual, informações relevantes nos áudios transcritos para gerar respostas precisas e alinhadas ao conteúdo enviado.

## 🚀 Tecnologias

- **Node.js**
- **Fastify**
- **PostgreSQL** com extensão **pgvector** para vetores
- **Drizzle ORM**
- **Zod**
- **Docker** - Containerização do banco de dados
- **Gemini API**

## 🏗️ Arquitetura

O projeto segue uma arquitetura modular com:

- **Separação de responsabilidades** entre rotas, schemas e conexão com banco
- **Validação de schemas** com Zod para type safety
- **ORM type-safe** com Drizzle para operações de banco de dados
- **Validação de variáveis de ambiente** centralizadas

## 🏗️ Arquitetura

O projeto segue uma arquitetura modular com:

- **Separação de responsabilidades entre rotas (http/routes), schemas (db/schemas) e serviços (services)**

- **Validação de schemas com Zod para garantir segurança de tipos**

- **ORM type-safe com Drizzle para operações no banco de dados**

- **Validação de variáveis de ambiente centralizada em services/env.ts**

- **Scripts de inicialização do banco em docker/setup.sql com suporte ao Docker Compose**

- **Organização clara entre camadas de dados, lógica de negócio e transporte HTTP**



## ⚙️ Setup e Configuração

### Pré-requisitos

- Node.js (versão com suporte a `--experimental-strip-types`)
- Docker e Docker Compose

### 1. Clone o repositório

### 2. Configure o banco de dados
```bash
docker-compose up -d
```

### 3. Configure as variáveis de ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
PORT=3333
DATABASE_URL=postgresql://docker:docker@localhost:5432/agents
```

### 4. Instale as dependências
```bash
npm install
```

### 5. Execute as migrações do banco
```bash
npx drizzle-kit migrate
```

### 6. (Opcional) Popule o banco com dados de exemplo
```bash
npm run db:seed
```

### 7. Execute o projeto

**Desenvolvimento:**
```bash
npm run dev
```

**Produção:**
```bash
npm run start
```

## 📚 Scripts Disponíveis

- `npm run dev` - Executa o servidor em modo de desenvolvimento com hot reload
- `npm run start` - Executa o servidor em modo de produção
- `npm run db:seed` - Popula o banco de dados com dados de exemplo

## 🌐 Endpoints

A API estará disponível em `http://localhost:3333`

- `GET /rooms` - Lista as salas disponíveis
- `GET /rooms/:roomId/questions` - Lista as perguntas de uma sala específica
- `POST /rooms` - Cria sala de perguntas
- `POST /rooms/:roomId/questions` - Cria uma pergunta em uma sala específica
- `POST /rooms/:roomId/audio` - Faz o upload do áudio salvando a trancrição no Bando de dados
