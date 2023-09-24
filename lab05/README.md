# Equipe Shrek

# Subgrupo DBSET

- Gabreil Gomes - 248287
- Paulo Santos - 248438
- Rodrigo de Barros - 272701

# Laboratório

[Link para o notebook com os resultados das consultas](https://github.com/PauloVictorSS/MC536-DBSET/blob/main/lab05/food-intake-analysis-advanced.ipynb)

## Questão 1:

Abaixo encontram-se as views referente a popularidade de todos os alimentos da base, a soma de consumo destes alimentos, as médias de consumo e as
médias de consumo relativo ao peso para cada alimento, bem como, a quantidade de vezes que um alimento aparece nas receitas, nessa ordem respectivamente.

```sql
CREATE VIEW Popularidade as (
SELECT FD.FCID_CODE, COUNT(I.FCID_CODE) as Popularidade
    FROM FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
    GROUP BY FD.FCID_CODE
)

CREATE VIEW Intake_Sum as (
SELECT FD.FCID_CODE, SUM(I.INTAKE) as Intake_Sum
    FROM FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
    GROUP BY FD.FCID_CODE
)

CREATE VIEW Intake_AVG as (
SELECT FD.FCID_CODE, AVG(I.INTAKE) as Intake_AVG
    FROM FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
    GROUP BY FD.FCID_CODE
)

CREATE VIEW Intake_AVG_BW as (
SELECT FD.FCID_CODE, AVG(I.INTAKE_BW) as Intake_AVG_BW
    FROM FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
    GROUP BY FD.FCID_CODE
)

CREATE VIEW Total_Recipes as (
SELECT FD.FCID_CODE, COUNT(R.FCID_CODE) as Total_Recipes
    FROM FCID_Description FD JOIN Recipes R ON R.FCID_CODE = FD.FCID_CODE
    GROUP BY FD.FCID_CODE
)
```

## Questão 2:

Com essa tabela pronta, podemos ver de prontidão que os alimentos com maior popularidade (pessoas que consomem ele) não são necessariamente os mais consumidos
em quantidade, muito menos os que têm maior média de consumo. Portanto, o termo popularidade pode variar de acordo com as propriedades analisadas, existem alimentos
consumidos por muitas pessoas, mas em quantidades pequenas, como o açúcar ou sal (em gramas), e existem outros consumidos por poucas pessoas, mas as que
consomem, consomem em grande quantidade.

```sql
SELECT FD.FCID_CODE, AVG(I.INTAKE) as Intake_AVG, SUM(I.INTAKE) as Intake_Sum, COUNT(I.FCID_CODE) as Popularidade
    FROM FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
    GROUP BY FD.FCID_CODE
    ORDER BY Popularidade Desc
```

## Questão 3:

Nessa questão 3, classificamos o grupo de pessoas que foram entrevistadas em três grupos: consomem leite abaixo da média, consomem leite
dentro da média e consomem leite acima da média. Poderiamos, por exemplo, criar views em cima dessas queries para ficar mais fácil a análise depois.
Podemos fazer esse tipo de classficação/grupo com qualquer alimento, nesse caso, só escolhemos um alimento bastante consumido, de forma arbitrária.

```sql
SELECT 
	I.SeqN, 
	AVG(I.INTAKE) as CONSUMO
FROM 
  FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
WHERE
  I.FCID_CODE = 3600222000
GROUP BY I.SeqN
HAVING 
	CONSUMO >= 0.8 * (
		SELECT AVG(I2.INTAKE)
		FROM FCID_Description FD2 JOIN Intake I2 ON I2.FCID_CODE = FD2.FCID_CODE
		WHERE FD2.FCID_CODE = 3600222000
		GROUP BY FD2.FCID_CODE
	) AND
	CONSUMO <= 1.2 * (
		SELECT AVG(I2.INTAKE)
		FROM FCID_Description FD2 JOIN Intake I2 ON I2.FCID_CODE = FD2.FCID_CODE
		WHERE FD2.FCID_CODE = 3600222000
		GROUP BY FD2.FCID_CODE
	)
```
```sql
SELECT 
	I.SeqN, 
	AVG(I.INTAKE) as CONSUMO
FROM 
  FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
WHERE
  I.FCID_CODE = 3600222000
GROUP BY I.SeqN
HAVING 
	CONSUMO < 0.8 * (
		SELECT AVG(I2.INTAKE)
		FROM FCID_Description FD2 JOIN Intake I2 ON I2.FCID_CODE = FD2.FCID_CODE
		WHERE FD2.FCID_CODE = 3600222000
		GROUP BY FD2.FCID_CODE
	)
```
```sql
SELECT 
	I.SeqN, 
	AVG(I.INTAKE) as CONSUMO
FROM 
  FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
WHERE
  I.FCID_CODE = 3600222000
GROUP BY I.SeqN
HAVING 
	CONSUMO > 1.2 * (
		SELECT AVG(I2.INTAKE)
		FROM FCID_Description FD2 JOIN Intake I2 ON I2.FCID_CODE = FD2.FCID_CODE
		WHERE FD2.FCID_CODE = 3600222000
		GROUP BY FD2.FCID_CODE
	)
```

## Questão 4:

Nessa questão 4, mostramos só um exemplo de como relacionar grupos diferentes e tirar métricas disso. Nesse caso, temos o
grupo de pessoas que tem um consumo de leite acima da média e o grupo de pessoas que tem um consumo de vinagre acima da média.
Fizemos uma comparação para ver quais pessoas estão em um grupo, mas não estão em outro. De acordo com as quantidades, conseguimos 
tirar conclusões, por exemplo (não é factual com base nos dados): "a maioria das pessoas que tem um consumo acima da média em leite,
tem um consumo abaixo da média em vinagre, isso porque..."

```sql
CREATE VIEW MaiorLeite as (SELECT 
	I.SeqN, 
	AVG(I.INTAKE) as CONSUMO
FROM 
  FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
WHERE
  I.FCID_CODE = 3600222000
GROUP BY I.SeqN
HAVING 
	CONSUMO > 1.2 * (
		SELECT AVG(I2.INTAKE)
		FROM FCID_Description FD2 JOIN Intake I2 ON I2.FCID_CODE = FD2.FCID_CODE
		WHERE FD2.FCID_CODE = 3600222000
		GROUP BY FD2.FCID_CODE
	));
```
```sql
CREATE VIEW MaiorVinagre as 
(SELECT 
	I.SeqN, 
	AVG(I.INTAKE) as CONSUMO
FROM 
  FCID_Description FD JOIN Intake I ON I.FCID_CODE = FD.FCID_CODE
WHERE
  I.FCID_CODE = 9500390000
GROUP BY I.SeqN
HAVING 
	CONSUMO > 1.2 * (
		SELECT AVG(I2.INTAKE)
		FROM FCID_Description FD2 JOIN Intake I2 ON I2.FCID_CODE = FD2.FCID_CODE
		WHERE FD2.FCID_CODE = 3600222000
		GROUP BY FD2.FCID_CODE
	)
)
```
```sql
SELECT ML.SeqN 
    FROM MaiorLeite ML
    WHERE 
    ML.SeqN NOT IN (SELECT SeqN FROM MaiorVinagre)
```


