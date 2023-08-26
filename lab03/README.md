# Equipe Shrek

# Subgrupo DBSET

- Gabreil Gomes - 248287
- Paulo Santos - 248438
- Rodrigo de Barros - 272701


## Modelo Relacional
~~~
Aluno(_ra_, nome, instituto, telefone)

Cardapio(_id_, descricao, data, tipoRefeicao)  

Porcao(_id_, quantidade, tipo)

CardapioPorcao(_id_, idCardapio, idPorcao)
  idCardapio chave estrangeira -> Cardapio(_id_)
  idPorcao chave estrangeira -> Porcao(_id_)

Escolhe(_id_, raAluno, idCardapioPorcao, data)
  raAluno chave estrangeira -> Aluno(_id_)
  idCardapioPorcao chave estrangeira -> CardapioPorcao(_id_)

Nutriente(_id_, descricao)

Ingrediente(_id_, nome)

CompoeIngrediente(_idIngredientePai_, _idIngredienteFilho_, quantidade)
  idIngredientePai chave estrangeira -> Ingrediente(_id_)
  idIngredienteFilho chave estrangeira -> Ingrediente(_id_)
	
NutrienteIngrediente(_idNutriente_, _idIngrediente_, valor)
  idNutriente chave estrangeira -> Nutriente(_id_)
  idIngrediente chave estrangeira -> Ingrediente(_id_)

PorcaoIngriente(_idPorcao_, _idIngrediente_)
  idPorcao chave estrangeira -> Porcao(_id_)
  idIngrediente chave estrangeira -> Ingrediente(_id_)

Classificacao(_id_, descricao)

ClassificacaoIngrediente(_idClassificacao_, _idIngrediente_)
  idClassificacao chave estrangeira -> Classificacao(_id_)
  idIngrediente chave estrangeira -> Ingrediente(_id_)

ClassificacaoCardapio(_idClassificacao_, _idCardapio_)
  idClassificacao chave estrangeira -> Classificacao(_id_)
  idCardapio chave estrangeira -> Cardapio(_id_)
~~~


