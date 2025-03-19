# Agregaciones

1. Para hacer esta práctica vamos a cargar unos datos ficticios de empresa.
2. Tienes un fichero denominado “productos.json”
3. Debes poner el resultado de las consultas en cada apartado
- Cuenta los productos de tipo “medio”, usando un método básico
```Json
db.productos.find(
    {tipo:'medio'}
).count()
```
**Resultados**
```Json
25
```
- Indicar con un distinct, las empresas (fabricantes) que hay en la colección
```Json
db.productos.distinct('fabricante')
```
**Resultados**
```Json
[
  'A.O. Smith',
  'Alere',
  'American Tire Distributors Holdings',
  'Anthem',
  'Archrock',
  'Ascena Retail Group',
  'AutoNation',
  'Best Buy',
  'CIT Group',
  'Cabot',
  'Comcast',
  'Comerica',
  'Core-Mark Holding',
  'DST Systems',
  'Darling Ingredients',
  'Delta Air Lines',
  'Delta Tucker Holdings',
  "Dick's Sporting Goods",
  'First Solar',
  'HCA Holdings',
  'Hanesbrands',
  'Hartford Financial Services Group',
  'Hawaiian Holdings',
  'HealthSouth',
  'Hyatt Hotels',
  'Kar Auction Services',
  'Kelly Services',
  'Kemper',
  'Kimberly-Clark',
  'Lennar',
  'Mercury General',
  'Mondelez International',
  'Motorola Solutions',
  'Nasdaq OMX Group',
  'National Oilwell Varco',
  'Nordstrom',
  'OneMain Holdings',
  'Oneok',
  'Orbital ATK',
  'Pep Boys-Mann',
  'Pool',
  'Precision Castparts',
  'Primoris Services',
  'Raymond James Financial',
  'Seaboard',
  'Securian Financial Group',
  'Simon Property Group',
  'State Farm Insurance Cos.',
  'State Street Corp.',
  'SunPower',
  'TEGNA',
  'Telephone & Data Systems',
  'Total System Services',
  'Tractor Supply',
  'TransDigm Group',
  'Trinity Industries',
  'TrueBlue',
  'Universal American',
  'Universal Health Services',
  'WGL Holdings',
  "Wendy's",
  'Werner Enterprises',
  'WestRock',
  'Williams-Sonoma'
]
```
- Usando aggregate, visualizar los productos que tengan más de 80 unidades
```Json
db.productos.aggregate(
 [
    {
        $match:{unidades:{$gt:80}}
    }
 ]
)

db.productos.aggregate(
 [
    {
        $match:{unidades:{$gt:80}}
    },
    {
     $project:{
        _id:0,
        unidades:1
     }
    }
 ]
)
```
**Resultados**
```Json
[
  {
    _id: ObjectId('67d9adc2953f84866adac827'),
    codigo: 0,
    nombre: 'Fantastic Wooden Fish',
    unidades: 95,
    precio: 291,
    fabricante: 'Kimberly-Clark',
    tipo: 'avanzado'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac829'),
    codigo: 2,
    nombre: 'Small Soft Fish',
    unidades: 96,
    precio: 189,
    fabricante: 'Primoris Services',
    tipo: 'medio'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac833'),
    codigo: 12,
    nombre: 'Refined Concrete Salad',
    unidades: 90,
    precio: 129,
    fabricante: 'Universal Health Services',
    tipo: 'avanzado'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac845'),
    codigo: 30,
    nombre: 'Small Rubber Pants',
    unidades: 89,
    precio: 16,
    fabricante: 'Hanesbrands',
    tipo: 'basico'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac848'),
    codigo: 33,
    nombre: 'Generic Concrete Hat',
    unidades: 82,
    precio: 70,
    fabricante: 'American Tire Distributors Holdings',
    tipo: 'basico'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac85c'),
    codigo: 53,
    nombre: 'Licensed Plastic Hat',
    unidades: 96,
    precio: 38,
    fabricante: 'Best Buy',
    tipo: 'medio'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac85d'),
    codigo: 54,
    nombre: 'Generic Metal Sausages',
    unidades: 84,
    precio: 77,
    fabricante: 'DST Systems',
    tipo: 'medio'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac864'),
    codigo: 61,
    nombre: 'Sleek Rubber Keyboard',
    unidades: 82,
    precio: 33,
    fabricante: 'Alere',
    tipo: 'basico'
  },
  {
    _id: ObjectId('67d9adc2953f84866adac869'),
    codigo: 66,
    nombre: 'Incredible Concrete Fish',
    unidades: 96,
    precio: 336,
    fabricante: 'Darling Ingredients',
    tipo: 'medio'
  }
]

[
  { unidades: 95 },
  { unidades: 96 },
  { unidades: 90 },
  { unidades: 89 },
  { unidades: 82 },
  { unidades: 96 },
  { unidades: 84 },
  { unidades: 82 },
  { unidades: 96 }
]
```
- Con $project visualizar solo el nombre, unidades y precio de los productos que tengan menos de 10 unidades
```Json
db.productos.aggregate(
 [
    {
        $match:{unidades:{$lt:10}}
    },
    {
     $project:{
        _id:0,
        nombre:1,
        unidades:1,
        precio:1
     }
    }
 ]
)
```
**Resultados**
```Json
[
  { nombre: 'Ergonomic Metal Ball', unidades: 5, precio: 246 },
  { nombre: 'Handmade Plastic Hat', unidades: 7, precio: 253 },
  { nombre: 'Ergonomic Metal Table', unidades: 0, precio: 94 },
  { nombre: 'Practical Frozen Chips', unidades: 0, precio: 305 },
  { nombre: 'Fantastic Metal Pants', unidades: 5, precio: 129 },
  { nombre: 'Intelligent Frozen Sausages', unidades: 3, precio: 111 },
  { nombre: 'Rustic Plastic Mouse', unidades: 5, precio: 24 }
]
```
- Con $project ponemos el fabricante pero le cambiamos el nombre por “empresa”. Usamos el mismo comando anterior
```Json
db.productos.aggregate(
 [
    {
        $match:{unidades:{$lt:10}}
    },
    {
     $project:{
        _id:0,
        nombre:1,
        unidades:1,
        precio:1,
        Empresa:"$fabricante",
     }
    }
 ]
)
```
**Resultados**
```Json
[
  {
    nombre: 'Ergonomic Metal Ball',
    unidades: 5,
    precio: 246,
    Empresa: 'Seaboard'
  },
  {
    nombre: 'Handmade Plastic Hat',
    unidades: 7,
    precio: 253,
    Empresa: "Dick's Sporting Goods"
  },
  {
    nombre: 'Ergonomic Metal Table',
    unidades: 0,
    precio: 94,
    Empresa: 'Kelly Services'
  },
  {
    nombre: 'Practical Frozen Chips',
    unidades: 0,
    precio: 305,
    Empresa: 'Delta Air Lines'
  },
  {
    nombre: 'Fantastic Metal Pants',
    unidades: 5,
    precio: 129,
    Empresa: 'OneMain Holdings'
  },
  {
    nombre: 'Intelligent Frozen Sausages',
    unidades: 3,
    precio: 111,
    Empresa: 'A.O. Smith'
  },
  {
    nombre: 'Rustic Plastic Mouse',
    unidades: 5,
    precio: 24,
    Empresa: 'Orbital ATK'
  }
]
```
- Añadir a la consulta anterior un campo calculado que se llame total y que multiplique precio por unidades.
```Json
db.productos.aggregate(
 [
    {
        $match:{unidades:{$lt:10}}
    },
    {
     $project:{
        _id:0,
        nombre:1,
        unidades:1,
        precio:1,
        Empresa:"$fabricante",
        total:{$multiply:["$precio","$unidades"]}
     }
    }
 ]
)
```
**Resultados**
```Json
[
  {
    nombre: 'Ergonomic Metal Ball',
    unidades: 5,
    precio: 246,
    Empresa: 'Seaboard',
    total: 1230
  },
  {
    nombre: 'Handmade Plastic Hat',
    unidades: 7,
    precio: 253,
    Empresa: "Dick's Sporting Goods",
    total: 1771
  },
  {
    nombre: 'Ergonomic Metal Table',
    unidades: 0,
    precio: 94,
    Empresa: 'Kelly Services',
    total: 0
  },
  {
    nombre: 'Practical Frozen Chips',
    unidades: 0,
    precio: 305,
    Empresa: 'Delta Air Lines',
    total: 0
  },
  {
    nombre: 'Fantastic Metal Pants',
    unidades: 5,
    precio: 129,
    Empresa: 'OneMain Holdings',
    total: 645
  },
  {
    nombre: 'Intelligent Frozen Sausages',
    unidades: 3,
    precio: 111,
    Empresa: 'A.O. Smith',
    total: 333
  },
  {
    nombre: 'Rustic Plastic Mouse',
    unidades: 5,
    precio: 24,
    Empresa: 'Orbital ATK',
    total: 120
  }
]
```
- Hacer que el nombre salga en mayúsculas con el operador $toUpper
```Json
db.productos.aggregate(
 [
    {
     $project:{
        _id:0,
        nombre:{$toUpper:"$nombre"},
     }
    }
 ]
)
```
**Resultados**
```Json
[
  { nombre: 'FANTASTIC WOODEN FISH' },
  { nombre: 'RUSTIC CONCRETE PANTS' },
  { nombre: 'SMALL SOFT FISH' },
  { nombre: 'PRACTICAL SOFT PANTS' },
  { nombre: 'ERGONOMIC METAL BALL' },
  { nombre: 'SMALL STEEL GLOVES' },
  { nombre: 'ERGONOMIC WOODEN SHIRT' },
  { nombre: 'HANDMADE STEEL CHAIR' },
  { nombre: 'HANDCRAFTED SOFT GLOVES' },
  { nombre: 'FANTASTIC CONCRETE SALAD' },
  { nombre: 'HANDMADE PLASTIC HAT' },
  { nombre: 'REFINED WOODEN TUNA' },
  { nombre: 'REFINED CONCRETE SALAD' },
  { nombre: 'UNBRANDED SOFT FISH' },
  { nombre: 'SMALL CONCRETE FISH' },
  { nombre: 'REFINED CONCRETE BIKE' },
  { nombre: 'TASTY COTTON PANTS' },
  { nombre: 'INCREDIBLE GRANITE GLOVES' },
  { nombre: 'PRACTICAL METAL MOUSE' },
  { nombre: 'HANDCRAFTED STEEL CHICKEN' }
]
```
- Añadir un campo calculado que ponga el nombre del producto y el tipo concatenado con el operador $concat. Le llamamos al campo “completo”
```Json
db.productos.aggregate(
 [
    {
     $project:{
        _id:0,
        completo:{$concat:["$nombre",", ","$tipo"]},
     }
    }
 ]
)
```
**Resultados**
```Json
[
  { completo: 'Fantastic Wooden Fish, avanzado' },
  { completo: 'Rustic Concrete Pants, medio' },
  { completo: 'Small Soft Fish, medio' },
  { completo: 'Practical Soft Pants, avanzado' },
  { completo: 'Ergonomic Metal Ball, medio' },
  { completo: 'Small Steel Gloves, avanzado' },
  { completo: 'Ergonomic Wooden Shirt, avanzado' },
  { completo: 'Handmade Steel Chair, medio' },
  { completo: 'Handcrafted Soft Gloves, basico' },
  { completo: 'Fantastic Concrete Salad, basico' },
  { completo: 'Handmade Plastic Hat, medio' },
  { completo: 'Refined Wooden Tuna, avanzado' },
  { completo: 'Refined Concrete Salad, avanzado' },
  { completo: 'Unbranded Soft Fish, basico' },
  { completo: 'Small Concrete Fish, medio' },
  { completo: 'Refined Concrete Bike, basico' },
  { completo: 'Tasty Cotton Pants, basico' },
  { completo: 'Incredible Granite Gloves, avanzado' },
  { completo: 'Practical Metal Mouse, basico' },
  { completo: 'Handcrafted Steel Chicken, medio' }
]
```
- Ordena el resultado por el campo “total”
```Json
db.productos.aggregate(
 [
    {
     $project:{
        _id:0,
        total:{$multiply:["$precio","$unidades"]}
     }
    },
    {
        $sort:{
            "$total":-1
        }
    }
 ]
)

db.productos.aggregate(
 [
    {
     $project:{
        _id:0,
        "total":{$multiply:["$precio","$unidades"]}
     }
    },
    {
        $sort:{
            "$total":1
        }
    }
 ]
)
```
**Resultados**
```Json
[
  { total: 32256 }, { total: 27645 },
  { total: 24163 }, { total: 22839 },
  { total: 20590 }, { total: 20160 },
  { total: 18414 }, { total: 18144 },
  { total: 15512 }, { total: 15145 },
  { total: 14994 }, { total: 12985 },
  { total: 11648 }, { total: 11644 },
  { total: 11610 }, { total: 11115 },
  { total: 10750 }, { total: 10023 },
  { total: 9434 },  { total: 9399 }
]

[
  { total: 0 },    { total: 0 },
  { total: 120 },  { total: 333 },
  { total: 630 },  { total: 645 },
  { total: 940 },  { total: 1075 },
  { total: 1104 }, { total: 1105 },
  { total: 1230 }, { total: 1368 },
  { total: 1424 }, { total: 1428 },
  { total: 1665 }, { total: 1767 },
  { total: 1771 }, { total: 1978 },
  { total: 2125 }, { total: 2256 }
]


```
- Haciendo una nueva consulta, averiguar el numero de productos por tipo de producto
```Json
db.productos.aggregate([
  { 
    $group: { _id: "$tipo", cantidad: { $sum: 1 } } }
])
```
**Resultados**
```Json
[
  { _id: 'avanzado', cantidad: 18 },
  { _id: 'basico', cantidad: 24 },
  { _id: 'medio', cantidad: 25 }
]
```
- Ordena el resultado por el campo “total”
```Json
db.productos.aggregate([
  { 
    $group: { 
      _id: "$tipo", 
      cantidad: { $sum: 1 }, 
      precio: { $sum: "$precio" } 
    } 
  },
  {
    $project: {
      _id: 0,
      tipo: "$_id",
      cantidad: 1,
      total: { $multiply: ["$precio", "$cantidad"] } 
    }
  },
  {
    $sort: {
      total: -1
    }
  }
])

```
**Resultados**
```Json
[
  { unidades: 25, tipo: 'medio', total: 109750 },
  { unidades: 24, tipo: 'basico', total: 85272 },
  { unidades: 18, tipo: 'avanzado', total: 50166 }
]
```
- Añadir el valor mayor y el menor
```Json
db.productos.aggregate([
  { 
    $group: { 
      _id: "$tipo", 
      cantidad: { $sum: 1 }, 
      precioTotal: { $sum: "$precio" },
      Max: { $max: "$precio" }, 
      Min: { $min: "$precio" }
    } 
  },
  {
    $project: {
      _id: 0,
      tipo: "$_id",
      cantidad: 1,
      total: { $multiply: ["$precioTotal", "$cantidad"] },
      Max: 1,
      Min: 1
    }
  },
  {
    $sort: {
      total: -1
    }
  }
])
```
**Resultados**
```Json
[
  { cantidad: 25, Max: 337, Min: 16, tipo: 'medio', total: 109750 },
  { cantidad: 24, Max: 285, Min: 16, tipo: 'basico', total: 85272 },
  { cantidad: 18, Max: 331, Min: 18, tipo: 'avanzado', total: 50166 }
]
```
- Añade el total de unidades por cada tipo
```Json
db.productos.aggregate([
  { 
    $group: { 
      _id: "$tipo", 
      cantidad: { $sum: 1 }, 
      precioTotal: { $sum: "$precio" },
      Max: { $max: "$precio" }, 
      Min: { $min: "$precio" },
      totalUnidades: { $sum: "$unidades" }

    } 
  },
  {
    $project: {
      _id: 0,
      tipo: "$_id",
      cantidad: 1,
      total: { $multiply: ["$precioTotal", "$cantidad"] },
      Max: 1,
      Min: 1,
      totalUnidades: 1
    }
  },
  {
    $sort: {
      total: -1
    }
  }
])
```
**Resultados**
```Json
[
  {
    cantidad: 25,
    Max: 337,
    Min: 16,
    totalUnidades: 1224,
    tipo: 'medio',
    total: 109750
  },
  {
    cantidad: 24,
    Max: 285,
    Min: 16,
    totalUnidades: 1067,
    tipo: 'basico',
    total: 85272
  },
  {
    cantidad: 18,
    Max: 331,
    Min: 18,
    totalUnidades: 773,
    tipo: 'avanzado',
    total: 50166
  }
]
```
- Con el operador $set y el operador “$substr” visualiza todos los datos del producto "Small Metal Tuna" y los primeros 5 caracteres del nombre.
```Json
db.productos.aggregate([
  { 
    $match: { nombre: "Small Metal Tuna" } 
  },
  { 
    $set: { 
      nombreCorto: { $substr: ["$nombre", 0, 5] } 
    } 
  }
])

```
**Resultados**
```Json
[
  {
    _id: ObjectId('67d9adc2953f84866adac85e'),
    codigo: 55,
    nombre: 'Small Metal Tuna',
    unidades: 46,
    precio: 43,
    fabricante: 'Raymond James Financial',
    tipo: 'medio',
    nombreCorto: 'Small'
  }
]
```
- Creamos una salida que tenga el nombre del articulo y el total (precio por unidades) y lo guardamos en una colección denominada productos2
```Json
db.productos.aggregate([
  {
    $project: {
      _id: 0,
      nombre: 1,
      total: { $multiply: ["$precio", "$unidades"] }
    }
  },
  { 
    $out: "productos2" 
  }
])
```
- Comprobamos que se ha creado
```Json
    show collections
```

- Hacemos un find para comprobar el resultado
```Json
    db.productos2.find()
```
**Resultados**
```Json
[
  {
    _id: ObjectId('67da496d5caff56a91524f91'),
    nombre: 'Fantastic Wooden Fish',
    total: 27645
  },
  {
    _id: ObjectId('67da496d5caff56a91524f92'),
    nombre: 'Rustic Concrete Pants',
    total: 18414
  },
  {
    _id: ObjectId('67da496d5caff56a91524f93'),
    nombre: 'Small Soft Fish',
    total: 18144
  },
  {
    _id: ObjectId('67da496d5caff56a91524f94'),
    nombre: 'Practical Soft Pants',
    total: 2747
  },
  {
    _id: ObjectId('67da496d5caff56a91524f95'),
    nombre: 'Ergonomic Metal Ball',
    total: 1230
  },
  {
    _id: ObjectId('67da496d5caff56a91524f96'),
    nombre: 'Small Steel Gloves',
    total: 1665
  },
  {
    _id: ObjectId('67da496d5caff56a91524f97'),
    nombre: 'Ergonomic Wooden Shirt',
    total: 14994
  },
  {
    _id: ObjectId('67da496d5caff56a91524f98'),
    nombre: 'Handmade Steel Chair',
    total: 5392
  },
  {
    _id: ObjectId('67da496d5caff56a91524f99'),
    nombre: 'Handcrafted Soft Gloves',
    total: 4512
  },
  {
    _id: ObjectId('67da496d5caff56a91524f9a'),
    nombre: 'Fantastic Concrete Salad',
    total: 12985
  },
  {
    _id: ObjectId('67da496d5caff56a91524f9b'),
    nombre: 'Handmade Plastic Hat',
    total: 1771
  },
  {
    _id: ObjectId('67da496d5caff56a91524f9c'),
    nombre: 'Refined Wooden Tuna',
    total: 8480
  },
  {
    _id: ObjectId('67da496d5caff56a91524f9d'),
    nombre: 'Refined Concrete Salad',
    total: 11610
  },
  {
    _id: ObjectId('67da496d5caff56a91524f9e'),
    nombre: 'Unbranded Soft Fish',
    total: 9434
  },
  {
    _id: ObjectId('67da496d5caff56a91524f9f'),
    nombre: 'Small Concrete Fish',
    total: 5040
  },
  {
    _id: ObjectId('67da496d5caff56a91524fa0'),
    nombre: 'Refined Concrete Bike',
    total: 2700
  },
  {
    _id: ObjectId('67da496d5caff56a91524fa1'),
    nombre: 'Tasty Cotton Pants',
    total: 3536
  },
  {
    _id: ObjectId('67da496d5caff56a91524fa2'),
    nombre: 'Incredible Granite Gloves',
    total: 20590
  },
  {
    _id: ObjectId('67da496d5caff56a91524fa3'),
    nombre: 'Practical Metal Mouse',
    total: 6650
  },
  {
    _id: ObjectId('67da496d5caff56a91524fa4'),
    nombre: 'Handcrafted Steel Chicken',
    total: 6215
  }
]
Type "it" for more
```
- Usando $cond y $project vamos a visualizar el nombre del producto, el precio y un campo llamado valoración que ponga “barato” si el precio es menor de 250 y caro si es mayor o igual
```Json
    show collections
```

- Hacemos un find para comprobar el resultado
```Json
db.productos.aggregate([
  {
    $project: {
      _id: 0,
      nombre: 1,
      precio: 1,
      valoración: {
        $cond: { 
          if: { $lt: ["$precio", 250] }, 
          then: "barato", 
          else: "caro" 
        }
      }
    }
  }
])

```
**Resultados**
```Json
[
  {
    nombre: 'Fantastic Wooden Fish',
    precio: 291,
    'valoración': 'caro'
  },
  {
    nombre: 'Rustic Concrete Pants',
    precio: 279,
    'valoración': 'caro'
  },
  { nombre: 'Small Soft Fish', precio: 189, 'valoración': 'barato' },
  {
    nombre: 'Practical Soft Pants',
    precio: 67,
    'valoración': 'barato'
  },
  {
    nombre: 'Ergonomic Metal Ball',
    precio: 246,
    'valoración': 'barato'
  },
  { nombre: 'Small Steel Gloves', precio: 37, 'valoración': 'barato' },
  {
    nombre: 'Ergonomic Wooden Shirt',
    precio: 238,
    'valoración': 'barato'
  },
  { nombre: 'Handmade Steel Chair', precio: 337, 'valoración': 'caro' },
  {
    nombre: 'Handcrafted Soft Gloves',
    precio: 282,
    'valoración': 'caro'
  },
  {
    nombre: 'Fantastic Concrete Salad',
    precio: 265,
    'valoración': 'caro'
  },
  { nombre: 'Handmade Plastic Hat', precio: 253, 'valoración': 'caro' },
  {
    nombre: 'Refined Wooden Tuna',
    precio: 212,
    'valoración': 'barato'
  },
  {
    nombre: 'Refined Concrete Salad',
    precio: 129,
    'valoración': 'barato'
  },
  {
    nombre: 'Unbranded Soft Fish',
    precio: 178,
    'valoración': 'barato'
  },
  {
    nombre: 'Small Concrete Fish',
    precio: 126,
    'valoración': 'barato'
  },
  {
    nombre: 'Refined Concrete Bike',
    precio: 180,
    'valoración': 'barato'
  },
  { nombre: 'Tasty Cotton Pants', precio: 52, 'valoración': 'barato' },
  {
    nombre: 'Incredible Granite Gloves',
    precio: 290,
    'valoración': 'caro'
  },
  {
    nombre: 'Practical Metal Mouse',
    precio: 190,
    'valoración': 'barato'
  },
  {
    nombre: 'Handcrafted Steel Chicken',
    precio: 113,
    'valoración': 'barato'
  }
]
Type "it" for more
```