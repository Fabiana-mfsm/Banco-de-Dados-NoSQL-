# - Introdução - NoSQL / Mongo DB

## Definição

### O que é NoSQL?

* NoSQL é um paradigma de banco de dados que engloba diversos tipos de bancos de dados não relacionais.

Projetados para oferecer:

* Flexibilidade
* Escalabilidade
* Alto desempenho

## Definição

### Os quatro principais paradigmas de bancos de dados NoSQL são:

* Bancos de dados orientados a documentos (ex.: MongoDB)
* Bancos de dados chave-valor (ex.: Redis)
* Bancos de dados de famílias de colunas (wide-column) (ex.: Cassandra)
* Bancos de dados orientados a grafos (ex.: Neo4j)

## O que é MongoDB?

### O que significa "Mongo"?

* **Humongous (Gigante)** — o MongoDB foi projetado para armazenar e gerenciar grandes volumes de dados de forma eficiente.

* MongoDB é um banco de dados NoSQL de código aberto, orientado a documentos, projetado para armazenar e gerenciar grandes quantidades de dados de maneira eficiente.

* Diferentemente dos bancos de dados relacionais tradicionais (como MySQL ou PostgreSQL), o MongoDB armazena os dados em documentos, em vez de linhas em tabelas.

## Como o MongoDB funciona?

* Um servidor MongoDB pode hospedar múltiplos bancos de dados.
* Cada banco de dados contém coleções (collections), e cada coleção armazena documentos (documents).

## JSON (BSON) Data Format

* Todo registro no MongoDB é, na verdade, um documento.
* Os documentos são armazenados no MongoDB em um formato semelhante ao JSON, chamado BSON (Binary JSON).
* Os documentos BSON são objetos que contêm uma lista ordenada dos elementos que armazenam.
* Cada elemento é composto por um nome de campo (field name) e um valor de um determinado tipo.

## Formato JSON / BSON (Binary JSON)

```json
{
  "name": "Jefté",
  "age": 33,
  "address": {
    "city": "Brazil"
  },
  "hobbies": [
    {
      "name": "Lego"
    },
    {
      "name": "Games"
    }
  ]
}
```

### Diagrama (No Schema / Users Collection)

**No Schema!**

| ID | Campos | Campos | Campos |
| :--- | :--- | :--- | :--- |
| **id: 1** | `"name": "Jefté"` | `"age": 35` | `...` |
| **id: 1** | `"name": "Brenno"` | | |
| **id: 1** | | `"age": 10` | `...` |

**Users Collection**


## Relacionamentos

* Diferentemente dos bancos de dados relacionais, o MongoDB minimiza o uso de relacionamentos entre coleções.

* Em vez de dividir os dados relacionados em várias tabelas e depois uni-los por meio de JOINs, o MongoDB geralmente armazena esses dados juntos no mesmo documento utilizando documentos incorporados (embedded documents).

## Comandos Principais

```text
mongosh
show databases / show dbs
use shop
show collections
db.<collection_name>.insertOne({<object>})
db.createCollection("<collection_name>")
db.<collection_name>.find()
```




## - Introdução - CRUD

### JSON

* `"name": "jefté"` é chamado de campo (field) ou propriedade (property) do documento JSON.
* Múltiplos campos são separados por vírgulas.
* Os campos (fields) são compostos por uma chave (key), também chamada de nome (name), e um valor (value).
* A chave e o valor são separados por dois-pontos (`:`).
* Os valores (values) podem ser:

  * strings (por exemplo, `"Jefté"`)
  * números (por exemplo, `35`)
  * booleanos (por exemplo, `true`)
  * arrays (`[...]`)
  * outros documentos, também chamados de objetos (`{...}`)

### CRUD
#### Create
- `insertOne(data, options)`
- `insertMany(data, options)`

#### Update
- `updateOne(filter, data, options)`
- `updateMany(filter, data, options)`
- `replaceOne(filter, data, options)`

#### Read
- `find(filter, options)`
- `findOne(filter, options)`

#### Delete
- `deleteOne(filter, options)`
- `deleteMany(filter, options)`

***
***
## Comandos e Operações do MongoDB
### Exibir os bancos de dados

```javascript
show databases
```
Esse comando exibe todos os bancos de dados existentes no MongoDB.

### Selecionar um banco de dados

```javascript
use loja_informatica
```
Esse comando seleciona o banco de dados `loja_informatica` para que as próximas operações sejam realizadas nele.

### Criar uma collection

```javascript
db.createCollection("cliente")
```
Cria uma nova collection chamada `cliente`.

As collections são utilizadas para armazenar documentos no MongoDB, funcionando de forma semelhante às tabelas dos bancos de dados relacionais.

### Exibir todas as collections

```javascript
show collections
```
Exibe todas as collections existentes no banco de dados selecionado.

### Exibir todos os documentos
```javascript
db.cliente.find()
```
Retorna todos os documentos armazenados na collection `cliente`.

### Inserir um documento

```javascript
db.cliente.insertOne({
    "nome": "Jefté",
    "idade": 35,
    "pets": ["Dora", "Sabrina"],
    "endereco": {
        "logradouro": "Sossego"
    }
})
```
O comando `insertOne()` é utilizado para inserir apenas um documento na collection.

### Inserir vários documentos

```javascript
db.cliente.insertMany([
    { "nome": "Brenno" },
    { "nome": "João" },
    { "nome": "Maria" },
    { "nome": "José" },
    { "nome": "Noé" }
])
```
O comando `insertMany()` permite inserir vários documentos de uma única vez.

### Buscar documentos por um campo

```javascript
db.cliente.find({ "nome": "José" })
```
Esse comando realiza uma busca na collection `cliente`, retornando os documentos que possuem o campo `nome` com o valor `"José"`.

### Buscar um documento pelo identificador

```javascript
db.cliente.find({
    "_id": ObjectId("6a7bbab007ff2cf8649f68a9")
})
```
O campo `_id` é utilizado pelo MongoDB como identificador único de cada documento. Esse comando permite localizar um documento específico através desse identificador.

