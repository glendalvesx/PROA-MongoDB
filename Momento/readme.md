<h1>ATIVIDADE: MOMENTO</h1>

<br> 1. Quantos funcionarios da empresa Momento trabalham no departamento de vendas? </br>
```
> db.funcionarios.countDocuments({departamento: ObjectId('85992103f9b3e0b3b3c1fe71')})
< 10
```

<br> 2. Inclua suas próprias informações no departamento de Tecnologia da empresa.</br>
```
> db.funcionarios.insertOne({
  nome: 'Glenda Alves',
  telefone: '11900000000',
  email: 'glenda.asantos1@gmail.com',
  dataAdmissao: '2024-09-23',
  cargo: 'Desenvolvedor(a) Mobile Kotlin',
  salario: 4500,
  departamento: ObjectId('85992103f9b3e0b3b3c1fe74'),
  comissionado: true
})

< {
    acknowledged: true,
    insertedId:ObjectId('66f190e5cf7a3d0a163c7709')
}
```

<br> 3. Agora diga, quantos funcionários temos ao total na empresa?. </br>
```
> db.funcionarios.countDocuments({})
< 24
```

<br> 4. E quanto ao Departamento de Tecnologia? </br>
```
> db.funcionarios.countDocuments({departamento: ObjectId('85992103f9b3e0b3b3c1fe74')})
< 6
```

<br> 5. Qual a média salarial do departamento de tecnologia? </br>
```
> db.funcionarios.aggregate([
{
   $match: {departamento: ObjectId('85992103f9b3e0b3b3c1fe74')}
},

{ 
   $group: {
   _id: null,
   mediaSalarial: {$avg: "$salario"}
}

}
])

< {
  _id: null,
  mediaSalarial: 4550
}
```

<br> 6. Quanto o departamento de Vendas gasta em salários? </br>
```
> db.funcionarios.aggregate([
{
   $match: {departamento: ObjectId('85992103f9b3e0b3b3c1fe71')}
},
{
   $group: {
   _id: null,
   totalSalarios: {$sum: "$salario"}
}
}
])

< {
  _id: null,
  totalSalarios: 95100
}
```

<br> 7. Um novo departamento foi criado. O departamento de Inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes. </br>

<h4>Primeiro devemos criar o Escritório no Brasil (que até o momento não existia): </h4>

```
> db.escritorios.insertOne({
nome: "Inovações",
endereco: "R. Tito, 54 - Vila Romana, São Paulo - SP, 05051-000",
telefone: "+55 11 91234-5678",
pais: "BR"
})

< {
  acknowledged: true,
  insertedId: ObjectId('66f1e590cf7a3d0a163c770a')
}
```

<h4>Escritório criado, agora devemos criar o departamento Inovações inserindo o ID do Escritório no Brasil </h4>

```
> db.departamentos.insertOne({
nome: "Inovações",
escritorio: ObjectId('66f1e590cf7a3d0a163c770a')
})

< {
  acknowledged: true,
  insertedId: ObjectId('66f1e775cf7a3d0a163c770b')
}
```

<br> 8. O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento. </br>
```
> db.funcionarios.insertMany([
  {
    nome: "Alice Santos",
    telefone: "+55 11 99876-5432",
    cargo: "Gerente de Inovações",
    salario: 12000,
    departamento: ObjectId('66f1e775cf7a3d0a163c770b')
  },
  {
    nome: "Bruno Oliveira",
    telefone: "+55 11 98765-4321",
    cargo: "Desenvolvedor de Produto",
    salario: 9000,
    departamento: ObjectId('66f1e775cf7a3d0a163c770b')
  },
  {
    nome: "Carla Pereira",
    telefone: "+55 11 97654-3210",
    cargo: "Analista de Pesquisa",
    salario: 8000,
    departamento: ObjectId('66f1e775cf7a3d0a163c770b')
  },
  {
    nome: "Daniel Costa",
    telefone: "+55 11 96543-2109",
    cargo: "Designer de UX",
    salario: 7500,
    departamento: ObjectId('66f1e775cf7a3d0a163c770b')
  },
  {
    nome: "Eduardo Almeida",
    telefone: "+55 11 95432-1098",
    cargo: "Engenheiro de Software",
    salario: 11000,
    departamento: ObjectId('66f1e775cf7a3d0a163c770b')
  },
  {
    nome: "Fernanda Lima",
    telefone: "+55 11 94321-0987",
    cargo: "Coordenadora de Projetos",
    salario: 9500,
    departamento: ObjectId('66f1e775cf7a3d0a163c770b')
  }
])

< {
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('66f1eb43cf7a3d0a163c770c'),
    '1': ObjectId('66f1eb43cf7a3d0a163c770d'),
    '2': ObjectId('66f1eb43cf7a3d0a163c770e'),
    '3': ObjectId('66f1eb43cf7a3d0a163c770f'),
    '4': ObjectId('66f1eb43cf7a3d0a163c7710'),
    '5': ObjectId('66f1eb43cf7a3d0a163c7711')
  }
}
```

<br> 9. Quantos funcionarios a empresa Momento tem agora? </br>
```
> db.funcionarios.countDocuments({})
< 30
```

<br> 10. Quantos funcionários da empresa Momento possuem conjuges? </br>
```
> db.funcionarios.countDocuments({"dependentes.conjuge": {$exists: true}})
< 7
```

<br> 11. Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO? </br>
```
> db.funcionarios.aggregate([
{
    $match: {
     cargo: { $ne: "CEO"}
}
},
{
   $group: {
   _id: null,
   mediaSalarial: { $avg: "$salario"}
   
}
}
])

< {
  _id: null,
  mediaSalarial: 9523.448275862069
}
```

<br> 12. Qual a média salarial do departamento de tecnologia? </br>
```
> db.funcionarios.aggregate([
{
      $match: {
      departamento: ObjectId("85992103f9b3e0b3b3c1fe74")
}
},
{
       $group: {
       _id: null,
       mediaSalarial: {$avg: "$salario"}

}
}
])

< {
  _id: null,
  mediaSalarial: 4550
}
```

<br> 13. Qual o departamento com a maior média salarial? </br>
```
> db.funcionarios.aggregate([
  {
    $group: {
      _id: "$departamento",
      mediaSalarial: { $avg: "$salario" }
    }
  },
  {
    $sort: { mediaSalarial: -1 }
  },
  {
    $limit: 1
  },
   {
        $lookup: {
            from: "departamentos",  
            localField: "_id", 
            foreignField: "_id",  
            as: "departamentoInfo"  
        }
    },
    {
        $unwind: "$departamentoInfo"  
    },
    {
        $project: {
            _id: 0,  
            departamento: "$departamentoInfo.nome",  
            mediaSalarial: 1
        }
    }
])

<{
  mediaSalarial: 71000,
  departamento: 'Executivo'
}
```

<br> 14. Qual o departamento com o menor número de funcionários? </br>
```
> db.funcionarios.aggregate([
  {
    $group: {
      _id: "$departamento",
      numeroFuncionarios: { $sum: 1 }
    }
  },
  {
    $sort: { numeroFuncionarios: 1 } 
  },
  {
    $limit: 1
  },
{
        $lookup: {
            from: "departamentos", 
            localField: "_id", 
            foreignField: "_id", 
            as: "departamentoInfo"  
        }
    },
    {
        $unwind: "$departamentoInfo"  
    },
    {
        $project: {
            _id: 0,  
            departamento: "$departamentoInfo.nome",  
            numeroFuncionarios: 1  
        }
    }
])

< {
  numeroFuncionarios: 1,
  departamento: 'Executivo'
}

```

<br> 15. Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa? </br>
```
> db.vendas.aggregate([
{ 
   $group: {
    _id:"$produto", total: {$sum: {$multiply: ["$precoUnitario", "$quantidade"]}}
}
},
{
    $sort: {total: -1}
},
{
     $limit: 1
}
])

< {
  _id: 'Sabre de Luz (Mace Windu)',
  total: 7922.32
}
```

<br> 16. Qual o produto mais vendido da empresa? </br>
```
> db.vendas.aggregate([
  {
    $group: {
      _id: "$produto",
      totalVendido: { $sum: "$quantidade" }
    }
  },
  {
    $sort: { totalVendido: -1 }
  },
  {
    $limit: 1
  }
])

< {
  _id: 'Laço da Verdade',
  totalVendido: 12
}
```

<br> 17. Qual o produto menos vendido da empresa? </br>
```
> db.vendas.aggregate([
  {
    $group: {
      _id: "$produto", // Agrupa por produto
      totalVendido: { $sum: "$quantidade" } // Soma a quantidade vendida de cada produto
    }
  },
  {
    $sort: { totalVendido: 1 } // Ordena pelo total vendido em ordem decrescente
  },
  {
    $limit: 1 // Limita o resultado ao produto mais vendido
  }
])

< {
  _id: 'Fake Batarang',
  totalVendido: 2
}
```
