
# QA Lab 01 - Testes de API REST

## Sobre o projeto

Projeto prático de Quality Assurance voltado à execução e documentação de testes funcionais manuais em uma API REST.

O objetivo é aplicar conhecimentos de métodos HTTP, JSON, autenticação, validação de respostas e documentação de casos de teste.

## API utilizada

**Restful Booker**

API pública de testes que permite criar, consultar, atualizar e excluir reservas.

**Base URL:** https://restful-booker.herokuapp.com

**Documentação da API:** [API Docs](https://restful-booker.herokuapp.com/apidoc/index.html)

## Ferramentas e conhecimentos aplicados

- Postman
- API REST
- Métodos HTTP: GET, POST, PUT e DELETE
- JSON
- Basic Auth
- Testes funcionais positivos e negativos
- Documentação de testes e evidências

## Casos de teste

| ID | Cenário | Tipo | Resultado |
|---|---|---|---|
| CT-01 | Criar reserva com dados válidos | Positivo | Aprovado |
| CT-02 | Consultar reserva inexistente | Negativo | Aprovado |
| CT-03 | Atualizar reserva existente | Positivo | Aprovado |
| CT-04 | Impedir atualização sem autenticação | Negativo | Aprovado |
| CT-05 | Excluir reserva existente | Positivo | Aprovado |

**Total:** 5 casos de teste executados manualmente.

Nos cenários executados, os resultados observados corresponderam aos resultados esperados.

## Documentação e evidências

Os casos de teste contêm:

- Objetivo e classificação
- Pré-condições
- Dados de teste
- Passos para execução
- Resultado esperado
- Resultado obtido
- Evidências das requisições e respostas

[Consultar documentação dos casos de teste](casos-de-teste.md)

As capturas de tela estão disponíveis na pasta `evidências/`.


## Collection do Postman


[Consultar Collection do Postman](QA%20Lab%2001%20-%20Testes%20de%20API%20REST.postman_collection.json)

Para utilizar:
1. Importar a Collection no Postman.
2. Configurar as variáveis `booking_id`, `invalid_booking_id`, `basic_username` e `basic_password`, conforme o cenário.
3. Seguir os passos documentados em `casos-de-teste.md`.

Os testes são manuais e não possuem scripts automatizados de validação.

## Observações

- Os testes foram executados manualmente no Postman.
- Os identificadores das reservas apresentados na documentação correspondem às execuções realizadas.
- A Restful Booker é uma API pública de testes; seus dados podem ser redefinidos.
- Novas execuções podem gerar identificadores e resultados diferentes, dependendo do estado da API.
- Credenciais de autenticação não são disponibilizadas neste repositório.

## Objetivo profissional

Este projeto integra meus estudos de Quality Assurance e meu desenvolvimento prático para atuação como QA Júnior.
