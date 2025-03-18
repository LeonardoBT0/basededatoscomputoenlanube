# Agregaciones

1. Para hacer esta práctica vamos a cargar unos datos ficticios de empresas.
2. Tienes un fichero denominado “productos.json”
3. Debes poner el resultado de las consultas en cada apartado

- Cuenta los productos de tipo “medio”, usando un método básico
- Indicar con un distinct, las empresas (fabricantes) que hay en la colección
- Usando aggregate, visualizar los productos que tengan más de 80 unidades
- Con $project visualizar solo el nombre, unidades y precio de los productos que tengan menos de 10 unidades
- Con $project ponemos el fabricante pero le cambiamos el nombre por “empresa”. Usamos el mismo comando anterior
- Añadir a la consulta anterior un campo calculado que se llame total y que multiplique precio por unidades.
- Hacer que el nombre salga en mayúsculas con el operador $toUpper
- Añadir un campo calculado que ponga el nombre del producto y el tipo concatenado con el operador $concat. Le llamamos al campo “completo”
- Ordena el resultado por el campo “total”
- Haciendo una nueva consulta, averiguar el numero de productos por tipo de producto
- Añadir el valor mayor y el menor
- Añade el total de unidades por cada tipo
- Con el operador $set y el operador “$substr” visualiza todos los datos del producto "Small Metal Tuna" y los primeros 5 caracteres del nombre.
- Creamos una salida que tenga el nombre del articulo y el total (precio por unidades) y lo guardamos en una colección denominada productos2
- Comprobamos que se ha creado
- Hacemos un find para comprobar el resultado
- Usando $cond y $project vamos a visualizar el nombre del producto, el precio y un campo llamado valoración que ponga “barato” si el precio es menor de 250 y caro si es mayor o igual
