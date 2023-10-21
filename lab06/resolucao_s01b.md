## Exercício

Escreva uma sentença em Cypher que crie o medicamento de nome `Metamizole`, código no DrugBank `DB04817`.

### Resolução
~~~cypher
CREATE (:Drug {drugbank: "DB04817", name: "Metamizole"})
~~~



## Exercício

Considerando que a `Dipyrone` e `Metamizole` são o mesmo medicamento com nomes diferentes, crie uma aresta com o rótulo `:SameAs` que ligue os dois.

### Resolução
~~~cypher
MATCH (d:Drug {name:"Dipyrone"})
MATCH (p:Drug {name:"Metamizole"})
CREATE (d)-[:SameAs]->(p)
~~~



## Exercício

Use o `DELETE` para excluir o relacionamento que você criou (apenas ele).

### Resolução
~~~cypher
MATCH (d:Drug {name:"Dipyrone"})
MATCH (p:Drug {name:"Metamizole"})
MATCH (d)-[e]->(p)
DELETE e
~~~
