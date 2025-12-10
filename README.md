# 📘 Instituto Alma – API
API RESTful desenvolvida em ASP.NET Core com autenticação JWT para gestão de atividades, eventos, ouvidoria, doações, transparência e usuários. Este backend fornece os endpoints utilizados pelo site e painel administrativo do Instituto Alma.

---
## 📑 Sumário

- [Autenticação](#-autenticação)
- [Endpoints da API](#-endpoints-da-api)
  - [Atividades](#-atividades)
  - [Eventos](#-eventos)
  - [Ouvidoria](#-ouvidoria)
  - [Doações](#-doações)
  - [Transparência](#-transparência)
- [Backend Publicado no Azure](#-backend-publicada-no-azure)
- [Frontend Publicado no Vercel](#-frontend-publicado-no-vercel)
- [Como Rodar o Projeto Localmente](#-como-rodar-o-projeto-localmente)
- [Como obter o JWT](#-Como-obter-o-token-JWT-(Login))
- [Perfil de Administrador](#-Usuário-Administrador-(Ambiente-de-Desenvolvimento))
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)

---
## 🔐 Autenticação
Algumas rotas exigem envio de um JWT no header:
Authorization: Bearer {seu_token}

---
## 📁 Endpoints da API
A API está organizada nos seguintes módulos:
- Atividades
- Eventos
- Ouvidoria
- Doação
- Transparência
- Usuários

---

Abaixo estão todos os endpoints, baseados fielmente na documentação Swagger.
## 📝 Atividades 
### GET /api/Atividades
Lista todas as atividades.


🔓 Acesso livre.

### POST /api/Atividades
Cria uma nova atividade.


🔐 Requer JWT.


📤 multipart/form-data)

Campos obrigatórios:
- Titulo
- Descricao
- ImagemArquivo (📤 arquivo)

### GET /api/Atividades/{id}
Obtém os detalhes de uma atividade específica.


🔓 Acesso livre. 

### PUT /api/Atividades/{id}
Atualiza uma atividade existente.


🔐 Requer JWT.


📤 multipart/form-data


Campos opcionais:
- Titulo
- Descricao
- ImagemArquivo (📤 arquivo)

### DELETE /api/Atividades/{id}
Exclui uma atividade.


🔐 Requer JWT.

---
## 🎉 Eventos
### GET /api/Eventos
Retorna todos os eventos.


🔓 Acesso livre.

### POST /api/Eventos
Cria um novo evento.


🔐 Requer JWT.


📤 multipart/form-data


Campos obrigatórios:
- Titulo
- Descricao
- LocalEvento
- ImagemArquivo (📤 arquivo)


Campos opcionais:
- DataEvento (date-time)

### GET /api/Eventos/{id}
Retorna um evento específico.


🔓 Acesso livre.

### PUT /api/Eventos/{id}
Atualiza os dados de um evento.


🔐 Requer JWT.


📤 multipart/form-data


Campos opcionais:
- Titulo
- Descricao
- DataEvento
- LocalEvento
- ImagemArquivo (📤 arquivo)

### DELETE /api/Eventos/{id}
Exclui um evento.


🔐 Requer JWT.

---
## 📨 Ouvidoria
### GET /api/Ouvidoria
Lista todas as mensagens enviadas.


🔐 Requer JWT.

### POST /api/Ouvidoria
Envia uma nova mensagem de ouvidoria.


🔐 Requer JWT(Usuario).


Campos obrigatórios:
- Titulo
- Descricao
- EmailRemetente (email válido)

### GET /api/Ouvidoria/{id}
Retorna uma mensagem específica.


🔐 Requer JWT.

### PUT /api/Ouvidoria/{id}
Atualiza os dados da mensagem.


🔐 Requer JWT.


Campos opcionais:
- Titulo
- Descricao

---
## 💰 Doações
### POST /api/Doacao
Registra uma nova doação.


JSON
Body baseado em DoacaoCreateDTO ("valor da doação" e "descrição" <-opcional )

### POST /api/Doacao/webhook
Webhook para receber notificações externas (Mercado Pago).


🔓 Acesso livre.

### GET /api/Doacao/me
Retorna as doações feitas pelo usuário autenticado.


🔐 Requer JWT.

### GET /api/Doacao/admin
Retorna todas as doações (acesso administrativo).


🔐 Requer JWT.

---
## 📄 Transparência
### GET /api/Transparencia
Lista todos os documentos de transparência.


🔓 Acesso livre.

### POST /api/Transparencia
Envia um novo documento PDF.


🔐 Requer JWT.


📤 multipart/form-data


Campos obrigatórios:
- Titulo
- PdfFile (📤 arquivo)
- Campos opcionais:
- Descricao

### GET /api/Transparencia/{id}
Retorna informações de um documento.


🔓 Acesso livre.

### DELETE /api/Transparencia/{id}
Exclui um registro de transparência.


🔐 Requer JWT.

### PUT /api/Transparencia/{id}
Atualiza um registro de transparência.


🔐 Requer JWT.


📤 multipart/form-data


Campos opcionais:
- Titulo
- Descricao
- PdfFile (📤 arquivo)

### GET /api/Transparencia/download/{id}
Baixa o arquivo PDF.


🔓 Acesso livre.

---
## 🌐 Backend publicada no Azure:
[https://ads2-2025-2-djcbfjadeparacd0.eastus-01.azurewebsites.net/swagger/index.html](https://ads2-2025-2-djcbfjadeparacd0.eastus-01.azurewebsites.net/swagger/index.html)


## 🌐 Frontend publicado no Vercel:
[https://alma-react-hmof.vercel.app](https://alma-react-hmof.vercel.app/)

---

## 🚀 Como Rodar o Backend Localmente

Siga os passos abaixo para rodar o projeto ASP.NET Core na sua máquina.

### 📌 1. Clone o repositório
git clone https://github.com/AndreFerreira30/Api_Alma.git
cd ApiAlma

### 📌 2. Instale as dependências
dotnet restore

### 📌 3. Configure o banco de dados
O projeto usa Entity Framework Core.
Crie o banco automaticamente rodando:
"dotnet ef database update"
Se der erro de “dotnet ef não encontrado”, instale o pacote global:
"dotnet tool install --global dotnet-ef"

### 📌 4. Inicie a API
dotnet run
A API subirá em:
- https://localhost:7220
- http://localhost:5091

### 📌 5. Acesse a documentação Swagger
Abra:
https://localhost:7220/swagger/index.html
Agora você pode testar todos os endpoints localmente.

---
## 🔑 Como obter o token JWT (Login)

Para acessar rotas protegidas, você precisa de um token JWT.  
Siga os passos abaixo para gerar seu token:

### 1️⃣ Enviar uma requisição de login  
Endpoint: POST /api/Usuarios/login
### Body (JSON):
{
  "email": "seu_email_aqui",
  "senha": "sua_senha_aqui"
}

### 2️⃣ Resposta
Se as credenciais estiverem corretas, a API retorna algo assim:
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}

### 3️⃣ Usar o token nas requisições protegidas
Adicione o token no header:
Authorization: Bearer SEU_TOKEN_AQUI

Agora você pode acessar as rotas de Usuario, como:
- POST /api/Ouvidoria
Para as demais rotas protegidas será necessário um perfil de administrador.

---
## 👤 Usuário Administrador (Ambiente de Desenvolvimento)

O sistema utiliza um campo booleano IsAdmin para controlar as permissões do usuário.  
Durante o processo de autenticação, o backend gera o claim:

new Claim(ClaimTypes.Role, usuario.IsAdmin ? "Admin" : "User")

Por motivos de segurança, o usuário administrador utilizado no ambiente publicado **não é divulgado publicamente**.

### Como habilitar um usuário administrador no ambiente local

Se você estiver rodando o projeto localmente, pode criar seus próprios usuários administrativos:

1. Registre um novo usuário usando:
   - POST /api/Usuarios/registrar
2. No banco de dados local, edite o registro do usuário e defina:
   - IsAdmin = true

> Isso fará com que o token JWT gerado inclua o claim "Admin", permitindo acessar rotas protegidas por autorização administrativa.

Este procedimento garante segurança no ambiente público e flexibilidade no ambiente de desenvolvimento.

---
## 🧰 Tecnologias Utilizadas:
- ASP.NET Core
- Entity Framework Core
- SQLite / SQL Server
- Autenticação com JWT
- Upload de arquivos via multipart/form-data
- Swagger (OpenAPI)
- Integração com Mercado Pago (webhook)
---
