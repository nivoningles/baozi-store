# Baozi Store - API REST

Trabalho da disciplina de Desenvolvimento Web Back-End (UNINTER, 2026).

API para cadastrar clientes, produtos e pedidos da Baozi Store, uma lojinha de pão chinês.
Feita com Java 21, Spring Boot, Spring Data JPA e banco H2.

## Rodando o projeto

Precisa do JDK 21 (a variável JAVA_HOME tem que apontar para ele).

```
.\mvnw spring-boot:run
```

No Linux/Mac: `./mvnw spring-boot:run`

A API fica em http://localhost:8080

O banco H2 é salvo na pasta `data/`. Dá para ver as tabelas em http://localhost:8080/h2-console
(JDBC URL: `jdbc:h2:file:./data/baozistore`, usuário `sa`, senha em branco).

Também deixei uma configuração para MySQL em `application-mysql.properties`
(rodar com `.\mvnw spring-boot:run -Dspring-boot.run.profiles=mysql`).

## Pacotes

- `model` - entidades Cliente, Produto e Pedido
- `repository` - interfaces JpaRepository
- `controller` - controllers REST

## Entidades

- **Cliente**: id, nome, clienteDesde
- **Produto**: id, nome, preco, estoque
- **Pedido**: id, cliente (cliente_id), produto (produto_id), quantidade

## Endpoints

Os três recursos (`/clientes`, `/produtos`, `/pedidos`) têm os mesmos endpoints:

- `POST /recurso` - cadastra
- `GET /recurso` - lista todos
- `GET /recurso/{id}` - busca por id
- `PUT /recurso/{id}` - atualiza
- `DELETE /recurso/{id}` - apaga

Exemplos de JSON:

```
POST /clientes  {"nome": "Nivon5596645", "clienteDesde": "2026-11-25"}
POST /produtos  {"nome": "Baozi de carne", "preco": 6.50, "estoque": true}
POST /pedidos   {"clienteId": 1, "produtoId": 1, "quantidade": 12}
```

Não é possível apagar um cliente ou produto que tenha pedido (retorna 409).

O arquivo `BaoziStore.postman_collection.json` tem as requisições para importar no Postman.
