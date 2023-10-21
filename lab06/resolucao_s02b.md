## Exercício

Faça a projeção em relação a Patologia, ou seja, conecte patologias que são tratadas pela mesma droga.

### Resolução
```cypher
MATCH (d1:Drug)-[]->(p1:Pathology)
MATCH (d2:Drug)-[]->(p2:Pathology)
WHERE d1 = d2
MERGE (p1)<-[r:IsTreated]->(p2)
ON CREATE SET r.weight=1
ON MATCH SET r.weight=r.weight+1
```

## Exercício

Construa um grafo ligando os medicamentos aos efeitos colaterais (com pesos associados) a partir dos registros das pessoas, ou seja, se uma pessoa usa um medicamento e ela teve um efeito colateral, o medicamento deve ser ligado ao efeito colateral.

### Resolução
```cypher
# Para criar Person: id unico
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' AS p
MERGE (:Person {id: p.idperson})

# Para criar Drugs: Code unico
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' AS p
MERGE (d:Drug {code: p.codedrug});

# Para criar SideEffect: Code unico
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' AS p
MERGE (d:SideEffects {code: p.codePathology});

# Ligando drugs com person (OFICIAL):
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' AS line
MATCH (p:Person { id: line.idperson })
MATCH (d:Drug { code: line.codedrug })
MERGE (d)-[t:Treats]->(p)
ON CREATE SET t.weight=1
ON MATCH SET t.weight=t.weight+1

# Ligando sides effects com person:
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' AS line
MATCH (p:Person { id: line.idPerson })
MATCH (s:SideEffects { code: line.codePathology })
MERGE (s)-[t:Occurs]->(p)
ON CREATE SET t.weight=1
ON MATCH SET t.weight=t.weight+1

# Conectando sides effects com drugs:
MATCH (d:Drug)-[a]->(p:Person)<-[b]-(s:SideEffects)
MERGE (d)<-[r:Relates]->(s)
ON CREATE SET r.weight=1
ON MATCH SET r.weight=r.weight+1
```

## Exercício

Que tipo de análise interessante pode ser feita com esse grafo?

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução
```cypher
# Listagem das drogas com mais efeitos colaterais:
MATCH (d)-[t:Relates]->(p)
WHERE t.weight > 20
RETURN d,t,p
```
