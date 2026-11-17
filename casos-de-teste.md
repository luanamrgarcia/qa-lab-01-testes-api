# QA Lab 01 - Testes de API REST

## CT-01 - Criar reserva com dados válidos

**Objetivo:** Validar se a API permite criar uma reserva
com dados válidos e registra corretamente as informações enviadas.

**Tipo de teste:** Funcional positivo

**Ferramenta:** Postman

**API:** Restful Booker

**Status:** Aprovado

### Pré-condições

- API Restful Booker acessível.
- Postman disponível para execução das requisições.
- Dados válidos definidos para criação da reserva.

### Dados de teste

**Método:** POST  
**Endpoint:** `https://restful-booker.herokuapp.com/booking`

```json
{
  "firstname": "Ana",
  "lastname": "Silva",
  "totalprice": 250,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-12-10",
    "checkout": "2026-12-15"
  },
  "additionalneeds": "Breakfast"
}
```

### Passos para execução

1. Acessar o Postman.
2. Criar uma nova requisição utilizando o método `POST`.
3. Informar a URL `https://restful-booker.herokuapp.com/booking`.
4. Selecionar Body → raw → JSON e inserir o JSON apresentado na seção Dados de teste.
5. Clicar em **Send**.
6. Verificar se o POST retornou `200 OK` e um `bookingid`.
7. Criar uma nova requisição utilizando o método `GET`.
8. Informar a URL `https://restful-booker.herokuapp.com/booking/{id}`, substituindo `{id}` pelo identificador retornado no POST.
9. Clicar em **Send**.
10. Verificar se o GET retornou `200 OK` e se os dados correspondem aos enviados na criação.


### Resultado esperado

A API deve criar uma reserva com os dados válidos informados, retornar `200 OK` e fornecer um `bookingid`.

Ao consultar a reserva pelo identificador retornado, a API deve responder `200 OK` e apresentar os mesmos dados enviados na criação.

### Resultado obtido

A requisição `POST /booking` retornou `200 OK` e o `bookingid` 357.

A consulta `GET /booking/357` retornou `200 OK`, apresentando os dados correspondentes aos informados na criação.

### Evidências

- [CT-01 - Criação da reserva](evidências/CT-01%20Criando%20Reserva.png)
- [CT-01 - Consulta para validação](evidências/CT-01%20Consultando%20Reserva.png)



## CT-02 - Consultar reserva inexistente

**Objetivo:** Validar o comportamento da API ao consultar uma reserva com identificador inexistente.

**Tipo de teste:** Funcional negativo

**Ferramenta:** Postman

**API:** Restful Booker

**Status:** Aprovado

### Pré-condições

- API Restful Booker acessível.
- Postman disponível para execução.
- Utilizar um identificador de reserva inexistente no momento do teste.

### Dados de teste

**Método:** GET

**Endpoint:** `https://restful-booker.herokuapp.com/booking/{id}`

**Parâmetro:** `{id}` - identificador inexistente.

**ID utilizado na execução:** `111`

### Passos para execução

1. Acessar o Postman.
2. Criar uma nova requisição utilizando o método `GET`.
3. Informar a URL https://restful-booker.herokuapp.com/booking/{id}, substituindo {id} por um identificador que não corresponda a uma reserva existente no momento da execução.
4. Clicar em **Send**.
5. Verificar se a API retornou `404 Not Found`.
6. Verificar se a resposta não apresentou dados de nenhuma reserva.

### Resultado esperado

A API deve retornar `404 Not Found`, sem apresentar dados de uma reserva.

### Resultado obtido

A requisição `GET /booking/111` retornou `404 Not Found`, com o corpo da resposta `Not Found`.

### Evidências

- [CT-02 - Consulta de reserva inexistente](evidências/CT-02%20Consultar%20reserva%20inexistente.png)


## CT-03 - Atualizar reserva existente

**Objetivo:** Validar se a API permite atualizar os dados de uma reserva existente e se as alterações são mantidas após uma nova consulta.

**Tipo de teste:** Funcional positivo

**Ferramenta:** Postman

**API:** Restful Booker

**Status:** Aprovado

### Pré-condições

- API Restful Booker acessível.
- Postman disponível para execução.
- Reserva existente com identificador conhecido.
- Credenciais válidas disponíveis para autenticação via Basic Auth.
- Dados válidos definidos para atualização.


### Dados de teste

**Método principal:** PUT

**Endpoint:** `https://restful-booker.herokuapp.com/booking/{id}`

**Parâmetro:** `{id}` - identificador de uma reserva existente.

**ID utilizado na execução:** `115`

**Autenticação:** Basic Auth

**Dados para criação da reserva:**
- Método: `POST`
- Endpoint: `https://restful-booker.herokuapp.com/booking`
- Utilizar os mesmos dados do JSON de atualização, mas com `totalprice` igual a `250`.

**Alteração realizada:**
- Campo: `totalprice`
- Valor original: `250`
- Novo valor: `350`
- Demais campos: manter os valores originais da reserva.


**JSON utilizado na atualização:**

```json
{
  "firstname": "Ana",
  "lastname": "Silva",
  "totalprice": 350,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-12-10",
    "checkout": "2026-12-15"
  },
  "additionalneeds": "Breakfast"
}
```

### Passos para execução

1. Acessar o Postman.
2. Criar uma requisição `POST` para `https://restful-booker.herokuapp.com/booking`, selecionar **Body → raw → JSON** e inserir o JSON de atualização com `totalprice` igual a `250`.
3. Clicar em **Send**, verificar se a API retornou `200 OK` e guardar o `bookingid` retornado.
4. Criar uma requisição utilizando o método `PUT` para atualizar a reserva.
5. Informar a URL `https://restful-booker.herokuapp.com/booking/{id}`, substituindo `{id}` pelo identificador retornado no POST.
6. Na aba **Headers**, configurar o cabeçalho `Authorization` com credenciais válidas utilizando o esquema `Basic Auth`.
7. Selecionar **Body → raw → JSON**.
8. Inserir o JSON de atualização documentado, com `totalprice` igual a `350` e os demais campos inalterados.
9. Clicar em **Send**.
10. Verificar se o PUT retornou `200 OK` e apresentou os dados atualizados.
11. Criar uma requisição utilizando o método `GET`.
12. Informar a URL `https://restful-booker.herokuapp.com/booking/{id}`, utilizando o mesmo identificador da reserva.
13. Clicar em **Send**.
14. Verificar se o GET retornou `200 OK`.
15. Confirmar que `totalprice` está com o valor `350` e que os demais dados permanecem iguais aos da criação.


### Resultado esperado

A API deve permitir a atualização da reserva autenticada, retornar `200 OK` e apresentar o novo valor de `totalprice`.

A consulta posterior deve retornar o preço atualizado para `350`, mantendo os demais dados da reserva.

### Resultado obtido

A reserva de ID `115` foi criada com preço `250`.

A requisição `PUT /booking/115` retornou `200 OK`, apresentando o preço atualizado para `350`.

A consulta `GET /booking/115` retornou `200 OK`, confirmando o novo preço e a manutenção dos demais dados.

### Evidências

- [CT-03 - Criação da reserva](evidências/CT-03%20Criando%20Reserva.png)
- [CT-03 - Atualização da reserva](evidências/CT-03%20Atualizando%20Reserva.png)
- [CT-03 - Validação da atualização](evidências/CT-03%20Conferido%20a%20atualização.png)


## CT-04 - Impedir atualização sem autenticação

**Objetivo:** Validar se a API impede a atualização de uma reserva quando a requisição não possui autenticação válida, preservando os dados existentes.

**Tipo de teste:** Funcional negativo

**Ferramenta:** Postman

**API:** Restful Booker

**Status:** Aprovado

### Pré-condições

- API Restful Booker acessível.
- Postman disponível para execução.
- Reserva existente com identificador conhecido.
- Dados válidos definidos para a tentativa de atualização.

### Dados de teste

**Método principal:** PUT

**Endpoint:** `https://restful-booker.herokuapp.com/booking/{id}`

**Parâmetro:** `{id}` - identificador de uma reserva existente.

**ID utilizado na execução:** `3281`

**Autenticação:** Não informada.

**Dados para criação da reserva:**
- Método: `POST`
- Endpoint: `https://restful-booker.herokuapp.com/booking`
- Utilizar os mesmos dados do JSON da tentativa de atualização, mas com `totalprice` igual a `350`.

**Alteração solicitada:**
- Campo: `totalprice`
- Valor original: `350`
- Valor solicitado: `500`
- Demais campos: manter os valores originais.


**JSON utilizado na tentativa de atualização:**

```json
{
  "firstname": "Bernaddo",
  "lastname": "Rodrigues",
  "totalprice": 500,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-12-22",
    "checkout": "2026-12-30"
  },
  "additionalneeds": "Breakfast"
}
```

### Passos para execução

1. Acessar o Postman.
2. Criar uma requisição `POST` para `https://restful-booker.herokuapp.com/booking`, selecionar **Body → raw → JSON** e inserir o JSON da tentativa de atualização com `totalprice` igual a `350`.
3. Clicar em **Send**, verificar se a API retornou `200 OK` e guardar o `bookingid` retornado.
4. Criar uma requisição utilizando o método `PUT`.
5. Informar a URL `https://restful-booker.herokuapp.com/booking/{id}`, substituindo `{id}` pelo identificador da reserva.
6. Na aba **Authorization**, selecionar **No Auth**.
7. Garantir que não existam tokens ou cookies de autenticação sendo enviados.
8. Selecionar **Body → raw → JSON**.
9. Inserir o JSON completo da reserva, alterando `totalprice` de `350` para `500`.
10. Clicar em **Send**.
11. Verificar se a API retornou `403 Forbidden`.
12. Criar uma requisição `GET` para `https://restful-booker.herokuapp.com/booking/{id}`, utilizando o mesmo identificador da reserva.
13. Clicar em **Send**.
14. Verificar se o GET retornou `200 OK`.
15. Confirmar que `totalprice` permaneceu em `350` e que os demais dados não foram alterados.

### Resultado esperado

A API deve impedir a atualização sem autenticação, retornando `403 Forbidden`.

A consulta posterior deve confirmar que os dados da reserva permaneceram inalterados.

### Resultado obtido

A requisição `PUT /booking/3281`, sem autenticação, retornou `403 Forbidden`.

A consulta `GET /booking/3281` retornou `200 OK`, confirmando que o preço permaneceu em `350`, sem aplicar a alteração solicitada para `500`.

### Evidências

- [CT-04 - Reserva criada](evidências/CT-04%20Reserva%20criada.png)
- [CT-04 - Atualização sem autenticação](evidências/CT-04%20Atualização%20sem%20Autenticação.png)
- [CT-04 - Consulta após a tentativa](evidências/CT-04%20Consulta%20após%20a%20tentativa.png)


## CT-05 - Excluir reserva existente

**Objetivo:** Validar se a API permite excluir uma reserva existente e se ela deixa de estar disponível para consulta.

**Tipo de teste:** Funcional positivo

**Ferramenta:** Postman

**API:** Restful Booker

**Status:** Aprovado

### Pré-condições

- API Restful Booker acessível.
- Postman disponível para execução.
- Reserva existente com identificador conhecido.
- Credenciais válidas disponíveis para autenticação.

### Dados de teste

**Método principal:** DELETE

**Endpoint:** `https://restful-booker.herokuapp.com/booking/{id}`

**Parâmetro:** `{id}` - identificador de uma reserva existente.

**ID utilizado na execução:** `3003`

**Autenticação:** Basic Auth (credenciais válidas).

**Dados para criação da reserva:**

**Método:** POST

**Endpoint:** `https://restful-booker.herokuapp.com/booking`

**JSON utilizado na criação:**

```json
{
  "firstname": "Lucas",
  "lastname": "Eduardo",
  "totalprice": 150,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-12-24",
    "checkout": "2026-12-25"
  },
  "additionalneeds": "Breakfast"
}
```

### Passos para execução

1. Acessar o Postman.
2. Criar uma requisição utilizando o método `POST`.
3. Informar a URL `https://restful-booker.herokuapp.com/booking`.
4. Selecionar **Body → raw → JSON** e inserir o JSON de criação apresentado nos dados de teste.
5. Clicar em **Send**.
6. Verificar se o POST retornou `200 OK` e guardar o `bookingid` da reserva criada.
7. Criar uma requisição utilizando o método `DELETE`.
8. Informar a URL `https://restful-booker.herokuapp.com/booking/{id}`, substituindo `{id}` pelo identificador retornado no POST.
9. Na aba **Headers**, configurar o cabeçalho `Authorization` com credenciais válidas utilizando o esquema `Basic Auth`.
10. Clicar em **Send**.
11. Verificar se o DELETE retornou `201 Created`, com o corpo `Created`.
12. Criar uma requisição utilizando o método `GET`.
13. Informar a URL `https://restful-booker.herokuapp.com/booking/{id}`, utilizando o mesmo identificador.
14. Clicar em **Send**.
15. Verificar se a API retornou `404 Not Found` e não apresentou dados da reserva excluída.


### Resultado esperado

A API deve excluir a reserva e retornar `201 Created`, com o corpo da resposta `Created`.

Uma consulta posterior pelo mesmo identificador deve retornar `404 Not Found`, com o corpo `Not Found`, sem apresentar os dados da reserva excluída.


### Resultado obtido

A reserva foi criada com o identificador `3003`.

A requisição `DELETE /booking/3003` retornou `201 Created`, com o corpo da resposta `Created`.

A consulta posterior `GET /booking/3003` retornou `404 Not Found`, com o corpo `Not Found`.

### Evidências

- [CT-05 - Criação da reserva](evidências/CT-05%20Criando%20Reserva.png)
- [CT-05 - Exclusão da reserva](evidências/CT-05%20Excluindo%20Reserva.png)
- [CT-05 - Validação da exclusão](evidências/CT-05%20Validando%20Reserva%20Excluída.png)
