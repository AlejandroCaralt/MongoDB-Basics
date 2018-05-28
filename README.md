# MongoDB-Basics

## Crear una base de datos.

```console
> use ProgrammingStudio
switched to db ProgrammingStudio
```

## Tener una colección.

```console
> db.createCollection("Proyecto")
{ "ok" : 1 }
```
<img src="MongoDB.png" >
Creando la base de datos, la coleccion y insertando algunos documentos.

## Insertar, modificar y borrar documentos en la colección.

### Insertar:
```console
> var Proyecto01 = {nombre: "Proyecto1", descripcion: "Proyecto en Angular", presupuesto: 5000}
> db.Proyecto.insert(Proyecto01)
WriteResult({ "nInserted" : 1 })

> db.Proyecto.insert({nombre: "Proyecto2", descripcion: "Proyecto en Java"})
WriteResult({ "nInserted" : 1 })
```

### Modificar:
```console
> modificacion = db.Proyecto.findOne({nombre: "Proyecto02"})
{
      "_id" : ObjectId("5b0ba91e7bd532f5d790cf44"),
      "nombre" : "Proyecto02",
      "descripcion" : "Proyecto en Java"
}

>modificacion.descripcion = "Descripción actualizada"
Descripción actualizada
>db.Proyecto.update({nombre: "Proyecto02"}, modificacion)
WriteResult({"nMatched" : 1, "nUpserted" : 0, "nModified" : 1})
>db.Proyecto.find({nombre: "Proyecto02"})
{ "_id" : ObjectId("5b0ba91e7bd532f5d790cf44"), "nombre" : "Proyecto02", "descripcion" : "Descripcion actualizada"}
```

### Eliminar:
```console
> db.Proyecto.remove({nombre: "Proyecto02"})
WriteResult({ "nRemoved" : 1 })
```

## Crear un índice sobre un campo de la colección.
```console
> db.Proyecto.createIndex({nombre: 1})
{
        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```
<img src="MongoDB_04.png" >
Modificando las descripción de un documento y creando un índice en un campo.

## Realizar consultas en las que utilices, igual, mayor y menor que.

### Presupuesto igual a "5000":
```console
> db.Proyecto.find({ "presupuesto": 5000}
{ "_id" : ObjectId("5b0ba8b07bd532f5d790cf43"), "nombre" : "Proyecto01", "descripcion" : "Proyecto en Angular", "presupuesto" : 5000}
```
### Presupuesto mayor que "1000":
```console
> db.Proyecto.find({ "presupuesto": {$gt: 1000}})
{ "_id" : ObjectId("5b0ba8b07bd532f5d790cf43"), "nombre" : "Proyecto01", "descripcion" : "Proyecto en Angular", "presupuesto" : 5000}
```
### Presupuesto menor que "10.000":
```console
> db.Proyecto.find({ "presupuesto": {$lt: 10000}})
{ "_id" : ObjectId("5b0ba8b07bd532f5d790cf43"), "nombre" : "Proyecto01", "descripcion" : "Proyecto en Angular", "presupuesto" : 5000}
```

## Realizar una consulta en la que los documentos se muestren ordenados y se limite el número de mostrados.
Muestra por pantalla los Proyectos con mayor presupuesto, ordenados ascendentemente.
```console
>db.Proyecto.find().sort({presupuesto: -1}).limit(2)
{ "_id" : ObjectId("5b0bc8ce7bd532f5d790cf47"), "nombre" : "Proyecto06", "descripcion" : "Proyecto en PHP", "presupuesto" : 12000}
{ "_id" : ObjectId("5b0ba8b07bd532f5d790cf43"), "nombre" : "Proyecto01", "descripcion" : "Proyecto en Angular", "presupuesto" : 5000}
```
<img src="MongoDB_03.png" >
Modificando las descripción de un documento y creando un índice en un campo.
Consultas con "Igual que, mayor que y menor que" y consulta ordenada y delimitada.

## Realizar una consulta con agrupamiento y una función para mostrar la media, o suma, o la que tú decidas.
Muestra por pantalla los proyectos agrupados por sus descripciones y la media de sus presupuestos.
```console
>db.Proyecto.aggregate([{$group: {_id: "$nombre", "PresupuestoMedio": {$avg: "$presupuesto"}}}])
```
<img src="MongoDB_02.png" >
