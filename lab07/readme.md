Recipes_WWEIA_FCID_0510 (Receita)
	- FCID_Code_Description (Ingrediente)
	- Food_Code_Description (Resultado da receita)
	- Cooking_Method_Description (como fazer)
	- Cooked_Status_Description (estado do ingrediente)

FCID_Code_Description (Ingrediente)
	- FCID_Cropgroup_Description(grupo/subgrupo alimentar)

Food_Code_Description (Resultado da receita)

commodity-profile (pesquisa de consumo)
	- Food_Code_Description (Resultado da receita)
	- FCID_Cropgroup_Description(grupo/subgrupo alimentar)

-----------------------------------------------------------------------------------------------------

- Resultado da receita (alimento)
	- código
	- descrição
- Ingrediente
	- código
	- descrição
- Grupo dos ingredientes
	- código
	- descrição

-----------------------------------------------------------------------------------------------------

Ingrediente    ->    Grupo dos ingredientes
	- quais os grupos e subgrupos de cada ingrediente

Ingrediente     ->   Resultado da receita
	- quais ingredientes participam de quais receitas

Grupo dos ingredientes     ->      Grupo dos ingredientes
	- quais subgrupos pertence a quais grupos

Ingrediente -> Ingrediente
	- ingredientes que aparecem na mesma receita

Resultado da receita  ->  Resultado da receita
	- receitas que tem os mesmos ingredientes

Resultado da receita  ->  Grupo dos ingredientes
	- quais os grupos/subgrupos dos ingredientes daquela receita

-----------------------------------------------------------------------------------------------------

1) Quais ingredientes são mais populares (aparecem em conjunto com diversos outros ingredientes)?

2)  Quais receitas usam os ingredientes mais comuns (ingredientes usados em muitas outras receitas)?

3) Quais são os grupos mais populares para fazer uma receita (no caso, os grupos que são mais conectados com receitas)?
	- acaba trazendo também quais os grupos mais populares para se fazer uma receita
