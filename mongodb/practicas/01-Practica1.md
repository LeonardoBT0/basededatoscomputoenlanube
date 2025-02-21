# Practica 1: Base de datos, colecciones e inserts

1. Conectarnos con mongosh a MongoDB
1. Crear una base de datos llamada curso
1. Comprobar que la base de datos no existe
1. Crear una coleccion que se llame facturas

``` json
db.createCollection('facturas')
show collections
```
5. Insertar un documento con los siguientes valores

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Factura | 10 |
| Ciente | Frutas Ramirez |
| Total | 223 |



| Codigo   | Valor   |
|-------------|-------------|
| Cod_Factura | 20 |
| Ciente | Ferreteria Juan |
| Total | 140 |

``` json
db.facturas.insertOne(
 {
    cod_facturas: 10,
    cliente: 'Frutas ramirez',
    total: 223
 }
)



db.facturas.insertOne( 
  { 
    cod_facturas: 20, 
    cliente: 'Ferreteria Juan', 
    total: 140 
  } 
)
```

6. Crear una nueva colleccion pero usando ddirectamente el insertOne, insertar un cocumento con los siguientes datos: 

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 1 |
| Nombre |  Tornillo x1" |
| Precio | 2 |
| Unidades | 1500 |

``` json
db.productos.insertOne( 
  { 
    cod_productos: 1, 
    nombre: 'Tornillo x 1', 
    precio: 2, 
    unidades: 1500 
  } 
)
```

7. Crear un nuevo documento de producto que contenga un array con los siguientes datos:

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 2 |
| Nombre |  Martillo |
| Precio | 20 |
| Unidades | 50 |
| Fabricantes | fab1, fab2, fab3, fab4 |

``` json
db.productos.insertOne(
  {
    cod_producto: 2,
    nombre: 'Martillo',
    precio: 20,
    unidades: 50,
    fabricantes: [ "fab1", "fab2", "fab3", "fab4"]
  }
)
```

8. Borrar la coleccion facturas

``` json
db.facturas.drop()
show collections
```

9. Insertar un documento en una coleccion denominada **fabricantes** para proba los sbdocumentos y la clave _id personalizada

| Codigo   | Valor   |
|-------------|-------------|
| id | 1 |
| Nombre |  fab1 |
| Localidad | ciudad: buenos aires,  pais: argentina, calle: calle pez 27, cod_postal:2900 |

``` json
db.fabricante.insertOne(
  {
    _id: 1,
    nombre: 'Fab1',
    Localidad: {
        ciudad: 'Buenos Aires',
        pais: 'Argentina',
        calle: 'Calle pez 27',
        cod_postal: 2900
    }
  }
)
```

10. Realizar una insercion de varios documentos en la coleccion productos

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 3 |
| Nombre |  Alicantes |
| Precio | 10 |
| Unidades | 25 |
| Fabricantes | fab1, fab2, fab5|

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 4 |
| Nombre |  Arandelas |
| Precio | 1 |
| Unidades | 500 |
| Fabricantes | fab2, fab3, fab4|