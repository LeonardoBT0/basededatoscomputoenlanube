# Arrays y documentos anidados

1. Para hacer esta práctica vamos a cargar unos datos ficticios de empresas.
2. Tienes un fichero denominado “personas.json”
3. Debes poner el resultado de las consultas en cada apartado
- Buscar las personas que vivan en Colombia
```Json
db.personas.find(
    {"direccion.pais":'Colombia'},
    {_id:0,"direccion.pais":1}
)

db.personas.find(
    {"direccion.pais":'Colombia'}
)
```
**Resultados**
```Json
[ { direccion: { pais: 'Colombia' } } ]


[
  {
    _id: ObjectId('67d97db231d0836bcd22ea73'),
    nombre: 'Anni Niño',
    direccion: {
      calle: '207 Taylor Cliffs',
      ciudad: 'Buenaventura',
      pais: 'Colombia'
    },
    colores: [ 'yellow', 'salmon', 'yellow' ],
    ingresos: 7387
  }
]
```
- Personas a las que le guste el color rosa
```Json
db.personas.find(
    {colores:'pink'},
    {_id:0,colores:1}
)

db.personas.find(
    {colores:'pink'}
)
```
**Resultados**
```Json
[
  { colores: [ 'pink', 'blue', 'teal' ] },
  { colores: [ 'orchid', 'teal', 'pink' ] }
]

[
  {
    _id: ObjectId('67d97db231d0836bcd22ea6b'),
    nombre: 'Laura Oquendo',
    direccion: {
      calle: '2800 Samir Trail',
      ciudad: 'Bijelo Polje',
      pais: 'Montenegro'
    },
    colores: [ 'pink', 'blue', 'teal' ],
    ingresos: 8707
  },
  {
    _id: ObjectId('67d97db231d0836bcd22ea78'),
    nombre: 'Lorena Saiz',
    direccion: { calle: '1611 Oscar Walk', ciudad: 'The Pas', pais: 'Canada' },
    colores: [ 'orchid', 'teal', 'pink' ],
    ingresos: 10407
  }
]
```
- Personas cuyo tercer color preferido sea el amarillo (yellow). Recuerda que los arrays comienzan por Cero. Deben salir 3
```Json
db.personas.find(
    {"colores.2":'yellow'},
    {_id:0,colores:1}
)

db.personas.find(
    {"colores.2":'yellow'}
)
```
**Resultados**
```Json
[
  { colores: [ 'indigo', 'green', 'yellow', 'salmon' ] },
  { colores: [ 'yellow', 'salmon', 'yellow' ] },
  {
    colores: [ 'green', 'indigo', 'yellow', 'salmon', 'grey', 'violet' ]
  }
]

[
  {
    _id: ObjectId('67d97db231d0836bcd22ea6c'),
    nombre: 'Laura Salcedo',
    direccion: {
      calle: '11046 Cayla Centers',
      ciudad: 'Rosso',
      pais: 'Mauritania'
    },
    colores: [ 'indigo', 'green', 'yellow', 'salmon' ],
    ingresos: 7435
  },
  {
    _id: ObjectId('67d97db231d0836bcd22ea73'),
    nombre: 'Anni Niño',
    direccion: {
      calle: '207 Taylor Cliffs',
      ciudad: 'Buenaventura',
      pais: 'Colombia'
    },
    colores: [ 'yellow', 'salmon', 'yellow' ],
    ingresos: 7387
  },
  {
    _id: ObjectId('67d97db231d0836bcd22ea74'),
    nombre: 'Andrea Paredes',
    direccion: {
      calle: '09438 Vandervort Drives',
      ciudad: 'San Antonio',
      pais: 'Puerto Rico'
    },
    colores: [ 'green', 'indigo', 'yellow', 'salmon', 'grey', 'violet' ],
    ingresos: 6340
  }
]
```
- Personas cuyo tercer color preferido sea el amarillo (yellow) y que vivan en Mauritania (debe salir uno)
```Json
db.personas.find({
 $and:[
    {"colores.2":'yellow'}, 
    {"direccion.pais":'Mauritania'}
 ]
},
{_id:0,"direccion.pais":1,"colores.1":1}
)

db.personas.find({
 $and:[
    {"colores.2":'yellow'}, 
    {"direccion.pais":'Mauritania'}
  ]
 }
)
```
**Resultados**
```Json
[ { direccion: { pais: 'Mauritania' }, colores: [] } ]

[
  {
    _id: ObjectId('67d97db231d0836bcd22ea6c'),
    nombre: 'Laura Salcedo',
    direccion: {
      calle: '11046 Cayla Centers',
      ciudad: 'Rosso',
      pais: 'Mauritania'
    },
    colores: [ 'indigo', 'green', 'yellow', 'salmon' ],
    ingresos: 7435
  }
]
```
- Usando el operador $all averiguar las personas que les gusta el plata (silver) y el salmon (salmon)
```Json
db.personas.find(
    {colores:{$all:['silver','salmon']}},
    {_id:0,colores:1}
)

db.personas.find(
    {colores:{$all:['silver','salmon']}}
)
```
**Resultados**
```Json
[ { colores: [ 'plum', 'silver', 'olive', 'salmon', 'silver' ] } ]

[
  {
    _id: ObjectId('67d97db231d0836bcd22ea70'),
    nombre: 'Ángel Anguiano',
    direccion: {
      calle: '20780 McLaughlin Union',
      ciudad: 'Paramaribo',
      pais: 'Suriname'
    },
    colores: [ 'plum', 'silver', 'olive', 'salmon', 'silver' ],
    ingresos: 5712
  }
]
```
- Con el operador $elemMatch, averigua las personas que les guste el rosa (Pink) o el rojo (red)

```Json
db.personas.find(
    {colores:{$elemMatch:{$eq:'pink',$eq:'red'}}},
    {_id:0,colores:1}
)

db.personas.find(
    {colores:{$elemMatch:{$eq:'pink',$eq:'red'}}}
)
```
**Resultados**
```Json
[
  { colores: [ 'indigo', 'sky blue', 'red' ] },
  { colores: [ 'maroon', 'red', 'cyan', 'blue', 'white', 'gold' ] },
  { colores: [ 'red', 'yellow', 'orange', 'violet' ] },
  { colores: [ 'orange', 'maroon', 'white', 'tan', 'red', 'maroon' ] }
]

[
  {
    _id: ObjectId('67d97db231d0836bcd22ea6f'),
    nombre: 'Sergi Cordero',
    direccion: {
      calle: '0605 Delfina Lodge',
      ciudad: 'Obiozara',
      pais: 'Nigeria'
    },
    colores: [ 'indigo', 'sky blue', 'red' ],
    ingresos: 7134
  },
  {
    _id: ObjectId('67d97db231d0836bcd22ea79'),
    nombre: 'Manuel Campos',
    direccion: {
      calle: '291 Waelchi Crest',
      ciudad: 'Holetown',
      pais: 'Barbados'
    },
    colores: [ 'maroon', 'red', 'cyan', 'blue', 'white', 'gold' ],
    ingresos: 11230
  },
  {
    _id: ObjectId('67d97db231d0836bcd22ea7a'),
    nombre: 'Salvador Meraz',
    direccion: {
      calle: '9327 Satterfield Alley',
      ciudad: 'Tuntange',
      pais: 'Luxembourg'
    },
    colores: [ 'red', 'yellow', 'orange', 'violet' ],
    ingresos: 4058
  },
  {
    _id: ObjectId('67d97db231d0836bcd22ea7d'),
    nombre: 'Ángel Zaragoza',
    direccion: {
      calle: "2758 O'Connell Ridge",
      ciudad: 'Barclayville',
      pais: 'Liberia'
    },
    colores: [ 'orange', 'maroon', 'white', 'tan', 'red', 'maroon' ],
    ingresos: 9869
  }
]
```