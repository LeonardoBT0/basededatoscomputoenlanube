
# Crud y consultas en MongoDB
Solo se crea si contiene por lo menos una coleccion
**use bd1**

## Como crear una coleccion
use db1
db.createCollection("Empleado")

## Mostrar las colecciones
show collections

## Insertar un documento


```json
 db.Alumnos.insertOne(
  {
    _id: ObjectId('679d2ab6078c2dd4adcb0ce2'),
    nombre: 'Soyla',
    apellido1: 'Vaca',
    ciudad: 'San Miguel de las Piedras'
  }
)
```

## Insercion
```json
db.Alumnos.insertOne
(
 { 
    nombre: "Joaquin",
    apellido1: "Dorian",
    apellido2: "Guerrero",
    edad: 15,
    aficiones: ["Cerveza","Hueva","Canavis"]
 }
)
```
## Insercion de documentos mas complejos con documentos anidados 
```json
db.Alumnos.insertOne
(
 {
    nombre: "Leonardo",
    apellido1: "Barrera",
    apellido2: "Tejeda",
    edad: 20,
    estudios: [
            "Kinder","Primaria","Secundaria","Preparatoria"
              ],
    experiencia: {
    lenguaje: "SQL",
    sbd: "SQL Server",
    aniosExp: 14
        }
 }
)
```