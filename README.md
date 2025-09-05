# AutoEscola API (Checkpoint 1 - SOA e WebServices)

API ReST com Spring Boot para **cadastro de instrutores e alunos** e **agendamento/cancelamento de instruções**.

## ⚙️ Stack
- Java 17
- Spring Boot 3 (Web, Validation, Data JPA)
- H2 Database (runtime)
- Flyway (migrações)
- Maven

## 🚀 Como rodar
```bash
# 1) Build
mvn clean package

# 2) Executar
mvn spring-boot:run
# ou
java -jar target/autoescola-api-1.0.0.jar
```

H2 Console: `http://localhost:8080/h2-console` (JDBC URL: `jdbc:h2:mem:autoescola`, user: `sa`, senha: `password`).

## 📚 Endpoints principais

### Instrutores
- **POST** `/api/instrutores` — cria instrutor (telefone opcional na criação)
- **GET** `/api/instrutores?page=0&size=10` — lista paginada (nome asc, 10 por página; retorna nome, e-mail, CNH e especialidade)
- **PUT** `/api/instrutores/{id}` — atualiza **apenas** nome, telefone e endereço
- **DELETE** `/api/instrutores/{id}` — exclusão lógica (ativo=false)

### Alunos
- **POST** `/api/alunos`
- **GET** `/api/alunos?page=0&size=10`
- **PUT** `/api/alunos/{id}` — atualiza **apenas** nome, telefone e endereço
- **DELETE** `/api/alunos/{id}` — exclusão lógica (ativo=false)

### Instruções
- **POST** `/api/instrucoes` — agendar (1h de duração, 06:00–21:00, seg–sáb, 30 min antecedência, máx. 2 por dia por aluno, instrutor único por horário; se não informar instrutor, seleciona aleatoriamente um disponível)
- **POST** `/api/instrucoes/{id}/cancelar?motivo=ALUNO_DESISTIU|INSTRUTOR_CANCELOU|OUTROS` — cancela com **mínimo 24h** de antecedência

> As regras seguem o enunciado do checkpoint: campos obrigatórios, paginação/ordenação, exclusão lógica, restrições de atualização e validações de negócio do agendamento/cancelamento.

## 🧱 Estrutura
```
src/main/java/com/fiap/autoescola
  ├─ controller
  ├─ dto
  ├─ domain
  │   ├─ entity
  │   ├─ enums
  │   └─ vo
  ├─ mapper
  ├─ repository
  └─ service
```

## 👥 Integrantes
- João Pedro Marques Rodrigues RM98307
- Vitor Shimizu RM550390

## 📄 Licença
MIT
