# MongoDB-Eleicoes
Schema Lógico e Físico de Banco de Dados NOSQL MongoDB para apuração de votos em Eleição Municipal de SP

Foram criadas **6 Collections** para organização dos dados, sendo elas:

- **Localidade**: registra o estado, cidade, zona, seção e UF
- **Candidato**: contém dados dos candidatos: número do candidato, nome, cargo ao qual está concorrendo e número do partido
- **Partido**: armazena o número, nome e sigla do partido
- **Eleitor**: contém dados dos eleitores: número do título de eleitor, nome, número da seção e da zona de voto
- **Votos_secao_candidato**: Total de votos parcial dos candidatos por seção específica
- **Resultado**: Resultado da eleição (prefeito e vereador) no município com total de votos

**Modelagem Lógica**

![schema_mongo](https://user-images.githubusercontent.com/64870434/90268668-c4827500-de2d-11ea-8b0d-1e5d0198e7ac.png)


**Modelagem Física**

**1. Criando o Banco de Dados**

```
use DBEleicoes;
```
**1.1. Criando uma Collection com dado de um eleitor e um candidato para que o database DBEleicoes persista no banco de dados MongoDB**

```
db.eleitor.insertOne(
						{
							num_titulo_eleitor: 1111,
							nom_eleitor: "Pedro Souza",
							num_secao: 10,
							num_zona: 101
						}
);

db.candidato.insertOne(
						{
							num_candidato: 10,
							nom_candidato: "Antonio Virgilio",
							num_partido: 201,
							nom_cargo: "prefeito"
						}
);

db.partido.insertOne(
						{
							num_partido: 201,
							nom_partido: "Partido 01",
							sgl_partido: "P1"
						}
);
```
**. Retorno das querys**
```
{
	"acknowledged" : true,
	"insertedId" : ObjectId("5f36a78d2b58483f862a88b2")
}
{
	"acknowledged" : true,
	"insertedId" : ObjectId("5f36a7ab2b58483f862a88b3")
}
{
	"acknowledged" : true,
	"insertedId" : ObjectId("5f36a7bf2b58483f862a88b4")
}
```
**1.2. Inserindo vários documentos/dados de uma só vez na Collection com o comando insertMany**
```
db.eleitor.insertMany([
						{
							num_titulo_eleitor: 1112,
							nom_eleitor: "Paula Andrade",
							num_secao: 12,
							num_zona: 102
						},
{
							num_titulo_eleitor: 1113,
							nom_eleitor: "Joao Gabriel",
							num_secao: 13,
							num_zona: 103
						},
{
							num_titulo_eleitor: 1114,
							nom_eleitor: "Gabriela Zup",
							num_secao: 14,
							num_zona: 104
						},
{
							num_titulo_eleitor: 1115,
							nom_eleitor: "Maria Eduarda",
							num_secao: 15,
							num_zona: 105
						},
{
							num_titulo_eleitor: 1115,
							nom_eleitor: "Antonio Santos",
							num_secao: 15,
							num_zona: 105
						},
{
							num_titulo_eleitor: 1115,
							nom_eleitor: "Silvana Mendes",
							num_secao: 15,
							num_zona: 105
						}
]);
```

**. Retorno da Collection Eleitor**
```
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("5f36a80e2b58483f862a88b6"),
		ObjectId("5f36a80e2b58483f862a88b7"),
		ObjectId("5f36a80e2b58483f862a88b8"),
		ObjectId("5f36a80e2b58483f862a88b9"),
		ObjectId("5f36a80e2b58483f862a88ba"),
		ObjectId("5f36a80e2b58483f862a88bb")
	]
}
```

**1.3. Inserção das outras Collections**

**. Collection Candidato**
```
db.candidato.insertMany([
							{
								num_candidato: 20, 
								nom_candidato: "Patricia Alves",
								num_partido: 202,
								nom_cargo: "prefeito"
							},
							{
								num_candidato: 30, 
								nom_candidato: "Guilherme Arrais",
								num_partido: 203,
								nom_cargo: "prefeito"
							},
							{
								num_candidato: 4545, 
								nom_candidato: "Gabriela Bual",
								num_partido: 204,
								nom_cargo: "vereador"
							},
								{
								num_candidato: 3233, 
								nom_candidato: "Ana Flavia",
								num_partido: 203,
								nom_cargo: "vereador"
							},
							{
								num_candidato: 2252, 
								nom_candidato: "Gilmar Duth",
								num_partido: 202,
								nom_cargo: "vereador"
							}]
);
```

**. Collection Partido**

```
db.partido.insertMany([
						{
							num_partido: 202,
							nom_partido: "Partido 02",
							sgl_partido: "P2"
						},
						{
							num_partido: 203,
							nom_partido: "Partido 03",
							sgl_partido: "P3"
						},
						{
							num_partido: 204,
							nom_partido: "Partido 04",
							sgl_partido: "P4"
						},

]);
```
**. Collection Voto_secao_candidato que mostra o total de votos por candidato em uma determinada Seção**

```
db.voto_secao_candidato.insertMany([
						{
							nom_candidato: "Patricia Alves",
							num_candidato: 20, 
							cargo: "prefeito",
							num_partido: 202,
							num_secao: 12,
							num_zona: 102,
							qtd_total_votos: 81000
						},
						{
							nom_candidato: "Guilherme Arrais",
							num_candidato: 30, 
							cargo: "prefeito",
							num_partido: 203,
							num_secao: 12,
							num_zona: 102,
							qtd_total_votos: 12000
						},
						{
							nom_candidato: "Gabriela Bual",
							num_candidato: 4545, 
							cargo: "vereador",
							num_partido: 204,
							num_secao: 12,
							num_zona: 102,
							qtd_total_votos: 5000
						},
						{
							nom_candidato: "Ana Flavia",
							num_candidato: 3233, 
							cargo: "vereador",
							num_partido: 203,
							num_secao: 14,
							num_zona: 104,
							qtd_total_votos: 1580
						},
						{
							nom_candidato: "Gilmar Duth",
							num_candidato: 2252, 
							cargo: "vereador",
							num_partido: 202,
							num_secao: 14,
							num_zona: 104,
							qtd_total_votos: 5172
						}
]);
```
**. Collection Localidade**
```
db.localidade.insertMany([
						{
							nom_cidade: "São Paulo",
							nom_estado: "São Paulo",
							sgl_uf: "SP",
							num_secao: 12,
							num_zona: 102
						},
						{
							nom_cidade: "São Paulo",
							nom_estado: "São Paulo",
							sgl_uf: "SP",
							num_secao: 13,
							num_zona: 103
						},
						{
							nom_cidade: "São Paulo",
							nom_estado: "São Paulo",
							sgl_uf: "SP",
							num_secao: 14,
							num_zona: 104
						},
						{
							nom_cidade: "São Paulo",
							nom_estado: "São Paulo",
							sgl_uf: "SP",
							num_secao: 15,
							num_zona: 105
						}
]);
```

**. Collection Localidade: Exibe o resultado final das eleições municipais com os cargos de prefeito e vereadores eleitos**
```
db.resultado.insertMany([
						{
							nom_candidato: "Patricia Alves",
							num_candidato: 20,
							cargo: "prefeito",
							num_partido: 202,
							qtd_final_votos: 101020
						},
						{
							nom_candidato: "Gabriela Bual",
							num_candidato: 4545,
							cargo: "vereador",
							num_partido: 204,
							qtd_final_votos: 32000
						},
						{
							nom_candidato: "Gilmar Duth",
							num_candidato: 2252,
							cargo: "vereador",
							num_partido: 202,
							qtd_final_votos: 27450
						}
]);
```
**2. Verificando se as inserções de dados estão corretas**


**2.1. Registros de Candidatos**


![3 verificando_candidatos](https://user-images.githubusercontent.com/64870434/90268895-204cfe00-de2e-11ea-98d3-6b090e304498.png)


**2.2. Registros de Eleitores**


![4 verificando_eleitores](https://user-images.githubusercontent.com/64870434/90268975-3fe42680-de2e-11ea-8563-b7011b1e9c58.png)


**3. Lista trazendo apenas o Nome do Candidato e o Cargo. Existem duas formas de exibir os dados no MongoDB:**



**3.1. Não organizada**, usando apenas o comando **find()** conforme abaixo:


```
> db.candidato.find({},{"nom_candidato": 1, "nom_cargo": 1});


{ "_id" : ObjectId("5f36a7ab2b58483f862a88b3"), "nom_candidato" : "Antonio Virgilio", "nom_cargo" : "prefeito" }
{ "_id" : ObjectId("5f36a8232b58483f862a88bc"), "nom_candidato" : "Patricia Alves", "nom_cargo" : "prefeito" }
{ "_id" : ObjectId("5f36a8232b58483f862a88bd"), "nom_candidato" : "Guilherme Arrais", "nom_cargo" : "prefeito" }
{ "_id" : ObjectId("5f36a8232b58483f862a88be"), "nom_candidato" : "Gabriela Bual", "nom_cargo" : "vereador" }
{ "_id" : ObjectId("5f36a8232b58483f862a88bf"), "nom_candidato" : "Ana Flavia", "nom_cargo" : "vereador" }
{ "_id" : ObjectId("5f36a8232b58483f862a88c0"), "nom_candidato" : "Gilmar Duth", "nom_cargo" : "vereador" }

```

**3.2. Organizada** com o comando **pretty()**, sendo exibida no **formato do arquivo JSON padrão** para que seja exibida assim, conforme abaixo:

```
> db.candidato.find({},{"nom_candidato": 1, "nom_cargo": 1}).pretty();


{
	"_id" : ObjectId("5f36a7ab2b58483f862a88b3"),
	"nom_candidato" : "Antonio Virgilio",
	"nom_cargo" : "prefeito"
}
{
	"_id" : ObjectId("5f36a8232b58483f862a88bc"),
	"nom_candidato" : "Patricia Alves",
	"nom_cargo" : "prefeito"
}
{
	"_id" : ObjectId("5f36a8232b58483f862a88bd"),
	"nom_candidato" : "Guilherme Arrais",
	"nom_cargo" : "prefeito"
}
{
	"_id" : ObjectId("5f36a8232b58483f862a88be"),
	"nom_candidato" : "Gabriela Bual",
	"nom_cargo" : "vereador"
}
{
	"_id" : ObjectId("5f36a8232b58483f862a88bf"),
	"nom_candidato" : "Ana Flavia",
	"nom_cargo" : "vereador"
}
{
	"_id" : ObjectId("5f36a8232b58483f862a88c0"),
	"nom_candidato" : "Gilmar Duth",
	"nom_cargo" : "vereador"
}
```


**4. Script DML de atualização do campo com "total_votos" da Collection "secao_candidato"**

```
db.voto_secao_candidato.updateOne(
							{ num_candidato: {$eq: 4545 } },
							{ $set: { "qtd_total_votos": 12562 } }
							);
```

**4.2. Query ok!**
```
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

**4.3. Verificando alteração: Trazendo apenas o candidato que teve o Total de Votos alterado através do comando de comparação e "$eq"**

```
db.voto_secao_candidato.find( { num_candidato: {$eq: 4545 } }).pretty();
```

**4.4.Retorno**

```
{
	"_id" : ObjectId("5f36aa6e01c0c5cb5298b789"),
	"nom_candidato" : "Gabriela Bual",
	"num_candidato" : 4545,
	"cargo" : "vereador",
	"num_partido" : 204,
	"num_secao" : 12,
	"num_zona" : 102,
	"qtd_total_votos" : 12562
}
```

**5. Apagando um Candidato específico da Collection**

```
db.candidato.deleteOne(	{ nom_candidato : {$eq: "Antonio Virgilio" } } );
```

**5.1. Retorno do DB** Candidato deletado não consta mais na base
```
{ "acknowledged" : true, "deletedCount" : 1 }
```

![7 drop_candidato](https://user-images.githubusercontent.com/64870434/90269007-4ffc0600-de2e-11ea-93b8-d3fe520f0ad7.png)
