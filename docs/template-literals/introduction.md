---
id: introduction
title: Introdução
sidebar_label: Introdução
---

Template literals são literais string que permitem expressões embutidas. Podemos criar uma string interpolada, ou seja, misturar uma expressão com a string que vai ser avaliada e depois colocar ela entre pólos, ao invés de concatenar. Fazemos isso apenas abrindo um `${expressão}`

## O que pode ser feito?
Com o Template String é possível fazer simplesmente isso:

```javascript
{
    "name": "${flow.name}",
    "result": "${10 * 5 / 2}"
}
```

O template literals aceita qualquer expressão da linguagem selecionada na criação do Workspace, porém é possível durante a execução você executar funções em outra linguagem. Fazemos isso apenas abrindo um `$(linguagem){expressão}`

```javascript
{
    "result_python": "$(py){[product] for product in flow.products}",
    "result_javascript": "$(js){flow.products.map(function (product) { return product })}"
}
```

Uma observação importante é que você pode associar objetos, listas, classes, funções, etc, a uma chave em seu JSON

```javascript
{
    "list": "${['Porsche', 'Ferrari', 'Lamborghini', 'McLaren']}",
    "dict": "${{'name': 'Porsche', 'nationality': 'Austria'}}",
    "function": "${lambda a : a * 10}"
    "class": "${function.my_module.MyClass()}"
}
```