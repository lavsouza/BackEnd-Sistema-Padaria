# Sistema Padaria - Backend

API REST em Spring Boot para gerenciar fornadas de uma padaria. O sistema controla os tipos de pao cadastrados, cria fornadas, associa paes a cada fornada, calcula horarios de entrada e saida e expoe os dados para o frontend de cliente e padeiro.

## Funcionalidades

- Listagem de tipos de pao disponiveis.
- Criacao, consulta e exclusao de fornadas.
- Inclusao de paes em uma fornada com quantidade.
- Alteracao da quantidade de paes em producao.
- Remocao de paes de uma fornada.
- Consulta de fornadas do dia e detalhamento por fornada ou por pao.

## Tecnologias

- Java 17
- Spring Boot 3.5.5
- Spring Web
- Spring JDBC
- PostgreSQL
- Maven

## Estrutura

- `src/main/java/web2/sistemapadaria/controller`: controllers REST.
- `src/main/java/web2/sistemapadaria/service`: regras de negocio.
- `src/main/java/web2/sistemapadaria/model/entities`: entidades de dominio.
- `src/main/java/web2/sistemapadaria/model/repositories`: acesso a dados via JDBC.
- `src/main/java/web2/sistemapadaria/DTO`: objetos de entrada e saida da API.
- `src/main/resources/schema_padaria.sql`: script de criacao das tabelas e carga inicial de paes.

## Banco de dados

Crie um banco PostgreSQL chamado `padaria` e execute o script:

```bash
psql -U postgres -d padaria -f src/main/resources/schema_padaria.sql
```

Configure o acesso ao banco em `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/padaria
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.datasource.driver-class-name=org.postgresql.Driver
```

## Como executar

No diretorio do projeto:

```bash
./mvnw spring-boot:run
```

No Windows:

```bash
mvnw.cmd spring-boot:run
```

A API fica disponivel em:

```text
http://localhost:8080
```

## Endpoints principais

### Paes

| Metodo | Rota | Descricao |
| --- | --- | --- |
| `GET` | `/pao/listar` | Lista todos os tipos de pao |
| `DELETE` | `/pao/excluir-pao-fornada/{pao}/{fornada}` | Remove um pao de uma fornada |

### Fornadas

| Metodo | Rota | Descricao |
| --- | --- | --- |
| `POST` | `/fornada/criar` | Cria uma nova fornada |
| `POST` | `/fornada/adicionar-pao` | Adiciona pao a uma fornada |
| `PUT` | `/fornada/alterar-quantidade` | Altera a quantidade de pao em uma fornada |
| `GET` | `/fornada/listar-fornadas` | Lista todas as fornadas |
| `GET` | `/fornada/listar-fornadas-dia` | Lista fornadas ativas do dia |
| `GET` | `/fornada/detalhar-fornada/{codFornada}` | Detalha uma fornada |
| `GET` | `/fornada/detalhar-fornada-pao/{codPao}` | Busca fornadas por tipo de pao |
| `DELETE` | `/fornada/excluir/{codigo}` | Exclui uma fornada |

## Exemplo de payload

```json
{
  "idPao": 1,
  "idFornada": 1,
  "quantidade": 20
}
```

## Projeto relacionado

Este backend foi criado para ser consumido pelo frontend:

```text
https://github.com/lavsouza/FrontEnd-Sistema-Padaria
```
