# Readme

## Migrations
```
dotnet ef database update
```

## Development

### Secrets
```
dotnet user-secrets set --project ./Isa.Api "JwtSettings:Secret" "" 
```

# Autenticação

## Registro de Usuário

Este é um endpoint de registro de usuário que permite aos usuários se inscreverem em um serviço. Ele suporta a criação de contas de usuário com um nome, endereço de e-mail e senha.

### Endpoint

- Método HTTP: POST
- URL: `https://api.isafin.com.br/auth/register`

### Parâmetros da Solicitação

O corpo da solicitação deve ser um objeto JSON com os seguintes campos:

- `name` (String) - O nome do usuário.
- `email` (String) - O endereço de e-mail do usuário.
- `password` (String) - A senha do usuário.

Exemplo de Corpo da Solicitação:

```json
{
	"name": "Fulano",
	"email": "fulano@silva.com",
	"password": "Pwd@123"
}
```


## Login de Usuário

Este é um endpoint de login de usuário que permite aos usuários autenticarem-se em um serviço. Os usuários devem fornecer seu endereço de e-mail e senha para fazer login.

### Endpoint

- Método HTTP: POST
- URL: `https://api.isafin.com.br/auth/login`

### Parâmetros da Solicitação

O corpo da solicitação deve ser um objeto JSON com os seguintes campos:

- `email` (String) - O endereço de e-mail do usuário.
- `password` (String) - A senha do usuário.

Exemplo de Corpo da Solicitação:

```json
{
	"email": "user1@example.com",
	"password": "hashed_password1"
}
```
### Exemplo de resposta
```json
{
    "id": "550e8400-e29b-41d4-a716-446655440001",
    "name": "User1",
    "email": "user1@example.com",
    "token": "eyJhbGciOiJBMTI4Q0JDLUhTMjU2IiwidHlwIjoiSldUIn0.eyJzdWIiOiI1NTBlODQwMC1lMjliLTQxZDQtYTcxNi00NDY2NTU0NDAwMDEiLCJnaXZlbl9uYW1lIjoiVXNlcjEiLCJqdGkiOiI3NGJlYTZiZC02NTZlLTQ0OWUtOTlhNy05MDA5NDExYTU5ZmMiLCJleHAiOjE3MDExMjQ2NjQsImlzcyI6IklTQSIsImF1ZCI6IklTQSJ9.kBRoyubDV6_uSti135IvwOqHYvo_vIXmO-_sFtyQngY"
}
```
### Token

Interessante apontar que após o login, todas as rotas necessitam do token.

---


# Usuário

## GET

Esta rota será utilizada para retornar todos os dados do usuário.

### Endpoint

- Método HTTP: GET
- URL: `https://api.isafin.com.br/user/{userID}`

### Exemplo de retorno

```json
{
    "user": {
        "email": "user1@example.com",
        "failedLoginAttempts": 0,
        "goal": 10000,
        "gender": 1,
        "createdDateTime": "2023-11-15T16:06:25.530164Z",
        "updatedDateTime": "2023-11-15T16:06:25.530164Z",
        "name": "testando",
        "password": "hashed_password1",
        "phone": "12341245",
        "revenue": 12000,
        "status": true,
        "id": {
            "value": "550e8400-e29b-41d4-a716-446655440001"
        },
        "domainEvents": []
    }
}
```

---

## Update

Esta rota será utilizada para atualizar os dados de usuário, senha entre outros pontos.

### Endpoint

- Método HTTP: PUT
- URL: `https://api.isafin.com.br/user`

### Parâmetros da Solicitação

O corpo da solicitação deve ser um objeto JSON com os seguintes campos:

- `name` (String) - O nome do usuário.
- `email` (String) - O endereço de e-mail do usuário.
- `password` (String) - A senha do usuário.
- `userId` (Guid) - ID de Usuário.
- `revenue` (Decimal) - Valor será considerado como a renda.
- `phone`  (String) - Telefone.
- `gender` (Bool) - Utilizaremos apenas Masculino e Feminino.
- `status` (Bool) - Status do user.
- `NewPassword` (String) - Aqui mais pra frente será implementado a validação para renovar senha.
- `ReNewPassword` (String) - Aqui mais pra frente será implementado a validação para renovar senha.
- 

Exemplo de Corpo da Solicitação:

```json
{
    "UserId": "550e8400-e29b-41d4-a716-446655440001",
    "revenue": 12000,
    "goal": 10000,
    "name": "testando",
    "phone": "12341245",
    "email": "user1@example.com",
    "gender": true,
    "status": true,
    "NewPassword": "hashed_password1",
    "ReNewPassword": "hashed_password1",
    "Password": "hashed_password1"
}
```

---

## Delete

Esta rota será utilizada para deletar os dados de usuário.

### Endpoint

- Método HTTP: DELETE
- URL: `https://api.isafin.com.br/user/{userId}`

### Retorno

```json
{
 "Aguardando implementação"
}
```

---


# Bancos


## Cadastro de bancos

Este é um endpoint de cadastro dos bancos e inicialmente será utilizado apenas para testes, essa rota em teoria não será necessária.

## Endpoint

- Método HTTP: POST
- URL: `https://api.isafin.com.br/banks`

## Parâmetros da Solicitação

O corpo da solicitação deve ser um objeto JSON com os seguintes campos:

- `code` (int) - Código do banco registrado no sistema nacional.
- `name` (String) - Nome do banco.
- `parameters` (String) - Parametros necessários para integração.
- `ProfileImage` (String) - Nome da imagem.
- `status` (Int) - Status atual da integração.

Exemplo de Corpo da Solicitação:

```json
{
    "Code":123,
    "Name":"TestBank2",
    "Parameters":"{['conta','password']}",
    "ProfileImage":"Nubank.png",
    "Status":1
}
```


---

## Listagem de Bancos

Este é um endpoint de listagem de bancos, inicialmente iremos precisar da inserção do UserId na URL para o funcionamento.
Aqui retornamos todos os bancos cadastrados.

### Endpoint

- Método HTTP: POST
- URL: `https://api.isafin.com.br/banks/{userId}`

### Exemplo de resposta

```json
[
    {
        "id": "6cd63d86-3ef2-4cf7-ac0f-d86d1cf25095",
        "code": "341",
        "name": "Itaú",
        "profileImage": "itau.png",
        "status": 1,
        "createdDateTime": "2023-11-07T12:44:23.762166Z",
        "updatedDateTime": "2023-11-07T12:44:23.762166Z"
    },
    {
        "id": "b4905805-9a4b-4707-b7a9-adbdd6c4dc97",
        "code": "237",
        "name": "Bradesco",
        "profileImage": "bradesco.png",
        "status": 1,
        "createdDateTime": "2023-11-07T12:44:23.762166Z",
        "updatedDateTime": "2023-11-07T12:44:23.762166Z"
    },
    {
        "id": "d1a56367-9ad5-4bb6-8458-c5702f1abb44",
        "code": "260",
        "name": "Nubank",
        "profileImage": "nubank.png",
        "status": 1,
        "createdDateTime": "2023-11-07T12:44:23.762166Z",
        "updatedDateTime": "2023-11-07T12:44:23.762166Z"
    }
]
```
---

## Setup de Bancos

Este é um endpoint será utilizado quando selecionado o banco para iniciar a conexão, aqui retornamos os valores necessários para integração *conta x banco* o foco é retornar os dados necessários para o cliente conseguir fazer a conexão.

### Endpoint

- Método HTTP: GET
- URL: `https://api.isafin.com.br/banks/setup/{bankCode}`

### Exemplo de resposta

```json
{
    "code": 260,
    "name": "Nubank",
    "profileImage": "nubank.png",
    "status": 1,
    "parameters": "{\"apiKey\": \"sua_chave_api_nubank\"}",
    "bankParameters": [
        {
            "name": "Password",
            "format": "P@ssw0rd",
            "description": "Integração com a API da NUBANK",
            "step": 2,
            "order": 2,
            "id": {
                "value": "0036b428-87e8-11ee-b9d1-0242ac120002"
            },
            "domainEvents": []
        },
        {
            "name": "Login",
            "format": "email@email.com",
            "description": "Integração com a API da NUBANK",
            "step": 2,
            "order": 1,
            "id": {
                "value": "f965b28e-87e7-11ee-b9d1-0242ac120002"
            },
            "domainEvents": []
        }
    ],
    "createdDateTime": "2023-11-15T16:06:25.412349Z",
    "updatedDateTime": "2023-11-15T16:06:25.412349Z",
    "id": {
        "value": "d1a56367-9ad5-4bb6-8458-c5702f1abb44"
    },
    "domainEvents": []
}
```

Ainda existem alguns pontos que precisamos melhorar na integração com o banco, primeiro ponto é o teste de envio dos paremetros na rota de accounts

---

# Transações

## Cadastro de Transações

Este endpoint permite aos usuários cadastrar uma nova transação no sistema.

## Endpoint

- Método HTTP: POST
- URL: `https://api.isafin.com.br/transactions`

## Parâmetros da Solicitação

O corpo da solicitação deve ser um objeto JSON com os seguintes campos:

- `accountId` (String) - ID da conta à qual a transação será associada.
- `description` (String) - Descrição da transação.
- `document` (String) - Documento associado à transação.
- `bankCode` (int) - Código do banco da transação.
- `frequency` (int) - Frequência da transação.
- `status` (bool) - Status da transação.
- `ignored` (bool) - Indicação se a transação foi ignorada.
- `fixed` (bool) - Indicação se a transação é fixa.
- `activityDate` (String) - Data de atividade da transação no formato ISO 8601.
- `classificationType` (int) - ID do tipo de classificação da transação.
- `amount` (float) - Valor da transação.
- `typeEntry` (int) - Tipo de entrada da transação.
- `typeValue` (int) - Tipo de valor da transação.
- `userId` (String) - ID do usuário associado à transação.

Exemplo de Corpo da Solicitação:

```json
{
    "accountId": "1bcb59c3-3187-4de1-a136-6b6ae19f2435",
    "description": "Pagamento de Fatura",
    "document": "teste",
    "bankCode": 260,
    "frequency": 0,
    "status": true,
    "ignored": false,
    "fixed": true,
    "activityDate": "2023-10-23T18:25:43.511Z",
    "classificationType": 1,
    "amount": -1000.00,
    "typeEntry": 2,
    "typeValue": 0,
    "userId": "1bcb59c3-3187-4de1-a136-6b6ae19f2435"
}
```
---


## Filtrar Transações

Este endpoint permite aos usuários filtrar transações com base em vários critérios, como o ID do usuário, a data de início e de fim do filtro e o ID da classificação.
Um ponto importante é que atualmente fazemos as *buscas* por transações de acordo com o mês, a data é aberta para ser selecionada mas por padrão faremos buscas `mensais`.

## Endpoint

- Método HTTP: POST
- URL: `https://api.isafin.com.br/transactions/filter`

## Parâmetros da Solicitação

O corpo da solicitação deve ser um objeto JSON com os seguintes campos:

```json
{
	"userId": "1bcb59c3-3187-4de1-a136-6b6ae19f2435",   //obrigatório
	"FilterStart": "2023-10-01T18:25:43.511Z",          //obrigatório
	"FilterEnd": "2023-10-30T18:25:43.511Z",            //obrigatório
	"CategoryId": 0                                     //obrigatório
}
```
- `userId` (String) - ID do usuário para o qual as transações serão filtradas.
- `FilterStart` (String) - Data de início do filtro no formato ISO 8601.
- `FilterEnd` (String) - Data de término do filtro no formato ISO 8601.
- `ClassificationId` (int) - ID da classificação para filtrar transações. (Opcional)
- `Outros` no *resumo* é toda transação sem categoria definida, `CategoryId` = 0
- `Gastos` o `CategoryId` = 1
- `Receita` o `CategoryId` = 2
- `Investimento` o `CategoryId` = 3


## Exemplo de resposta

```json
{
    "resum": {
        "total": 6930.00,
        "higherTransaction": "A compra de maior valor é da Mercado sendo 900,00",
        "lowerTransaction": "A compra de menor valor é da Mercado sendo 500,00",
        "goalPercent": "Você gastou 59% do valor total da sua renda"
    },
    "transaction": [
        {
            "activityDate": "2023-09-13T16:17:28.093793Z",
            "origin": "Cartão de Crédito",
            "description": "Roupas",
            "descriptionUser": "",
            "method": "Cartão final (5678)",
            "amount": 720.00,
            "bankCode": 260,
            "frequency": 1,
            "userId": {
                "value": "550e8400-e29b-41d4-a716-446655440001"
            },
            "accountId": {
                "value": "550e8400-e29b-41d4-a716-446655440016"
            },
            "status": true,
            "ignored": false,
            "fixed": false,
            "categoryId": 2,
            "id": {
                "value": "550e8400-e29b-41d4-a716-446655440134"
            },
            "domainEvents": []
        },
        {
            "activityDate": "2023-11-13T16:10:36.592365Z",
            "origin": "Cartão de Crédito",
            "description": "Mercado",
            "descriptionUser": "",
            "method": "Cartão final (1234)",
            "amount": 700.00,
            "bankCode": 260,
            "frequency": 1,
            "userId": {
                "value": "550e8400-e29b-41d4-a716-446655440001"
            },
            "accountId": {
                "value": "550e8400-e29b-41d4-a716-446655440010"
            },
            "status": true,
            "ignored": false,
            "fixed": false,
            "categoryId": 2,
            "id": {
                "value": "550e8400-e29b-41d4-a716-446655440124"
            },
            "domainEvents": []
        }
    ],
    "historyTransaction": []
}
```
---

## Resumo de Transações

Este endpoint permite aos visualização do resumo de transações com base em vários critérios, como o ID do usuário, a data de início e de fim do filtro.
Um ponto importante é que atualmente fazemos as *buscas* por transações de acordo com o mês, a data é aberta para ser selecionada mas por padrão faremos buscas `mensais`.

## Endpoint

- Método HTTP: POST
- URL: `https://api.isafin.com.br/transactions/resum`

## Parâmetros da Solicitação

O corpo da solicitação deve ser um objeto JSON com os seguintes campos:

```json
{
	"userId": "1bcb59c3-3187-4de1-a136-6b6ae19f2435",   //obrigatório
	"FilterStart": "2023-10-01T18:25:43.511Z",          //obrigatório
	"FilterEnd": "2023-10-30T18:25:43.511Z",            //obrigatório
}
```
- `userId` (String) - ID do usuário para o qual as transações serão filtradas.
- `FilterStart` (String) - Data de início do filtro no formato ISO 8601.
- `FilterEnd` (String) - Data de término do filtro no formato ISO 8601.


## Exemplo de resposta

```json
{
    "resum": {
        "others": 6930.00,
        "spend": 6010.00,
        "saves": 0,
        "earn": 0
    },
    "transaction": [
        {
            "activityDate": "2023-09-14T16:17:28.093793Z",
            "origin": "Conta Corrente",
            "description": "Farmácia",
            "descriptionUser": "",
            "method": "Cartão final (1234)",
            "amount": 530.00,
            "bankCode": 260,
            "frequency": 1,
            "userId": {
                "value": "550e8400-e29b-41d4-a716-446655440001"
            },
            "accountId": {
                "value": "550e8400-e29b-41d4-a716-446655440015"
            },
            "status": true,
            "ignored": false,
            "fixed": false,
            "categoryId": 1,
            "id": {
                "value": "550e8400-e29b-41d4-a716-446655440133"
            },
            "domainEvents": []
        },
        {
            "activityDate": "2023-09-13T16:17:28.093793Z",
            "origin": "Cartão de Crédito",
            "description": "Roupas",
            "descriptionUser": "",
            "method": "Cartão final (5678)",
            "amount": 720.00,
            "bankCode": 260,
            "frequency": 1,
            "userId": {
                "value": "550e8400-e29b-41d4-a716-446655440001"
            },
            "accountId": {
                "value": "550e8400-e29b-41d4-a716-446655440016"
            },
            "status": true,
            "ignored": false,
            "fixed": false,
            "categoryId": 2,
            "id": {
                "value": "550e8400-e29b-41d4-a716-446655440134"
            },
            "domainEvents": []
        },
        {
            "activityDate": "2023-09-12T16:17:28.093793Z",
            "origin": "Conta Corrente",
            "description": "Eletrônicos",
            "descriptionUser": "",
            "method": "Pix",
            "amount": 950.00,
            "bankCode": 260,
            "frequency": 1,
            "userId": {
                "value": "550e8400-e29b-41d4-a716-446655440001"
            },
            "accountId": {
                "value": "550e8400-e29b-41d4-a716-446655440017"
            },
            "status": true,
            "ignored": false,
            "fixed": false,
            "categoryId": 3,
            "id": {
                "value": "550e8400-e29b-41d4-a716-446655440135"
            },
            "domainEvents": []
        }
    ]
}
```
---
