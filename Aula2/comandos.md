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


## Atividade - MongoDB: Antes e Depois



**Exercício 1 – Consulta**  

```js
store> db.costumers.find({ city: 'Salvador' })
[
  {
    _id: ObjectId('6a98577f99861978fa655eeb'),
    name: 'Ana',
    age: 25,
    city: 'Salvador',
    active: true,
    points: 120
  },
  {
    _id: ObjectId('6a98577f99861978fa655eed'),
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: false,
    points: 80
  }
] 
```
**Exercício 2 – Atualização**  
```js
store> db.costumers.updateOne({name:'Carlos'},{$set:{active:'true'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
store> db.costumers.find({name:'Carlos'})
[
  {
    _id: ObjectId('6a98577f99861978fa655eed'),
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: 'true',
    points: 80
  }
]
```
**Exercício 3 – Atualizar vários documentos**
```js
store> db.costumers.updateMany({city:'Salvador'},{$set: {state:'BA'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}

store> db.costumers.find({city:'Salvador'})
[
  {
    _id: ObjectId('6a98577f99861978fa655eeb'),
    name: 'Ana',
    age: 25,
    city: 'Salvador',
    active: true,
    points: 120,
    state: 'BA'
  },
  {
    _id: ObjectId('6a98577f99861978fa655eed'),
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: true,
    points: 80,
    state: 'BA'
  }
]
```
**Exercício 4 – Incremento**

```js
store> db.costumers.updateOne({name:'Ana'}, {$inc: {points:170}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
**Exercício 5 – Inserção**
```js
store> db.costumers.insertOne({
|   "name": "Fernando",
|   "age": 29,
|   "city": "Recife",
|   "active": true,
|   "points": 90
| })
{
  acknowledged: true,
  insertedId: ObjectId('6a987f8899861978fa655ef0')
}
```
**Exercício 6 – Remoção**
```js
store> db.costumers.deleteOne({name:'Eduarda'})
{ acknowledged: true, deletedCount: 1 }
```
**Exercício 7 –  Criar um novo campo**
```js
store> db.costumers.updateOne ({_id:ObjectId('6a98577f99861978fa655eed')},{$set:{vip:true}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

store> db.costumers.find({_id:ObjectId('6a98577f99861978fa655eed')})
[
  {
    _id: ObjectId('6a98577f99861978fa655eed'),
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: true,
    points: 80,
    state: 'BA',
    vip: true
  }
]
```
**Exercício 8 –  Remover um campo**

```js
store> db.costumers.updateMany({}, { $unset: { points: "" } })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 7,
  modifiedCount: 5,
  upsertedCount: 0
}
```
Exercício 9 – Remover um campo

```js
store> db.costumers.find().sort({ age: 1 })
[
  { _id: ObjectId('6a9880c099861978fa655ef1'), name: 'Eduarda' },
  { _id: ObjectId('6a98810499861978fa655ef2'), name: 'Carlos' },
  {
    _id: ObjectId('6a98577f99861978fa655eeb'),
    name: 'Ana',
    age: 25,
    city: 'Salvador',
    active: true,
    state: 'BA'
  },
  {
    _id: ObjectId('6a98577f99861978fa655eed'),
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: true,
    state: 'BA',
    vip: true
  },
  {
    _id: ObjectId('6a987f8899861978fa655ef0'),
    name: 'Fernando',
    age: 29,
    city: 'Recife',
    active: true
  },
  {
    _id: ObjectId('6a98577f99861978fa655eec'),
    name: 'Bruno',
    age: 32,
    city: 'Feira de Santana',
    active: true
  },
  {
    _id: ObjectId('6a98577f99861978fa655eee'),
    name: 'Daniela',
    age: 40,
    city: 'São Paulo',
    active: true
  }
]
```

**Exercício 10 – Filtro com múltiplas condições**
```js
store> db.costumers.find({ active: true, age: { $gt: 30 } }, { name: 1, _id: 0 })
[ { name: 'Bruno' }, { name: 'Daniela' } ]
```



