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
{ "_id" : ObjectId("5b0ba91e7bd532f5d790cf44"), "nombre" : "Proyecto02", "descripcion" : "Descripcion
