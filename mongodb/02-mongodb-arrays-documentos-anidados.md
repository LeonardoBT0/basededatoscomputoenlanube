# Busquedas en Arrays y Documentos anidaddos

## Buscar dentro de un documento anidado

```Json

db1> db.ciudades.find({
 alcalde: {
    nombre: "Crystal",
    apellidos: "Long",
    edad:76
  }
 }
)

 db.ciudades.find({
     "alcalde.nombre":"Crystal"
 }
)
```

1. Seleccionar las ciudades donde los alcaldes tengan mas de 70 años

```Json
db.ciudades.find(
 {
    "alcalde.edad":{$gte:70}
 }
)

db.ciudades.find( 
    {"alcalde.edad": { $gte: 70 } },
    {_id:0,nombre:1, "alcalde.edad":1} 
)
```

3. Seleccionar las ciudades donde el alcalde tenga 76 años o 41

```Json
db.ciudades.find(
 {
    $or:[
    {"alcalde.edad":{$gt:76}},
    {"alcalde.edad":{$gt:41}}
    ]
 }
)
```

# Consultas con Arrays

1. Crear la coleccion de casas

2. Cargar los documentos de la coleccion cazas, de la data cazas

## Ejemplos de consultas con Arrays

1. Buscar los documentos que tengan usa como paises

```Json
 db.cazas.find({
   paises:"usa"
 }
)
```

2. Buscar los documentos donde cualquier elemento del array dimensiones sea mayor a 5

```Json
 db.cazas.find({
   dimensiones:{$gt:5}
 }
)
```

3. Buscar los documentos donde las dimensiones del avion por ancho que es la posicion 1, sea superior a 14

```Json
 db.cazas.find({
   "dimensiones.1":{$gt:14}
 }
)

 db.cazas.find(
   {"dimensiones.1":{$gt:14}},
   {_id:0,modelo:1,dimensiones:1}
)
```

### Arrays. Operador $all

1. Buscar los aviones que estan sirviendo en Egipto y en Israel

```Json
 db.cazas.find({
   paises:{$all:["egipto","israel"]}
 }
)

 db.cazas.find({
   $and:[
   {paises:"egipto"},
   {paises:"israel"}
   ]
 }
)
```

2. Seleccionar los cazas que sirven en inglaterra y españa

```Json
 db.cazas.find({
   paises:{$all:["inglaterra","españa"]}
 }
)
```

## Arrays operador #elemMatch -> Permite hacer busquedas dentro de arrays, este busca la lista dde condiciones que esten dentro del operador

1. Buscar que aviones tienen uso dentro de inglaterra

```Json
db.cazas.find({
   paises:{$elemMatch:{$eq:"inglaterra"}}
})
```

2. Buscar los aviones donde las dimensiones sean menores a 20 o mayores a 15

```Json
db.cazas.find({
   dimensiones:{$elemMatch:{$gt:15,$lt:20}}
})
```

### Buscar en arrays de documentos anidados

1. Utilizar la coleccion ciudades
2. Buscar los consejeros de nombre Jeri Flower de edad 78

```Json
db.cazas.find({
   dimensiones:{$elemMatch:{$gt:15,$lt:20}}
})
```

3. Buscar en consejeros que la edad sea mayor a 70

```Json
db.cazas.find({
  "consejeros.edad":{$gt:70}
})
```

4. Buscar consejeros en la posiscion 2 que esten ente 70 y 80 años

```Json
db.ciudades.find(
    {"consejeros.2.edad":{$gte:70,$lte:80}},
    {_id:0,"consejeros.nombre":1,"consejeros.edad":1}
)  
```

5. Buscar en consejeros de la posicion 0 que sean mayores a 70 

```Json
db.ciudades.find(
    {"consejeros.0.edad":{$gt:70}},
    {_id:0,"consejeros.nombre":1,"consejeros.edad":1}
)  
```

6. Buscar consejeros mayores a 70

```Json
db.ciudades.find(
    {"consejeros.edad":{$gt:70}},
)  
```