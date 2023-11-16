### Quais os tipos de nós que vamos utilizar (e quais as suas propriedades)

```
- Resultado da receita (alimento)
	- código
	- descrição
- Ingrediente
	- código
	- descrição
- Grupo dos ingredientes
	- código
	- descrição
```


### Quais vão ser os tipos de areastas e o que queremos com elas

```
Ingrediente    =>    Grupo dos ingredientes
- Quais os grupos e subgrupos de cada ingrediente

Ingrediente    =>    Resultado da receita
- Quais ingredientes participam de quais receitas

Grupo dos ingredientes    =>    Grupo dos ingredientes
- Quais subgrupos pertence a quais grupos

Ingrediente    =>    Ingrediente
- Ingredientes que aparecem na mesma receita

Resultado da receita    =>    Resultado da receita
- Receitas que tem os mesmos ingredientes

Resultado da receita    =>    Grupo dos ingredientes
- Quais os grupos/subgrupos dos ingredientes daquela receita
```


### Perguntas para análise que 

```
1) Quais ingredientes são mais populares (aparecem em conjunto com diversos outros ingredientes)?

2) Quais receitas usam os ingredientes mais comuns (ingredientes usados em muitas outras receitas)?

3) Quais são os grupos mais populares para fazer uma receita (no caso, os grupos que são mais conectados com receitas)?
	- Acaba trazendo também quais os grupos mais populares para se fazer uma receita
```
