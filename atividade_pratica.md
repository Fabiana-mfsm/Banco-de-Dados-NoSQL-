# - Atividade Prática - MongoDB: Antes e Depois

## Banco de dados utilizado

```javascript
use store
```

Esse comando seleciona o banco de dados `store` para realizar as operações da atividade.

### Collection utilizada

```javascript
db.customers
```

A collection `customers` será utilizada para armazenar os documentos dos clientes.

---

## 1. Consultar clientes de Salvador

```javascript
db.customers.find(
    { city: "Salvador" },
    { _id: 0, name: 1, city: 1 }
)
```

Esse comando realiza uma busca pelos clientes que moram em **Salvador**.

* `{ city: "Salvador" }` → filtra os clientes pela cidade.
* `name: 1` → exibe o nome do cliente.
* `city: 1` → exibe a cidade.
* `_id: 0` → oculta o identificador do documento.

---

## 2. Ativar o cliente Carlos

```javascript
db.customers.updateOne(
    { name: "Carlos" },
    { $set: { active: true } }
)
```

O comando `updateOne()` é utilizado para atualizar um único documento.

* `{ name: "Carlos" }` → localiza o cliente Carlos.
* `$set` → altera o valor de um campo.
* `active: true` → define Carlos como cliente ativo.

---

## 3. Adicionar o estado BA aos clientes de Salvador

```javascript
db.customers.updateMany(
    { city: "Salvador" },
    { $set: { state: "BA" } }
)
```

O comando `updateMany()` permite atualizar vários documentos de uma única vez.

* `{ city: "Salvador" }` → seleciona os clientes de Salvador.
* `$set` → adiciona ou altera um campo.
* `state: "BA"` → adiciona o estado da Bahia aos documentos encontrados.

---

## 4. Aumentar os pontos da Ana

```javascript
db.customers.updateOne(
    { name: "Ana" },
    { $inc: { points: 50 } }
)
```

O operador `$inc` é utilizado para aumentar ou diminuir valores numéricos.

Neste caso, são adicionados **50 pontos** aos pontos atuais da Ana.

* `name: "Ana"` → localiza a cliente Ana.
* `$inc` → incrementa o valor.
* `points: 50` → adiciona 50 pontos ao campo `points`.

---

## 5. Inserir o cliente Fernando

```javascript
db.customers.insertOne({
    name: "Fernando",
    age: 29,
    city: "Recife",
    active: true,
    points: 90
})
```

O comando `insertOne()` é utilizado para inserir um único documento na collection.

O documento cadastra o cliente **Fernando**, com idade de 29 anos, residente em Recife, ativo e com 90 pontos.

---

## 6. Excluir a cliente Eduarda

```javascript
db.customers.deleteOne(
    { name: "Eduarda" }
)
```

O comando `deleteOne()` é utilizado para excluir um documento da collection.

* `{ name: "Eduarda" }` → localiza a cliente Eduarda.
* `deleteOne()` → remove o documento encontrado.

Nesse caso, o documento completo da Eduarda será excluído.

---

## 7. Tornar Daniela uma cliente VIP

```javascript
db.customers.updateOne(
    { name: "Daniela", age: 40 },
    { $set: { vip: true } }
)
```

Esse comando adiciona o campo `vip` ao documento da Daniela.

* `{ name: "Daniela", age: 40 }` → localiza a Daniela.
* `$set` → adiciona ou altera um campo.
* `vip: true` → define a cliente como VIP.

---

## 8. Remover os pontos do Bruno

```javascript
db.customers.updateOne(
    { name: "Bruno" },
    { $unset: { points: "" } }
)
```

O operador `$unset` é utilizado para remover um campo de um documento.

Nesse caso, somente o campo `points` será removido.

O documento do Bruno continuará existindo normalmente na collection.

---

## 9. Ordenar clientes pela idade

```javascript
db.customers.find().sort({ age: -1 })
```

Esse comando exibe todos os clientes ordenados pela idade.

* `sort()` → realiza a ordenação dos documentos.
* `age` → campo utilizado para a ordenação.
* `-1` → ordem decrescente.

Portanto, os clientes serão exibidos do **mais velho para o mais novo**.

---

## 10. Consultar clientes ativos com mais de 30 anos

```javascript
db.customers.find(
    {
        active: true,
        age: { $gt: 30 }
    },
    {
        name: 1,
        _id: 0
    }
)
```

Esse comando realiza uma busca utilizando dois critérios.

* `active: true` → seleciona somente clientes ativos.
* `$gt: 30` → seleciona clientes com idade maior que 30 anos.
* `name: 1` → exibe somente o nome.
* `_id: 0` → oculta o identificador.

### Resultado esperado

```text
Bruno
Daniela
```

---

# Comandos e Operadores utilizados

| Comando/Operador | Função                                      |
| ---------------- | ------------------------------------------- |
| `use`            | Seleciona um banco de dados                 |
| `find()`         | Consulta documentos                         |
| `insertOne()`    | Insere um documento                         |
| `updateOne()`    | Atualiza um documento                       |
| `updateMany()`   | Atualiza vários documentos                  |
| `deleteOne()`    | Exclui um documento                         |
| `$set`           | Adiciona ou altera um campo                 |
| `$inc`           | Incrementa ou diminui um valor              |
| `$unset`         | Remove um campo                             |
| `$gt`            | Busca valores maiores que determinado valor |
| `sort()`         | Ordena os documentos                        |

---

