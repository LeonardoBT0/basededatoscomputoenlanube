# Agregacion en MongoDB (Freamwork)

## Metodos para realizar agregaciones simples 

- distinct(): Devueve valores no duplicados
- countDocuments(): Cuenta los documentos en una coleccion
- estimatedDocumentCount(): Cuenta de manera aproximada un periodo de tiempo


## Una agregacion pipeline consta de una o mas etapas (stage) que procesan documentos

1. Cada etapa realiza una operacion en los documentos de entreda. Por ejemplo, una fase puede filtrar documentos y calcular valores

2. Los documentos que se generan en una fase pasan a la siguiente 

3. Puede devolver resultados para grupos de documentos como totales, maximp, minimo, etc

### Se utiliza la clausula "aggregate"

- Existen una serie de operadores qaue se pueden utilizar par arealizar operaciones. Se tienen distintos tipos: etapa, de comparacion, booleanos, aritmeticos, de cadena,
etc.

## Metodos Simples: countDocuments() y distinct()

1. Contar los documentos de la coleccion libros

```Json
db.libros.countDocuments()
```

2. Contar los documentos de la editorial Terra

```Json
db.libros.countDocuments(
    {
        editorial: "Terra"
    }
)

db.libros.countDocuments(
    {
        editorial: {$eq:"Terra"}
    }
)
```

3. Seleccionar todos los libros mostrando solamente la editorial

```Json
db.libros.find(
    {},
    {_id:0,editorial:1}
)
```

4. Seleccionar todos las distintas editoriales

```Json
db.libros.distinct("editorial")
```

[Documentacion de Agregaciones](https://www.mongodb.com/docs/manual/aggregation/)

## $match. Un pipeline basica
# Tiene funciones de etapa

```Json
db.libros.aggregate(
    [
        {$match:{editorial:"Terra"}}
    ]
)
```

## $project. Inciar  y renombrar campos

```Json
db.libros.aggregate(
 [
    {
        $match:{editorial:"Terra"}
    },
    {
        $project:{
            _id:0,
            titulo:1,
            precio:1,
            NombreEditorial:"$editorial",
            editorial:1
            }
    }
 ]
)
```

# .sort Ordenacion

```Json
db.libros.aggregate(
 [
   {
     $sort:
       {
         precio: 1
       }
   }
 ]
)
```

## $group.Agrupaciones

Cuantos documentos hay por cada una de las editoriales

```Json
_id: "$editorial",
"Numeero Documentos":{
    $count: {}
}
```

Cuantos documentos hay por cada una de las editoriales por numero de documentos de manera descendente



-- Utilizando Mongo Atlas Base de Datos sample_airnb
-- Agrupar por tipo de propiedad, mostrando el numero de propiedades y el promedio de sus precios 

```Json
[
  {
    $group:
     
      {
        _id: "$property_type",
        Numero: {
          $count: {}
        },
        Media: {
          $avg: "$price"
        }
      }
  }
]
```

--Operadores $set y $unset

```Json
[
  {
    $group: {
      _id: "$property_type",
      Numero: {
        $count: {}
      },
      Media: {
        $avg: "$price"
      }
    }
  },
  {
    $set:
    
      {
        Media_total: {
          $trunc: "$Media"
        }
      }
  }
]
```


Operador $unset

```Json
[
  {
    $group: {
      _id: "$property_type",
      Numero: {
        $count: {}
      },
      Media: {
        $avg: "$price"
      }
    }
  },
  {
    $set: {
      Media_total: {
        $trunc: "$Media"
      }
    }
  },
  {
    $unset:
    
      ["Media","Media_total"]
  }
]
```


-- Creando nuevas colecciones utilizando el Operador $out
-- Debe ser el ultimo en la agregacion

```Json
{
  _id:0,
  price:1,
  name:1,
  room_type:1,
  caro:{
    $gt:["$price",300]
  },
  medio:{
    $and:[
      {$gte:["$price",100]},
      {$lte:["price",300]}
    ]
  },
  barato:{
    $lt :["price",100]
  }
}
```
- $cod - Devuelve valores segun una condicion ( es parecido a un operador ternario de un lenguaje de proogramacion)

```Json
{
  _id: 0,
  price: 1,
  name: 1,

  caro: {
    $cond: [
      { $gt: ["$price", 300] },
      "si",
      "no"
    ]
  },

  medio: {
    $cond: [
      { 
        $and: [
          { $gte: ["$price", 100] },
          { $lte: ["$price", 300] }
        ] 
      },
      "si",
      "no"
    ]
  },

  baratito: {
    $cond: [
      { $lt: ["$price", 100] },
      "si",
      "no"
    ]
  }
}
```

-Views 

```Json
db.createView("ganancias_libros","libros",
[
  {
    $match:
      {
        editorial: "Biblio"
      }
  },
  {
    $project: {
      _id: 0,
      titulo: 1,
      precio: 1,
      cantidad: 1,
      "Nombre de editorial": "editorial",
      "Total de ganancias": {
        $multiply: ["$precio", "$cantidad"]
      }
    }
  },
  {
    $sort:
      {
        "Total ganancias": -1
      }
  }
]
)

db["ganancias_libros"].find(
    {"Total de ganancias":{$lte:240}},
    {titulo:1,"Total de ganancias":1}
).sort({titulo:-1})  
```

```Json

```