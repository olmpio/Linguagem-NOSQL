# 🚀 API RESTful - CRUD com Spring Boot e MongoDB

Projeto desenvolvido como parte de uma atividade prática de programação, implementando um CRUD completo (Create, Read, Update, Delete) utilizando **Java**, **Spring Boot** e **Spring Data MongoDB**.

---

## 🛠️ Tecnologias Utilizadas

* **Java 25+**
* **Spring Boot**
* **Maven**
* **MongoDB** (Banco de dados NoSQL)

---

## 📂 Estrutura do Projeto

O projeto segue o padrão arquitetural em camadas:
* **`models`**: Classes que representam as entidades do banco de dados (`Estudante`, `Curso`, `Professor`).
* **`repositories`**: Interfaces que estendem `MongoRepository` para realizar a comunicação direta com o MongoDB.
* **`controllers`**: Classes anotadas com `@RestController` que expõem os endpoints da API.
