## Modelo de datos en MongoDB

- Modelos
    - Embebidos,
    - Referenciados

- Modelos Embebidos

*Uno a Uno*

 json
db.departamentos.insertMany([
    {
        _id: 1,
        nombre: "Tecnologias de la Informacion",
        responsable: {
            nombre: "Monico",
            apellidos: "Ramirez Perez"
        },
        descripcion: "ejemplo de departamento"
    },
    {
        _id: 2,
        nombre: "Tecnologias de la Informacion",
        responsable: {
            nombre: "Raul",
            apellidos: "Lopez Hernandez"
        },
        descripcion: "ejemplo de departamento"
    }
])


-- Modelos Referenciados

*Uno a Uno*

db.localidades.insertMany([
    {
        _id: 'BA',
        ciudad: "Buenos Aires",
        pais: "Argentina",
        poblacion: 16000000, // mejor como número
        turismo: ["edificios", "tango", "gastronomia", "museos", "parques"], // corregí "edificions"
        direccion: "Avenida Tortolos",
        cod_departamento: 1
    },
    {
        _id: 'SA',
        ciudad: "Santiago",
        pais: "Chile",
        poblacion: 20000000, // mejor como número
        turismo: ["iglesias", "vino", "gastronomia", "museos"], // corregí "iglesia" a "iglesias" (opcional)
        direccion: "Avenida Soyla Vaca del Corral",
        cod_departamento: 2
    }
])

db.departamentos.aggregate([
    {
        $lookup: {
            from: "localidades",
            localField: "_id",
            foreignField: "cod_departamento",
            as: "localidades"
        }
    }
])

db.categorias.insertMany([{
    _id:"1",
    nombre:"categoria1"
},
{
    _id:"2",
    "nombre":"categoria2"
}

])

db.productos.insertMany(
    [
        {
            _id:"1",
            "nombre":"producto1",
            "precio":10,
            "existencia":20,
            "cod_categoria":1
        },
         {
            _id:"2",
            "nombre":"producto2",
            "precio":10,
            "existencia":20,
            "cod_categoria":2
        }
    ]
)


db.categorias.aggregate([
    {
        $lookup: {
            from: "productos",
            localField: "_id",
            foreignField: "cod_categoria",
            as: "productos"
        }
    }
])