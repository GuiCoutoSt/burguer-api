# my-burguer-api 🍔

Seja bem-vindo(a) à my-burguer-api. Essa API te o objetivo de simular um marketplace de lanches. 

# URL Base 🔗

`https://my-burguer-api.herokuapp.com/`

# Endpoints 🔚

Essa API possuí 4 endpoints: `register`, `login`, `products`,  `suggestions` e `cupoms`. É possível cadastrar usuários, login, e ver cupons de desconto. Apenas os administradores da api podem cadastrar produtos e cupons de desconto. Para ver os produtos e escrever e ver sugestões os usuários precisam estar logados.

# Rotas que não precisam de autenticação 🔓

## Listando Cupons de Desconto 💵

Para listar os cupons basta fazer uma requisição `GET` no endpoint `/cupoms`. Essa requisição retornará a lista de todos os cupons registrados no sistema. *Apenas os administradores podem adicionar novos cupons.*

`GET /cupoms - FORMATO DA RESPOSTA - STATUS 200`

```json
[
	{
	  "id": 1,
    "code": "KENZINHO",
		"dicount": 10.0
  }
]
```

## Listando Produtos 🍟

Para listar os produtos basta fazer uma requisição `GET` no endpoint `/products`. Essa requisição retornará a lista de todos os produtos registrados no sistema. *Apenas os administradores podem adicionar novos cupons.*

`GET /cupoms - FORMATO DA RESPOSTA - STATUS 200`

```json
[
    {
        "id": 1,
        "name": "Hamburguer",
        "category": "Sanduíches",
        "price": 14,
        "image": "https://i.imgur.com/TWcbQmo.png",
        "quantity": 1
    },
    {
        "id": 2,
        "name": "X-Burguer",
        "category": "Sanduíches",
        "price": 16,
        "image": "https://i.imgur.com/3VwE0ne.png",
        "quantity": 1
    },
    {
        "id": 3,
        "name": "Big Kenzie",
        "category": "Sanduíches",
        "price": 18,
        "image": "https://i.imgur.com/4dlr2mK.png",
        "quantity": 1
    },
    {
        "id": 4,
        "name": "Combo Kenzie",
        "category": "Combos",
        "price": 24,
        "image": "https://i.imgur.com/TGHgJSr.png",
        "quantity": 1
    },
    {
        "id": 5,
        "name": "Fanta Guaraná",
        "category": "Sanduíches",
        "price": 5,
        "image": "https://i.imgur.com/FQjpDYw.png",
        "quantity": 1
    },
    {
        "id": 6,
        "name": "Coca Cola",
        "category": "Sanduíches",
        "price": 7,
        "image": "https://i.imgur.com/k0KTXMi.png",
        "quantity": 1
    },
    {
        "id": 7,
        "name": "Milkshake Ovomaltine",
        "category": "Sobremesas",
        "price": 10,
        "image": "https://i.imgur.com/GQyQW64.png",
        "quantity": 1
    },
    {
        "id": 8,
        "name": "Sunday",
        "category": "Sobremesas",
        "price": 10,
        "image": "https://i.imgur.com/5hNbmcM.png",
        "quantity": 1
    }
]
```

## Cadastro de Usuários 👤

Para cadastrar um usuário é necessário realizar uma requisição `POST` com o endpoint `/register`.

O `body` da requisição deve conter os seguintes campos, sendo obrigatórios o email e a senha:

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
	"name": "Jhon Doe",
	"email": "jhondoe@mail.com",
	"password": "******",
}
```

Caso corra tudo bem, esse é o formato da resposta:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Impob25kb2VAbWFpbC5jb20iLCJpYXQiOjE2NDIwOTI0NTMsImV4cCI6MTY0MjA5NjA1Mywic3ViIjoiMSJ9.f5wwehC5t5ER2dgmA-o560MjcOhzyyLxG7XrDvjwSuQ",
	"user": {
	  "email": "jhondoe@mail.com",
	  "name": "Jhon Doe",
    "id": 1
  }
```

### Possíveis Erros 💣

`POST /register - FORMATO DA RESPOSTA - STATUS 400`

```
"Email and password are required"
```

`POST /register - FORMATO DA RESPOSTA - STATUS 400`

```
"Email already exists"
```

`POST /register - FORMATO DA RESPOSTA - STATUS 400`

```
"Email format is invalid"
```

## Login 💻

Alguns endpoints exigem que o usuário esteja logado. Essa é a estrutura base do `body` da requisição de `Login`:

`POST /login FORMATO DA REQUISIÇÃO`

```json
{
	"email": "jhondoe@mail.com",
  "password": "123456"
}
```

Se tudo der certo, essa é a resposta esperada:

`POST /login FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Impob25kb2VAbWFpbC5jb20iLCJpYXQiOjE2NDIxMDA5NDEsImV4cCI6MTY0MjEwNDU0MSwic3ViIjoiMSJ9.kayLOprKoebmHalz5vb7mFj7zQ39-QrCVZTc8FEgbu4",
	  "user": {
	    "email": "jhondoe@mail.com",
      "name": "Jhon Doe",
      "id": 1
    }
}
```

### Possíveis Erros 💣

---

`POST /register - FORMATO DA RESPOSTA - STATUS 400`

```
"Cannot find user"
```

`POST /register - FORMATO DA RESPOSTA - STATUS 400`

```
"Incorrect password"
```

`POST /register - FORMATO DA RESPOSTA - STATUS 400`

```
"Email and password are required"
```

# Rotas que necessitam de autenticação 🔒

Essas requisições necessitam do Bearer Token do usuário para serem efetuadas!

## Cadastrando Sugestões 📝

Para cadastrar os sugestões, é necessário que o usuário esteja logado e seja o dono daquela sugestão. O `body` da requisição tem o seguinte formato:

`POST /suggestions - FORMATO DA REQUISIÇÂO`

```json
{
	"text": "Poderiam adicionar mais opções de sobremesas.",
  "userId": 1
}
```

`POST /animals - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"text": "Poderiam adicionar mais opções de sobremesas.",
  "userId": 1,
	"id": 2
}
```

## Listando Sugestões 📝

Para listar os sugestões, é necessário que o usuário esteja logado. O `body` da requisição tem o seguinte formato:

`POST /suggestions - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"id": 1,
  "text": "Poderiam adicionar mais opções de sobremesas.",
  "userId": 1
}
```

### Possíveis Erros 💣

`GET /vaccines - FORMATO DA RESPOSTA - STATUS 401`

```
"Missing authorization header"
```

# Query Params 🗄️

Para mais informações sobre os query params que podem ser utilizados nesta aplicação, visite a biblioteca do [JSON-Server](https://github.com/typicode/json-server#routes).
