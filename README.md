# NLW Agents - Server

Este é o backend da aplicação **NLW Agents**, uma plataforma de perguntas e respostas que utiliza a API do Google Gemini para gerar respostas inteligentes.

## Sobre o Projeto

O servidor é responsável por gerenciar salas, perguntas e interagir com a API do Gemini para fornecer respostas baseadas em áudio ou texto. Ele oferece uma API REST para que o frontend possa consumir os dados e utiliza WebSockets para comunicação em tempo real.

## ✨ Tecnologias Principais

O projeto foi construído com as seguintes tecnologias e bibliotecas principais:

-   **[Node.js](https://nodejs.org/en)**: Um ambiente de execução JavaScript server-side que permite construir aplicações de rede escaláveis. É a base para toda a nossa aplicação backend.
-   **[TypeScript](https://www.typescriptlang.org/)**: Um superset do JavaScript que adiciona tipagem estática. Usamos para escrever um código mais robusto, legível e com menos bugs em tempo de execução.
-   **[Fastify](https://www.fastify.io/)**: Um framework web para Node.js, focado em alta performance e baixo overhead. É utilizado para construir nossa API REST de forma rápida e eficiente.
-   **[Drizzle ORM](https://orm.drizzle.team/)**: Um ORM (Object-Relational Mapper) "headless" para TypeScript. Ele oferece uma maneira segura, performática e flexível de interagir com o banco de dados SQL, escrevendo queries com sintaxe muito próxima ao SQL puro, mas com a segurança de tipos do TypeScript.
-   **[PostgreSQL](https://www.postgresql.org/)**: Um poderoso sistema de banco de dados objeto-relacional de código aberto, conhecido por sua robustez e conformidade com os padrões SQL.
-   **[Zod](https://zod.dev/)**: Uma biblioteca de declaração e validação de esquemas para TypeScript. É usada para validar os dados de entrada das requisições HTTP, garantindo que apenas dados válidos cheguem às nossas rotas.
-   **[Google Gemini API](https://ai.google.dev/)**: A API de IA generativa do Google, utilizada para processar as perguntas (incluindo chunks de áudio) e gerar respostas coesas e contextuais.
-   **[tsx](https://github.com/esbuild-kit/tsx)**: Um executor de TypeScript para Node.js que utiliza a velocidade do esbuild. É usado no script `dev` para executar o servidor em modo de desenvolvimento com hot-reload, agilizando o fluxo de trabalho.

## ⚙️ Setup e Configuração

Siga os passos abaixo para configurar e rodar o projeto em seu ambiente local.

### Pré-requisitos

-   [Node.js](https://nodejs.org/en/) (v22.x ou superior - com suporte a --experimental-strip-types)
-   [Docker](https://www.docker.com/get-started/) e Docker Compose
-   Uma chave de API do Google Gemini

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
    Copie o arquivo de exemplo `.env.example` para um novo arquivo chamado `.env` e preencha as variáveis.

    ```bash
    cp .env.example .env
    ```

    Abra o arquivo `.env` e adicione sua `GEMINI_API_KEY`. A `DATABASE_URL` já está configurada para o container Docker do passo anterior.

4.  **Inicie o banco de dados com Docker:**
    O projeto inclui um arquivo `docker-compose.yml` para facilitar a inicialização do banco de dados. Execute o comando abaixo para iniciar o container do PostgreSQL em segundo plano.

    ```bash
    docker compose up -d
    ```

    *Este comando sobe um container PostgreSQL com as credenciais e porta definidas no `docker-compose.yml`, que são as mesmas do arquivo `.env.example`.*

5.  **Execute as migrações do banco de dados:**
    Este comando irá aplicar os arquivos de migração SQL gerados pelo Drizzle Kit, criando as tabelas no seu banco de dados.

    ```bash
    npm run db:generate
    npm run db:migrate
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
-   `npm run db:generate`: Gera novos arquivos de migração com base em alterações no schema.
-   `npm run db:migrate`: Aplica as migrações pendentes no banco de dados.
-   `npx drizzle-kit studio`: Abre uma interface web para visualizar e interagir com o banco de dados.

## Endpoints da API

Você pode usar o arquivo `client.http` para testar os endpoints com a extensão REST Client do VS Code.

-   `GET /health`: Verifica a saúde da aplicação.
-   `GET /rooms`: Lista todas as salas cadastradas.
-   `GET /rooms/{{roomId}}/questions`: Lista as perguntas de uma sala específica.
-   `POST /rooms`: Cria uma nova sala.
-   `POST /rooms/{{roomId}}/questions`: Cria uma nova pergunta para uma sala