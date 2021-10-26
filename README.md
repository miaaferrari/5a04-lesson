ATIVIDADE 5A04

ENDPOINTS
A API tem um total de 9 endpoints, sendo em volta principalmente do usuário - podendo cadastrar seu perfil, cursos e livros.

O JSON para utilizar no Insomnia é este aqui -> 
Para importar o JSON no Insomnia é só clicar na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From Url" e colocar o link acima v

O url base da API é 

Rotas que não precisam de autenticação



LISTANDO USUÁRIOS

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os devs já cadastrados na plataforma, na API podemos acessar a lista dessa forma: Aqui conseguimos ver os usuários, suas tecnologias e seus trabalhos cadastrados.

GET /users - FORMATO DA RESPOSTA - STATUS 200
 
 [
  {
    "email": "kenzinho@mail.com",
    "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
    "name": "Kenzinho",
    "age": 38,
    "id": 1
  },
  {
    "email": "mia@gmail.com",
    "password": "$2a$10$AM..4uCJbQpPMcFbdryPJ.tWlb/U1tkkA1XDjBX9lx7zJgJIZPM5W",
    "name": "mia",
    "id": 2
  }
]


Podemos acessar um usuário específico utilizando o endpoint:

GET /users/:user_id - FORMATO DA RESPOSTA - STATUS 
{
  "email": "mia@gmail.com",
  "password": "$2a$10$AM..4uCJbQpPMcFbdryPJ.tWlb/U1tkkA1XDjBX9lx7zJgJIZPM5W",
  "name": "mia",
  "id": 2
}

Também podemos pegar os cursos ou livros de um usuário específico utilizando os endpoints abaixo:

GET /users/2?_embed=books - FORMATO DA RESPOSTA - STATUS 200

{
  "email": "mia@gmail.com",
  "password": "$2a$10$AM..4uCJbQpPMcFbdryPJ.tWlb/U1tkkA1XDjBX9lx7zJgJIZPM5W",
  "name": "mia",
  "id": 2,
  "books": [
    {
      "name": "Águas de Primavera",
      "author": "Ivan Turguêniev",
      "category": "romance",
      "userId": 2,
      "id": 1
    },
    {
      "name": "Fundação",
      "author": "Isaac Asimov",
      "category": "sci-fi",
      "userId": 2,
      "id": 2
    }
  ]
}

GET /users/2?_embed=course - FORMATO DA RESPOSTA - STATUS 200

{
  "email": "mia@gmail.com",
  "password": "$2a$10$AM..4uCJbQpPMcFbdryPJ.tWlb/U1tkkA1XDjBX9lx7zJgJIZPM5W",
  "name": "mia",
  "id": 2,
  "course": [
    {
      "name": "Kenzie Q1",
      "finish": true,
      "userId": 2,
      "id": 1
    },
    {
      "name": "Kenzie Q2",
      "finish": false,
      "userId": 2,
      "id": 2
    },
    {
      "name": "Kenzie Q3",
      "finish": false,
      "userId": 2,
      "id": 3
    },
    {
      "name": "Kenzie Q4",
      "finish": false,
      "userId": 2,
      "id": 4
    }
  ]
}



LISTANDO LIVROS

GET /books - FORMATO DA RESPOSTA - STATUS 200

[
  {
    "name": "Águas de Primavera",
    "author": "Ivan Turguêniev",
    "category": "romance",
    "userId": 2,
    "id": 1
  },
  {
    "name": "Fundação",
    "author": "Isaac Asimov",
    "category": "sci-fi",
    "userId": 2,
    "id": 2
  }
]

Também é possível pegar os livros de um usuário específico com o endpoint abaixo:

GET /users/2/books - FORMATO DA RESPOSTA - STATUS 200

[
  {
    "name": "Águas de Primavera",
    "author": "Ivan Turguêniev",
    "category": "romance",
    "userId": 2,
    "id": 1
  },
  {
    "name": "Fundação",
    "author": "Isaac Asimov",
    "category": "sci-fi",
    "userId": 2,
    "id": 2
  }
]



LISTANDO CURSOS ESPECÍFICOS DE UM USUÁRIO

GET /users/2/course - FORMATO DA RESPOSTA - STATUS 200

[
  {
    "name": "Kenzie Q1",
    "finish": true,
    "userId": 2,
    "id": 1
  },
  {
    "name": "Kenzie Q2",
    "finish": false,
    "userId": 2,
    "id": 2
  },
  {
    "name": "Kenzie Q3",
    "finish": false,
    "userId": 2,
    "id": 3
  },
  { 
    "name": "Kenzie Q4",
    "finish": false,
    "userId": 2,
    "id": 4
  }
]



CRIAÇÃO DE USUÁRIO

POST /users - FORMATO DA REQUISIÇÃO

{
	"email": "mia@gmail.com",
	"password": "123456",
	"name": "mia"
}

FORMATO DA RESPOSTA - STATUS 201

{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1pYUBnbWFpbC5jb20iLCJpYXQiOjE2MzUyNzU0NjQsImV4cCI6MTYzNTI3OTA2NCwic3ViIjoiMiJ9.AA6dvgvGWg9ci4FG9cyV8zmgfviWe68bpbE16edPgms",
  "user": {
    "email": "mia@gmail.com",
    "name": "mia",
    "id": 2
  }
}



LOGIN

POST /login - FORMATO DA REQUISIÇÃO

{
	"email": "mia@gmail.com",
	"password": "123456"
}

FORMATO DA RESPOSTA - STATUS 201

{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1pYUBnbWFpbC5jb20iLCJpYXQiOjE2MzUyNzU1MzEsImV4cCI6MTYzNTI3OTEzMSwic3ViIjoiMiJ9.E1OIzbur7IAOX7cwpQ46HwxOeBPHoY6s8rqwhTdijds",
  "user": {
    "email": "mia@gmail.com",
    "name": "mia",
    "id": 2
  }
}

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.





ROTAS QUE NECESSITAM DE AUTORIZAÇÃO

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

    Authorization: Bearer {token}

Após o usuário estar logado, ele deve conseguir visualizar e adicionar livros que leu e cursos que fez até agora.

ADICIONAR LIVROS

POST /books - FORMATO DA REQUISIÇÃO

{
	"name": "Fundação",
	"author": "Isaac Asimov",
	"category": "sci-fi",
	"userId": 2
}

*userId é o id do usuário criado no momento do registro na aplicação.

FORMATO DA RESPOSTA - STATUS 201

{
  "name": "Fundação",
  "author": "Isaac Asimov",
  "category": "sci-fi",
  "userId": 2,
  "id": 2
}



ADICIONAR CURSOS

POST /course - FORMATO DA REQUISIÇÃO

{
	"name": "Kenzie Q4",
	"finish": false,
	"userId": 2
}

FORMATO DA RESPOSTA - STATUS 201

{
  "name": "Kenzie Q4",
  "finish": false,
  "userId": 2,
  "id": 5
}

Também é necessária autorização para ver todos os cursos com o endpoint abaixo:

GET /course - FORMATO DA RESPOSTA - STATUS 200

[
  {
    "name": "Kenzie Q1",
    "finish": true,
    "userId": 2,
    "id": 1
  },
  {
    "name": "Kenzie Q2",
    "finish": false,
    "userId": 2,
    "id": 2
  },
  {
    "name": "Kenzie Q3",
    "finish": false,
    "userId": 2,
    "id": 3
  },
  {
    "name": "Kenzie Q4",
    "finish": false,
    "userId": 2,
    "id": 4
  }
]


