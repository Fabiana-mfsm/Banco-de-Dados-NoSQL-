# - Atividade Prática - Consultas MongoDB

## Banco de dados utilizado

```javascript
use store
```

O banco de dados utilizado na atividade é o `store`.

### Collection utilizada

```javascript
db.customers
```

A collection `customers` armazena os documentos dos clientes.

---

# Estado atual da collection

Antes de realizar as consultas, a collection `customers` apresenta os seguintes documentos:

```javascript
db.customers.find()
```

### Resultado

```javascript
[
  {
    _id: ObjectId('6a976c3e14588ee5cb6975ae'),
    name: 'Ana',
    age: 25,
    city: 'Salvador',
    active: true,
    points: 170,
    state: 'BA'
  },
  {
    _id: ObjectId('6a976c3e14588ee5cb6975af'),
    name: 'Bruno',
    age: 32,
    city: 'Feira de Santana',
    active: true
  },
  {
    _id: ObjectId('6a976c3e14588ee5cb6975b0'),
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: true,
    points: 80,
    state: 'BA'
  },
  {
    _id: ObjectId('6a976c3e14588ee5cb6975b1'),
    name: 'Daniela',
    age: 40,
    city: 'São Paulo',
    active: true,
    points: 500,
    vip: true
  },
  {
    _id: ObjectId('6a97761c14588ee5cb6975b3'),
    name: 'Fernando',
    age: 29,
    city: 'Recife',
    active: true,
    points: 90
  }
]
```

---

# Consultas

## 1. Mostrar apenas os nomes dos clientes

### Comando

```javascript
db.customers.find(
    {},
    { _id: 0, name: 1 }
)
```

O comando `find()` realiza uma consulta na collection.

* `{}` → indica que todos os documentos serão pesquisados.
* `name: 1` → mostra apenas o campo `name`.
* `_id: 0` → oculta o identificador `_id`.

### Resultado

```text
[
  { name: 'Ana' },
  { name: 'Bruno' },
  { name: 'Carlos' },
  { name: 'Daniela' },
  { name: 'Fernando' }
]
```

---

## 2. Contar quantos clientes existem

### Comando

```javascript
db.customers.countDocuments()
```

O comando `countDocuments()` conta a quantidade de documentos existentes na collection.

### Resultado

```text
5
```

Existem **5 clientes** cadastrados.

---

## 3. Contar apenas os clientes ativos

### Comando

```javascript
db.customers.countDocuments(
    { active: true }
)
```

O comando conta somente os clientes que possuem `active` como `true`.

### Resultado

```text
5
```

Existem **5 clientes ativos**.

---

## 4. Mostrar o cliente com maior pontuação

### Comando

```javascript
db.customers.find().sort({ points: -1 }).limit(1)
```

O comando utiliza `sort()` para ordenar os clientes pela pontuação.

* `points: -1` → ordena da maior para a menor pontuação.
* `limit(1)` → mostra somente o primeiro resultado.

### Resultado

```text
{
  name: 'Daniela',
  age: 40,
  city: 'São Paulo',
  active: true,
  points: 500,
  vip: true
}
```

A cliente com maior pontuação é **Daniela**, com **500 pontos**.

---

## 5. Mostrar o cliente com menor idade

### Comando

```javascript
db.customers.find().sort({ age: 1 }).limit(1)
```

O comando ordena os clientes pela idade.

* `age: 1` → ordem crescente, do menor para o maior.
* `limit(1)` → mostra somente o primeiro documento.

### Resultado

```text
{
  name: 'Ana',
  age: 25,
  city: 'Salvador',
  active: true,
  points: 170,
  state: 'BA'
}
```

A cliente com menor idade é **Ana**, com **25 anos**.

---

## 6. Mostrar apenas clientes com pontuação entre 100 e 400

### Comando

```javascript
db.customers.find({
    points: { $gte: 100, $lte: 400 }
})
```

O comando utiliza operadores de comparação para definir um intervalo de pontuação.

* `$gte: 100` → maior ou igual a 100.
* `$lte: 400` → menor ou igual a 400.

### Resultado

```text
[
  {
    name: 'Ana',
    age: 25,
    city: 'Salvador',
    active: true,
    points: 170,
    state: 'BA'
  }
]
```

Apenas **Ana** possui pontuação entre 100 e 400.

---

## 7. Mostrar apenas clientes das cidades de Salvador ou São Paulo

### Comando

```javascript
db.customers.find({
    city: { $in: ["Salvador", "São Paulo"] }
})
```

O operador `$in` permite pesquisar documentos cujo valor de um campo esteja dentro de uma lista de valores.

Neste caso, são pesquisadas as cidades **Salvador** e **São Paulo**.

### Resultado

```text
[
  {
    name: 'Ana',
    age: 25,
    city: 'Salvador',
    active: true,
    points: 170,
    state: 'BA'
  },
  {
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: true,
    points: 80,
    state: 'BA'
  },
  {
    name: 'Daniela',
    age: 40,
    city: 'São Paulo',
    active: true,
    points: 500,
    vip: true
  }
]
```

---

## 8. Mostrar todos os clientes ordenados por nome

### Comando

```javascript
db.customers.find().sort({ name: 1 })
```

O comando `sort()` organiza os documentos pelo campo `name`.

* `name: 1` → ordem crescente, de A até Z.

### Resultado

```text
[
  { name: 'Ana' },
  { name: 'Bruno' },
  { name: 'Carlos' },
  { name: 'Daniela' },
  { name: 'Fernando' }
]
```

Os clientes são apresentados em ordem alfabética.

---

## 9. Mostrar apenas os três primeiros clientes

### Comando

```javascript
db.customers.find().limit(3)
```

O comando `limit(3)` limita a consulta aos três primeiros documentos encontrados.

### Resultado

```text
[
  {
    name: 'Ana',
    age: 25,
    city: 'Salvador',
    active: true,
    points: 170,
    state: 'BA'
  },
  {
    name: 'Bruno',
    age: 32,
    city: 'Feira de Santana',
    active: true
  },
  {
    name: 'Carlos',
    age: 28,
    city: 'Salvador',
    active: true,
    points: 80,
    state: 'BA'
  }
]
```

---

## 10. Mostrar apenas os clientes inativos

### Comando

```javascript
db.customers.find({
    active: false
})
```

O comando procura os documentos que possuem o campo `active` com valor `false`.

### Resultado

```text
[]
```

Não existem clientes inativos na collection.

---

# Comandos utilizados

| Comando/Operador   | Função                               |
| ------------------ | ------------------------------------ |
| `find()`           | Realiza consultas na collection      |
| `countDocuments()` | Conta documentos                     |
| `sort()`           | Ordena os resultados                 |
| `limit()`          | Limita a quantidade de resultados    |
| `$gte`             | Maior ou igual a                     |
| `$lte`             | Menor ou igual a                     |
| `$in`              | Pesquisa valores dentro de uma lista |

---


