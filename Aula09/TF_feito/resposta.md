# Resposta - Exercícios de MongoDB CRUD

## Exercício 1: Criação e Coleções (O "C" do CRUD)

### 1. Criar banco de dados e coleção

```javascript
// Criar/acessar o banco de dados
use loja_virtual

// Criar a coleção (será criada quando inserir dados)
db.createCollection("produtos")
```

### 2. Inserir o primeiro produto (Smartphone)

```javascript
db.produtos.insertOne({
  nome: "Smartphone Galaxy A15",
  categoria: "Eletronicos",
  preco: 1299.90,
  marca: "Samsung",
  armazenamento: "128GB",
  cor: "Azul"
})
```

### 3. Inserir dois outros produtos de categorias diferentes

```javascript
db.produtos.insertMany([
  {
    nome: "MongoDB na Pratica",
    categoria: "Livros",
    preco: 79.90,
    autor: "Joao Silva",
    editora: "Tech Books",
    paginas: 320
  },
  {
    nome: "Camiseta Basica",
    categoria: "Roupas",
    preco: 49.90,
    tamanho: "M",
    cor: "Preta",
    material: "Algodao"
  }
])
```

---

## Exercício 2: Consultas e Filtros (O "R" do CRUD)

### 1. Listar todos os produtos da coleção

```javascript
db.produtos.find()
// Ou com formatação melhor:
db.produtos.find().pretty()
```

**Resultado esperado:**
```javascript
[
  { _id: ObjectId(...), nome: "Smartphone Galaxy A15", categoria: "Eletronicos", preco: 1299.90, ... },
  { _id: ObjectId(...), nome: "MongoDB na Pratica", categoria: "Livros", preco: 79.90, ... },
  { _id: ObjectId(...), nome: "Camiseta Basica", categoria: "Roupas", preco: 49.90, ... }
]
```

### 2. Buscar apenas produtos com preço superior a 100

```javascript
db.produtos.find({ preco: { $gt: 100 } })
```

**Resultado esperado:**
```javascript
[
  { _id: ObjectId(...), nome: "Smartphone Galaxy A15", categoria: "Eletronicos", preco: 1299.90, ... }
]
```

### 3. Listar apenas produtos da categoria "Eletronicos"

```javascript
db.produtos.find({ categoria: "Eletronicos" })
```

**Resultado esperado:**
```javascript
[
  { _id: ObjectId(...), nome: "Smartphone Galaxy A15", categoria: "Eletronicos", preco: 1299.90, ... }
]
```

### 4. Buscar retornando apenas nome e preço

```javascript
db.produtos.find({}, { nome: 1, preco: 1, _id: 0 })
```

**Resultado esperado:**
```javascript
[
  { nome: "Smartphone Galaxy A15", preco: 1299.90 },
  { nome: "MongoDB na Pratica", preco: 79.90 },
  { nome: "Camiseta Basica", preco: 49.90 }
]
```

---

## Exercício 3: Atualização Dinâmica (O "U" do CRUD)

### 1. Atualizar o preço de um produto específico

```javascript
db.produtos.updateOne(
  { nome: "Smartphone Galaxy A15" },
  { $set: { preco: 999.90 } }
)
```

**Resultado:** O smartphone terá o preço atualizado para 999.90

### 2. Adicionar campo "estoque" em todos os produtos

```javascript
db.produtos.updateMany(
  {},
  { $set: { estoque: 50 } }
)
```

**Resultado:** Todos os produtos agora têm o campo `estoque: 50`

### 3. Marcar produtos da categoria "Roupas" com promoção

```javascript
db.produtos.updateMany(
  { categoria: "Roupas" },
  { $set: { promocao: true } }
)
```

**Resultado:** Produtos de roupas têm `promocao: true` adicionado

---

## Exercício 4: Exclusão de Dados (O "D" do CRUD)

### 1. Remover um produto específico

```javascript
db.produtos.deleteOne({ nome: "MongoDB na Pratica" })
```

**Resultado:** O livro é removido da coleção

### 2. Remover todos os produtos de uma categoria

```javascript
db.produtos.deleteMany({ categoria: "Roupas" })
```

**Resultado:** Todos os produtos da categoria "Roupas" são removidos

---

## Resumo de Comandos Utilizados

| Operação | Comando |
|----------|---------|
| Criar banco | `use loja_virtual` |
| Criar coleção | `db.createCollection("produtos")` |
| Inserir um | `db.produtos.insertOne({...})` |
| Inserir vários | `db.produtos.insertMany([...])` |
| Listar todos | `db.produtos.find()` |
| Filtrar | `db.produtos.find({ campo: valor })` |
| Atualizar um | `db.produtos.updateOne({ filter }, { $set: {...} })` |
| Atualizar vários | `db.produtos.updateMany({ filter }, { $set: {...} })` |
| Deletar um | `db.produtos.deleteOne({ filter })` |
| Deletar vários | `db.produtos.deleteMany({ filter })` |

---

## Dicas Importantes

1. **Operadores de comparação MongoDB:**
   - `$gt`: Maior que (>)
   - `$lt`: Menor que (<)
   - `$eq`: Igual (=)
   - `$ne`: Não igual (!=)

2. **Projeção em find():**
   - `{ campo: 1 }` = incluir
   - `{ campo: 0 }` = excluir

3. **Operadores de atualização:**
   - `$set`: Define um valor
   - `$inc`: Incrementa
   - `$push`: Adiciona a um array

---

**Data de conclusão:** 29 de abril de 2026
