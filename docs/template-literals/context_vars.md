---
id: context_vars
title: Variáveis de contexto
sidebar_label: Variáveis de contexto
---

Durante a execução de uma expressão, é possível acessar algumas variáveis de contexto. Essas variáveis te permitem obter resultados de uma ação, invocar funções, acessar variáveis de ambiente, etc. Nas próximas sessões vamos ver as variáveis disponíveis e como cada uma funciona.

## flow

Você pode declarar varáveis utilizando a ação 'Flow var'. Para acessar essas variáveis você deve usar a seguinte expressão `${flow.nome_da_variável}`. Veja o seguinte exemplo:

```javascript
{
    "name": "${flow.name}"
}
```

## workspace

Você pode declarar varáveis utilizando a ação 'Workspace var'. Para acessar essas variáveis você deve usar a seguinte expressão `${workspace.nome_da_variável}`. Veja o seguinte exemplo:

```javascript
{
    "data": "${workspace.data}"
}
```

## env

No Flowyt é possível declarar variáveis de ambiente, para acessar essas variáveis você deve usar a seguinte expressão `${env.nome_da_variável}`. Veja o seguinte exemplo:

```javascript
{
    "url": "${env.base_url}"
}
```

## request

Você pode obter valores da request que iniciou o seu flow, para acessar essas variáveis você deve usar a seguinte expressão `${request.nome_da_variável}`. Os seguintes valores estão disponíveis para você acessar:

* headers
* params
* qs
* form
* data

Vamos supor que você construiu um workspace, publicou e agora está enviando a seguinte requisição para ele:

POST: `https://<subdomain>.engine.flowyt.com/<workspace>/loja/<string:loja>/livro?has_variants=true`

```
curl --request POST \
  --url https://livraria-marcus.engine.flowyt.com/controle-estoque/loja/BH/livro?has_variants=true \
  --header 'accept: application/json' \
  --header 'content-type: application/json' \
  --header 'x-flowyt-debug: false' \
  --data '{
    "name": "O pequeno príncipe",
    "description": "Le Petit Prince , o Pequeno Príncipe, era um garoto baixo e com cabelos cor de ouro, possuía uma personalidade simpática e muito gentil. Esse menino vive em um asteroide e sua única companhia é uma Rosa."
  }'
```

Você poderia por exemplo pegar os dados que vem do body da requisição da seguinte forma:

```javascript
{
    "name": "${request.data.name}",
    "description": "${request.data.description}"
}
```

Da mesma forma, você poderia querer pegar uma query string (qs), e o parâmetro da url `<string:loja>`

```javascript
{
    "has_variants": "${request.qs.has_variants}",
    "loja": "${request.params.loja}"
}
```

Geralmente os headers tem uma estrutura de nomeação, onde a primeira letra de cada palavra é maiuscula e as palavras são separadas por hífen, veja o exemplo do `Content-Type`, para que você consiga pegar esse valor da requisição, você deve deixar todas as letras minúsculas e substituir o hífen por underline, veja o exemplo:

```javascript
{
    "content": "${request.headers.content_type}"
}
```

## function

Quando a complexidade do seu fluxo começa a aumentar é natural se fazer necessário o uso de funções, essas funções podem ser acessadas com a seguinte expressão `${functions.nome_do_modulo.nome_da_função}`. Veja o exemplo:

```javascript
{
    "avg": "${functions.util.calc_avg(flow.data)}"
}
```

## response

Algumas ações elas produzem algum resultado, por exemplo a ação `Request` após ela ser executada, ela adiciona o resultado da requisição dentro da variável de contexto `response`, porém cada ação produz seu próprio resultado tornando assim os valores acessados no `response` dinâmicos. No caso da ação `Request`, você poderia acessar os dados da request utilizando a seguinte expressão `${response.data}`. Veja outro exemplo:

```javascript
{
    "status": "${response.status}",
    "data": "${response.data}"
}
```

## workspace_info

Em alguns momentos algumas informações do workspace podem ser úteis, por isso você pode usar a variável de contexto `workspace_info` para recuperar as seguintes informações:

* id
* name
* debug
* release: id, name
* safe_mode: active, safe_time

Esses dados podem ser acessadas com a seguinte expressão `${workspace_info.nome_da_variável}`. Veja o exemplo:

```javascript
{
    "release_id": "${workspace_info.release.id}",
    "workspace_name": "${workspace_info.name}"
}
```
