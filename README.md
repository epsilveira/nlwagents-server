# NLW Agents - Server

Este é o backend do projeto **NLW Agents**, desenvolvido durante a Next Level Week da [Rocketseat](https://rocketseat.com.br).

## 🚀 Tecnologias Utilizadas

O projeto foi construído com as seguintes tecnologias e bibliotecas principais:

-   **Node.js**: Ambiente de execução JavaScript.
-   **TypeScript**: Superset do JavaScript que adiciona tipagem estática.
-   **Fastify**: Framework web focado em performance e baixo overhead.
-   **PostgreSQL**: Banco de dados relacional.
-   **pgvector**: Extensão do PostgreSQL para armazenar e consultar embeddings vetoriais.
-   **Drizzle ORM**: ORM "TypeScript-first" para interagir com o banco de dados.
-   **Zod**: Biblioteca para validação de schemas e tipos.
-   **Biome**: Ferramenta para formatação e linting de código.
-   **Docker**: Para containerização do banco de dados.

## ⚙️ Setup e Configuração

Siga os passos abaixo para configurar e rodar o projeto em seu ambiente local.

### Pré-requisitos

-   [Node.js](https://nodejs.org/en/) (v22.x ou superior)
-   [Docker](https://www.docker.com/get-started/) e Docker Compose

### Passos

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/epsilveira/nlwagents-server.git
    cd nlwagents-server/server
    ```

2.  **Instale as dependências:**
    ```bash
    npm install
    ```

3.  **Configure as variáveis de ambiente:**
    Copie o arquivo `.env.example` para um novo arquivo chamado `.env` e, se necessário, ajuste a variável `DATABASE_URL`.
    ```bash
    cp .env.example .env
    ```

4.  **Inicie o banco de dados com Docker:**
    Este comando irá subir um container PostgreSQL com a extensão `pgvector` habilitada.
    ```bash
    docker compose up -d
    ```

5.  **Execute as migrações do banco de dados:**
    Este comando criará as tabelas no banco de dados com base nos schemas definidos em `src/db/schema`.
    ```bash
    npx drizzle-kit migrate
    ```

6.  **(Opcional) Popule o banco de dados:**
    Para popular o banco com dados de teste, execute o script de seed.
    ```bash
    npm run db:seed
    ```

7.  **Inicie o servidor:**
    O servidor iniciará em modo de desenvolvimento com watch na porta definida no seu arquivo `.env` (padrão: 3333).
    ```bash
    npm run dev
    ```

## 📜 Scripts Disponíveis

-   `npm run dev`: Inicia o servidor em modo de desenvolvimento.
-   `npm run start`: Inicia o servidor em modo de produção.
-   `npm run db:seed`: Popula o banco de dados com dados de teste.
-   `npx drizzle-kit generate`: Gera novos arquivos de migração com base em alterações no schema.
-   `npx drizzle-kit migrate`: Aplica as migrações pendentes no banco de dados.
-   `npx drizzle-kit studio`: Abre uma interface web para visualizar e interagir com o banco de dados.

## Endpoints da API

Você pode usar o arquivo `client.http` para testar os endpoints com a extensão REST Client do VS Code.

-   `GET /health`: Verifica a saúde da aplicação.
-   `GET /rooms`: Lista todas as salas cadastradas.