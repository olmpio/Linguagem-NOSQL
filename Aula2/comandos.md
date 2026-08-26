# MongoDB - Comandos Básicos

Este documento reúne os comandos essenciais para começar a trabalhar com o MongoDB: bancos de dados, collections e operações de CRUD (Create, Read, Update, Delete).

## Bancos de Dados

**Exibir os bancos de dados existentes**

```js
show databases
```

**Selecionar (ou criar) um banco de dados**

Se o banco de dados informado ainda não existir, o MongoDB o cria automaticamente assim que o primeiro dado for inserido.

```js
use loja_informatica
```

## Collections

**Criar uma nova collection**

```js
db.createCollection("cliente")
```

**Mostrar todas as collections do banco atual**

```js
show collections
```

## Consultando Documentos (Read)

**Mostrar todos os documentos de uma collection**

```js
db.cliente.find()
```

**Buscar por um campo específico**

```js
db.cliente.find({"nome": "José"})
```

**Buscar pelo identificador único (`_id`)**

```js
db.cliente.find({_id: ObjectId('6a7bbab007ff2cf8649f68a9')})
```

## Inserindo Documentos (Create)

**Inserir apenas um documento**

```js
db.cliente.insertOne({
  "nome": "jefté",
  "idade": 35,
  "pets": ["dora", "sabrina"],
  "endereco": {
    "logradouro": "Sossego"
  }
})
```

**Inserir vários documentos de uma vez**

```js
db.cliente.insertMany([
  { "nome": "Brenno" },
  { "nome": "João" },
  { "nome": "Maria" },
  { "nome": "José" },
  { "nome": "Noé" }
])
```

## Resumo dos Comandos

| Comando | Ação |
|---------|------|
| `show databases` | Lista os bancos de dados disponíveis |
| `use <nome>` | Seleciona ou cria um banco de dados |
| `db.createCollection("<nome>")` | Cria uma nova collection |
| `show collections` | Lista as collections do banco atual |
| `db.<collection>.find()` | Retorna todos os documentos da collection |
| `db.<collection>.find({campo: valor})` | Busca documentos por um campo específico |
| `db.<collection>.insertOne({...})` | Insere um único documento |
| `db.<collection>.insertMany([...])` | Insere múltiplos documentos de uma vez |
