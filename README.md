# 🧪 Desafio Técnico - Estágio / Desenvolvedor Júnior (Java + Spring)

Seja bem-vindo(a) ao desafio técnico para seleção de estagiários e desenvolvedores júnior!

Este projeto tem como objetivo avaliar seus conhecimentos em **Java**, **Spring Boot**, **JPA/Hibernate**, **PostgreSQL** e boas práticas de desenvolvimento de APIs RESTful.

## 🧩 Descrição do Projeto

Você deverá desenvolver uma API REST para o gerenciamento de **Clientes** e suas **Contas**.

O projeto deve ser implementado com as seguintes tecnologias:

- Java 8 ou superior
- Spring Boot (Web, Data JPA)
- PostgreSQL (Banco de dados obrigatório)
- Validação com Bean Validation (opcional, uso não obrigatório)
- Lombok (opcional)
- JUnit (para testes)

---

## 🧱 Estrutura das Entidades

### 📌 Cliente

| Campo     | Tipo      | Regras de negócio                          |
|-----------|-----------|--------------------------------------------|
| id        | Long      | Gerado automaticamente                     |
| nome      | String    | Obrigatório                                |
| cpf       | String    | Obrigatório, único                         |
| telefone  | String    | Opcional                                   |
| email     | String    | Opcional                                   |

### 📌 Conta

| Campo       | Tipo           | Regras de negócio                                                                 |
|-------------|----------------|-----------------------------------------------------------------------------------|
| id          | Long           | Gerado automaticamente                                                            |
| referencia  | String         | Obrigatório. Formato: `MM-AAAA`                                                   |
| valor       | BigDecimal     | Obrigatório. **Não pode ser menor que 0**                                        |
| situacao    | Enum (String)  | Obrigatório: `PENDENTE`, `PAGA`, `CANCELADA`                                     |

Relacionamento: Uma conta está associada a **um cliente**.

### 📌 Regras de Negócio para Conta

- ❌ **Não pode criar uma conta com valor menor que 0**
- ❌ **Não pode criar uma conta sem cliente associado**
- ❌ **Não pode criar uma conta já com a situação `CANCELADA`**

Estas regras devem ser implementadas e validadas no código.

---

## 📋 Funcionalidades obrigatórias (Endpoints)

### Clientes

- [POST] `/clientes`  
  👉 Cadastrar um novo cliente

- [PUT] `/clientes/{id}`  
  ✏️ Atualizar os dados de um cliente

- [DELETE] `/clientes/{id}`  
  🗑️ Excluir cliente (remoção permanente)

- [GET] `/clientes`  
  📃 Listar todos os clientes

### Contas

- [POST] `/clientes/{idCliente}/contas`  
  👉 Criar uma conta para um cliente

- [PUT] `/contas/{id}`  
  ✏️ Atualizar os dados de uma conta

- [DELETE] `/contas/{id}`  
  🚫 Excluir logicamente a conta (altera `situacao` para `CANCELADA`)

- [GET] `/clientes/{idCliente}/contas`  
  📃 Listar todas as contas de um cliente

---

## 🔍 Exemplo de Requisições

### Criar Cliente

```http
POST /clientes
Content-Type: application/json

{
  "nome": "João Silva",
  "cpf": "12345678900",
  "telefone": "11999998888",
  "email": "joao@email.com"
}
```

### Criar Conta

```http
POST /clientes/1/contas
Content-Type: application/json

{
  "referencia": "06-2025",
  "valor": 250.00,
  "situacao": "PENDENTE"
}
```

---

## ✅ Critérios de Avaliação

- Funcionamento dos endpoints conforme especificado
- Implementação das regras de negócio (conta não pode ser criada inválida)
- Uso correto do Spring Web e Spring Data JPA
- Modelagem adequada das entidades e relacionamento entre elas
- Organização do projeto (pacotes, nomes de classes)
- Boas práticas de código (claridade, legibilidade)
- README bem estruturado (esse mesmo 😉)
- Testes (mínimo: unitário ou de integração simples)

**❗ O uso de validação Bean Validation (como @NotNull, @Email) é opcional e não obrigatório.**

---

## 🛠️ Configuração do Projeto

1. Clone este repositório:
```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
```

2. Configure o banco de dados PostgreSQL com as credenciais abaixo ou altere no `application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/desafio
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

3. Execute o projeto com:
```bash
./mvnw spring-boot:run
```

---

## 🚨 Observações

- Não é necessário criar autenticação/autorização
- O projeto deve ser entregue com todos os endpoints funcionando
- Testes unitários e/ou de integração serão considerados um diferencial
- O código será analisado! Comentários e organização contam!

---

## 📦 Extras (opcional, mas bem-vindo)

- Documentação com Swagger/OpenAPI
- Utilização de DTOs para entrada e saída de dados
- Tratamento de exceções com `@RestControllerAdvice`
- Logs e mensagens de erro claras

---

## 📅 Prazo

O prazo de entrega será informado pelo avaliador. Certifique-se de enviar o projeto completo no repositório GitHub ou similar, com instruções claras para execução.

Boa sorte! 💻🚀
