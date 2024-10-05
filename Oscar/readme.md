<br> 1- Quantas vezes Natalie Portman foi indicada ao Oscar? </br>
```
> db["Oscar"].countDocuments({nome_do_indicado: /Natalie Portman/})
< 3
```

<br> 2- Quantos Oscars Natalie Portman ganhou? </br>
```
> db["Oscar"].countDocuments({nome_do_indicado: /Natalie Portman/, vencedor: "true"})
< 1
```

<br> 3- Amy Adams já ganhou algum Oscar? </br>
```
> db["Oscar"].countDocuments({nome_do_indicado: /Amy Adams/, vencedor: "true"})
< 0
```

<br> 4- A série de filmes Toy Story ganhou um Oscar em quais anos? </br>
```
> db["Oscar"].distinct("ano_cerimonia", {nome_do_filme: /Toy Story/, vencedor: "true"})
< [2011, 2020]
```

<br> 5- A partir de que ano que a categoria "Actress" deixa de existir? </br>
```
> db.Oscar.find({categoria: 'ACTRESS'}, {ano_cerimonia: 1, categoria: 1, _id: 0}).sort({
    ano_cerimonia: -1
    }).limit(1)

< {
  ano_cerimonia: 1976,
  categoria: 'ACTRESS'
}
```

<br> 6- O primeiro Oscar para melhor Atriz foi para quem? Em que ano? </br>
```
> db.Oscar.find({categoria: "ACTRESS", vencedor: 'true'}, {ano_cerimonia: 1, categoria: 1, nome_do_indicado: 1}).limit(1)

< {
  _id: ObjectId('66ead2f6f3af78fe52ccfb37'),
  ano_cerimonia: 1928,
  categoria: 'ACTRESS',
  nome_do_indicado: 'Janet Gaynor'
}
```

<br> 7- Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0. </br>
```
> db.Oscar.updateMany(
{vencedor: "true"},
{ $set: {vencedor: 1 }}
)

db.Oscar.updateMany(
  {vencedor: "false"},
  {$set: {vencedor: 0 }}
)

< {
  acknowledged: true,
  insertedId: null,
  matchedCount: 8423,
  modifiedCount: 8423,
  upsertedCount: 0
}
```

<br> 8- Em qual edição do Oscar "Crash" concorreu ao Oscar? </br>
```
> db.Oscar.distinct('cerimonia', {nome_do_filme: "Crash"})
< [ 78 ]
```

<br> 9- Bom... dê um Oscar para um filme que merece muito, mas não ganhou. </br>
```
> db.Oscar.updateOne({vencedor: 1, ano_cerimonia: 2004}, {$set: {vencedor: 0}})
< {
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

> db.Oscar.updateOne({nome_do_filme: "City of God", ano_cerimonia: 2004}, {$set: {vencedor: 1}})
< {
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
<br> 10- O filme Central do Brasil aparece no Oscar? </br>
```
> db.Oscar.find({nome_do_filme: "Central Station"})

< {
  _id: ObjectId('66ead2f8f3af78fe52cd19a6'),
  id_registro: 7795,
  ano_filmagem: 1998,
  ano_cerimonia: 1999,
  cerimonia: 71,
  categoria: 'ACTRESS IN A LEADING ROLE',
  nome_do_indicado: 'Fernanda Montenegro',
  nome_do_filme: 'Central Station',
  vencedor: 0
}

{
  _id: ObjectId('66ead2f8f3af78fe52cd19d0'),
  id_registro: 7837,
  ano_filmagem: 1998,
  ano_cerimonia: 1999,
  cerimonia: 71,
  categoria: 'FOREIGN LANGUAGE FILM',
  nome_do_indicado: 'Brazil',
  nome_do_filme: 'Central Station',
  vencedor: 0
}
```

<br> 11- Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. </br>
```
> db.Oscar.insertMany([{
ano_filmagem: 2003,
ano_cerimonia: 2004,
cerimonia: 76,
categoria: "Best Picture",
nome_do_indicado: "Fernando Meirelles",
nome_do_filme: "Carandiru",
vencedor: 0
},
{
  ano_filmagem: 2007,
  ano_cerimonia: 2008,
  cerimonia: 80,
  categoria: "Best Picture",
  nome_do_indicado: "José Padilha",
  nome_do_filme: "Elite Squad",
  vencedor: 0
},
{
  ano_filmagem: 2015,
  ano_cerimonia: 2016,
  cerimonia: 88,
  categoria: "Best Picture",
  nome_do_indicado: "Anna Muylaert",
  nome_do_filme: "The Second Mother",
  vencedor: 0
}])

< {
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6701c142f07dc801e4e36557'),
    '1': ObjectId('6701c142f07dc801e4e36558'),
    '2': ObjectId('6701c142f07dc801e4e36559')
  }
}
``` 

<br> 12 - Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor? </br>
```
> db.Oscar.find({ano_cerimonia: 2001, vencedor: 1, categoria: { "$in": ["ACTRESS IN A LEADING ROLE", "BEST PICTURE", "DIRECTING"]}}, {categoria: 1, nome_do_indicado: 1, _id: 0})

< {
  categoria: 'ACTRESS IN A LEADING ROLE',
  nome_do_indicado: 'Julia Roberts'
}

{
  categoria: 'DIRECTING',
  nome_do_indicado: 'Steven Soderbergh'
}

{
  categoria: 'BEST PICTURE',
  nome_do_indicado: 'Douglas Wick, David Franzoni and Branko Lustig, Producers'
}
```