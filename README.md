# TodoList - Gerenciador de Tarefas

Projeto desenvolvido durante o minicurso de Java com Spring Boot da Rocketseat. Uma API REST para gerenciamento de tarefas com autenticação básica.

## Tecnologias Utilizadas

- Java 17
- Spring Boot 3.5.5
- Spring Data JPA
- H2 Database (em memória)
- BCrypt para criptografia de senhas
- Lombok
- Maven

## Funcionalidades

### Usuários
- Cadastro de usuários
- Autenticação básica (Basic Auth)
- Senhas criptografadas com BCrypt

### Tarefas
- Criar tarefas
- Listar tarefas do usuário autenticado
- Atualizar tarefas
- Validação de datas (início e fim)
- Controle de propriedade (usuário só pode alterar suas próprias tarefas)

## Como Executar

1. Clone o repositório
2. Navegue até o diretório do projeto
3. Execute o comando:
```bash
mvn spring-boot:run
```

A aplicação estará disponível em `http://localhost:8080`

## Endpoints

### Usuários

**POST /users/**
- Cadastra um novo usuário
- Body:
```json
{
  "username": "usuario",
  "name": "Nome do Usuário",
  "password": "senha123"
}
```

### Tarefas

**POST /tasks/**
- Cria uma nova tarefa
- Requer autenticação Basic Auth
- Body:
```json
{
  "title": "Título da tarefa",
  "description": "Descrição da tarefa",
  "startAt": "2024-01-01T10:00:00",
  "endAt": "2024-01-01T18:00:00",
  "priority": "ALTA"
}
```

**GET /tasks/**
- Lista todas as tarefas do usuário autenticado
- Requer autenticação Basic Auth

**PUT /tasks/{id}**
- Atualiza uma tarefa específica
- Requer autenticação Basic Auth
- Usuário só pode alterar suas próprias tarefas

## Validações

- Título da tarefa: máximo 50 caracteres
- Data de início deve ser maior que a data atual
- Data de fim deve ser maior que a data atual
- Data de início deve ser anterior à data de fim
- Usuários não podem alterar tarefas de outros usuários

## Banco de Dados

O projeto utiliza o H2 Database em memória. O console do H2 pode ser acessado em:
- URL: `http://localhost:8080/h2-console`
- JDBC URL: `jdbc:h2:mem:todolist`
- Username: `admin`
- Password: `admin`

## Estrutura do Projeto

```
src/main/java/br/com/miguelgewehr/todolist/
├── TodolistApplication.java
├── task/
│   ├── TaskController.java
│   ├── TaskModel.java
│   ├── ITaskRepository.java
│   └── filter/
│       └── FilterTaskAuth.java
├── user/
│   ├── UserController.java
│   ├── UserModel.java
│   └── IUserRepository.java
└── utils/
    └── utils.java
```

## Autenticação

A API utiliza Basic Authentication. Para acessar os endpoints de tarefas, inclua o header:

```
Authorization: Basic <base64(username:password)>
```

## Minicurso Rocketseat

Este projeto foi desenvolvido como parte do minicurso gratuito de Java com Spring Boot oferecido pela Rocketseat, abordando conceitos fundamentais como:

- Configuração de projeto Spring Boot
- Criação de APIs REST
- Persistência de dados com JPA
- Autenticação e segurança
- Validações e tratamento de erros
