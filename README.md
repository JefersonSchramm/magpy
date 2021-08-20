<p align="center"><img src="https://i.postimg.cc/brS990LC/magpy-logo.png"></p>

-----

MagPy é uma API RestFull desenvolvida utilizando a linguagem Python. A ferramenta foi criada para garantir que todos seus projetos em Python estejam usando as últimas versões
disponíves dos pacotes. A ferramenta recebe um nome de projeto, uma lista de pacotes e devolve a 
última versão de cada pacote.

A ferramenta utiliza como base de dados a 
[API pública do PyPI](https://warehouse.readthedocs.io/api-reference/json.html)
para verificar as últimas atualizações dos pacotes.

## Destaques

- Verifica a existência dos pacotes, e
- Garante que os pacotes estejam sempre atualizados


## 📃 API

Todos os endpoints ativos estão na URL https://magpyschramm.herokuapp.com/api e seguem a arquitetura REST.

Todas as requisições devem ser codificadas como JSON com o cabeçalho `Content-Type: application/json`. A maioria das respostas, incluindo erros, também é codificada exclusivamente como JSON.

> 🔥 A documentação da API pode ser encontrada no link abaixo
> 
> [API Docs](https://magpyschramm.herokuapp.com/api)

### Testando a API
Um arquivo `Tests.py` está disponível neste repositório. Ele irá executar uma sequência de requests para testar os retorno da API.

-----
Abaixo, alguns exemplos de chamadas que podem ser feitas nessa API:
## POST /projects
**Cria o projeto e seus pacotes**
<p>Estrutura do objeto:</p>

```json
{
    "name": "titan",
    "packages": [
        {"name": "Django"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```
O código HTTP de retorno deve ser `201` e o corpo esperado na resposta é:
```json
{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.6"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```

Se um dos pacotes informados não existir, ou uma das versões especificadas for
inválida, retornará o código HTTP `400` e o corpo abaixo:
```json
{
    "error": "One or more packages doesn't exist"
}
```

## GET /projects
**Lista todos os projetos e seus pacotes**

O código HTTP de retorno deve ser `200` e o corpo esperado na resposta é:
```json
[
  {
    "name": "titan",
    "packages": [
      {
        "name": "django-rest-swagger",
        "version": "2.2.0"
      },
      {
        "name": "Django",
        "version": "2.2.24"
      },
      {
        "name": "psycopg2-binary",
        "version": "2.9.1"
      }
    ]
  },
  {
    "name": "zeus",
    "packages": [
      {
        "name": "pytz",
        "version": "2021.1"
      },
      {
        "name": "requests",
        "version": "2.26.0"
      }
    ]
  }
]
```

## GET /projects/{name}/
**Lista o projeto informado e todos os seus pacotes**

O código HTTP de retorno deve ser `200` e o corpo esperado na resposta é:
```json

{
  "name": "zeus",
  "packages": [
    {
      "name": "pytz",
      "version": "2021.1"
    },
    {
      "name": "requests",
      "version": "2.26.0"
    }
  ]
}
```

## PUT /projects/{name}
**Atualiza o nome e todos os pacotes do projeto informado**

<p>Estrutura do objeto:</p>

```json
{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.5"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```
O código HTTP de retorno deve ser `200` e o corpo esperado na resposta é:
```json
{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.5"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```

Se um dos pacotes informados não existir, ou uma das versões especificadas for
inválida, retornará o código HTTP `200` e o corpo abaixo:
```json
{
    "error": "One or more packages doesn't exist"
}
```

## PATCH /projects/{name}
**Atualiza o nome e todos os pacotes do projeto informado**

<p>Estrutura do objeto:</p>

```json
{
    "packages": [
        {"name": "Django"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```
O código HTTP de retorno deve ser `200` e o corpo esperado na resposta é:
```json
{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.6"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```

Se um dos pacotes informados não existir, ou uma das versões especificadas for
inválida, retornará o código HTTP `400` e o corpo abaixo:
```json
{
    "error": "One or more packages doesn't exist"
}
```

## DELETE /projects/{name}
**Deleta o projeto e seus pacotes**

O código HTTP de retorno deve ser `204`

-----
# Autor 😎
- #### Jeferson Eduardo Schramm

## License

MIT
