# Proyecto MongoDB: Base de Datos de Red Social

Este proyecto tiene como objetivo desarrollar una base de datos en MongoDB para gestionar usuarios y publicaciones de una red social. El trabajo incluye la creación de colecciones para `users` y `posts`, y la ejecución de varias consultas para insertar, actualizar, obtener y eliminar datos.

---

## Estructura del Proyecto

### Colecciones:
1. **users**: Contiene los datos de los usuarios de la red social.
   - `username`: Nombre de usuario.
   - `email`: Correo electrónico del usuario.
   - `age`: Edad del usuario.

2. **posts**: Contiene las publicaciones realizadas en la red social.
   - `title`: Título de la publicación.
   - `body`: Contenido de la publicación.
   - `username`: Nombre de usuario que realizó la publicación.
     - `username`: Nombre del usuario que dejó el comentario.
     - `body`: Texto del comentario.

---

## 1. Consultas Requeridas

### 1.1 Insertar Datos

Se insertaron al menos 10 usuarios y 15 publicaciones con al menos 2 comentarios por publicación.

facebook> db.users.insertMany([
...   { username: "Pedro", email: "pedro@email.com", age: 24 },
...   { username: "Sofia", email: "sofia@email.com", age: 26 },
...   { username: "Laura", email: "laura@email.com", age: 27 },
...   { username: "Luis", email: "luis@email.com", age: 26 },
...   { username: "Clara", email: "clara@email.com", age: 29 },
...   { username: "Jose", email: "jose@email.com", age: 31 },
...   { username: "Karla", email: "karla@email.com", age: 28 },
...   { username: "Diana", email: "diana@email.com", age: 30 },
...   { username: "Manuel", email: "manuel@email.com", age: 25 },
...   { username: "Fernanda", email: "fernanda@email.com", age: 27 }
... ]);
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6748e66b95d264db706f9f9c'),
    '1': ObjectId('6748e66b95d264db706f9f9d'),
    '2': ObjectId('6748e66b95d264db706f9f9e'),
    '3': ObjectId('6748e66b95d264db706f9f9f'),
    '4': ObjectId('6748e66b95d264db706f9fa0'),
    '5': ObjectId('6748e66b95d264db706f9fa1'),
    '6': ObjectId('6748e66b95d264db706f9fa2'),
    '7': ObjectId('6748e66b95d264db706f9fa3'),
    '8': ObjectId('6748e66b95d264db706f9fa4'),
    '9': ObjectId('6748e66b95d264db706f9fa5')
  }
}
facebook> 

facebook> db.posts.updateOne(
...   { title: "Publicación 1" },
...   {
...     $set: {
...       title: "Publicación actualizada",
...       body: "Cuerpo actualizado",
...       username: "Carlos",
...       comments: [
...         { username: "Laura", body: "Comentario actualizado" },
...         { username: "Sofia", body: "Otro comentario actualizado" }
...       ]
...     }
...   }
... );
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
facebook> 

facebook> 

facebook> db.posts.updateOne(
...   { title: "Publicación 2" },
...   { $set: { body: "Nuevo cuerpo de la publicación" } }
... );
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
facebook> 

facebook> 

facebook> db.posts.updateOne(
...   { title: "Publicación 3" },
...   { $set: { "comments.0.body": "Comentario modificado" } }
... );
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
facebook> 

facebook> 

facebook> db.users.updateOne(
...   { username: "Pedro" },
...   { $set: { email: "pedro.nuevo@email.com", age: 25 } }
... );
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
facebook> 

facebook> 

facebook> db.users.updateOne({ username: "Laura" }, { $set: { email: "laura.nuevo@email.com" } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
facebook> db.users.updateOne({ username: "Sofia" }, { $set: { email: "sofia.nuevo@email.com" } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
facebook> 

facebook> 

facebook> db.users.updateOne({ username: "Luis" }, { $inc: { age: 5 } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
facebook>  

facebook> db.posts.find().pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8b'),
    title: 'Mi primera publicación',
    body: 'Este es el cuerpo de la primera publicación',
    username: 'Maria',
    comments: [
      { username: 'Carlos', body: 'Gran publicación!' },
      { username: 'Ana', body: 'Muy interesante!' }
    ]
  },
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8f'),
    title: 'Publicación 3',
    body: 'Cuerpo de la publicación 3',
    username: 'Pedro',
    comments: [
      { username: 'Laura', body: 'Comentario modificado' },
      { username: 'Sofia', body: 'Muy útil, gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f90'),
    title: 'Publicación 4',
    body: 'Cuerpo de la publicación 4',
    username: 'Sofia',
    comments: [
      { username: 'Pedro', body: 'Gracias por compartir' },
      { username: 'Laura', body: 'Me gustó mucho' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f91'),
    title: 'Publicación 5',
    body: 'Cuerpo de la publicación 5',
    username: 'Laura',
    comments: [
      { username: 'Pedro', body: 'Interesante lectura' },
      { username: 'Sofia', body: 'Muy claro todo' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f92'),
    title: 'Publicación 6',
    body: 'Cuerpo de la publicación 6',
    username: 'Ana',
    comments: [
      { username: 'Carlos', body: 'Gran explicación' },
      { username: 'Maria', body: 'Muchas gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f93'),
    title: 'Publicación 7',
    body: 'Cuerpo de la publicación 7',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: '¡Muy bueno!' },
      { username: 'Laura', body: 'Buen aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f94'),
    title: 'Publicación 8',
    body: 'Cuerpo de la publicación 8',
    username: 'Clara',
    comments: [
      { username: 'Luis', body: 'Me encantó' },
      { username: 'Laura', body: '¡Gracias por compartir!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f95'),
    title: 'Publicación 9',
    body: 'Cuerpo de la publicación 9',
    username: 'Laura',
    comments: [
      { username: 'Maria', body: 'Muy inspirador' },
      { username: 'Carlos', body: 'Buen contenido' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f96'),
    title: 'Publicación 10',
    body: 'Cuerpo de la publicación 10',
    username: 'Pedro',
    comments: [
      { username: 'Ana', body: 'Muy interesante' },
      { username: 'Carlos', body: 'Gracias por esto' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f97'),
    title: 'Publicación 11',
    body: 'Cuerpo de la publicación 11',
    username: 'Laura',
    comments: [
      { username: 'Luis', body: 'Muy educativo' },
      { username: 'Clara', body: '¡Gracias!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f98'),
    title: 'Publicación 12',
    body: 'Cuerpo de la publicación 12',
    username: 'Sofia',
    comments: [
      { username: 'Laura', body: 'Me ayudó mucho' },
      { username: 'Luis', body: 'Buen post' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9a'),
    title: 'Publicación 14',
    body: 'Cuerpo de la publicación 14',
    username: 'Maria',
    comments: [
      { username: 'Sofia', body: 'Excelente' },
      { username: 'Pedro', body: 'Muy bien explicado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9b'),
    title: 'Publicación 15',
    body: 'Cuerpo de la publicación 15',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: 'Muy útil' },
      { username: 'Laura', body: 'Gracias por compartir' }
    ]
  }
]
facebook> 

facebook> 

facebook> db.posts.find({ username: "Carlos" }).pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  }
]
facebook> 

facebook> 

facebook> db.users.find({ age: { $gt: 20 } }).pretty();
[
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9f'),
    username: 'Luis',
    email: 'luis@email.com',
    age: 31
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa1'),
    username: 'Jose',
    email: 'jose@email.com',
    age: 31
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  }
]
facebook> 

facebook> 

facebook> db.users.find({ age: { $lt: 23 } }).pretty();

facebook> 

facebook> // Usuarios con edad entre 25 y 30

facebook> db.users.find({ age: { $gte: 25, $lte: 30 } }).pretty();
[
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  }
]
facebook> 

facebook> 

facebook> db.users.find().sort({ age: 1 }).pretty();
[
  { _id: ObjectId('6748d45b95d264db706f9f83') },
  { _id: ObjectId('6748d54495d264db706f9f85'), username: 'Catalina' },
  { _id: ObjectId('6748d59995d264db706f9f86'), username: 'Catalina' },
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9f'),
    username: 'Luis',
    email: 'luis@email.com',
    age: 31
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa1'),
    username: 'Jose',
    email: 'jose@email.com',
    age: 31
  }
]
facebook> 

facebook> 

facebook> db.users.find().sort({ age: -1 }).pretty();
[
  {
    _id: ObjectId('6748e66b95d264db706f9f9f'),
    username: 'Luis',
    email: 'luis@email.com',
    age: 31
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa1'),
    username: 'Jose',
    email: 'jose@email.com',
    age: 31
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },

]


facebook> db.users.countDocuments();
17
facebook> 

facebook> 

facebook> db.posts.find({}, { title: 1, _id: 0 }).forEach(post => {
...   print(`Título de la publicación: "${post.title}"`);
... });
Título de la publicación: "Mi primera publicación"
Título de la publicación: "Nuevo título de la publicación"
Título de la publicación: "Publicación actualizada"
Título de la publicación: "Publicación 2"
Título de la publicación: "Publicación 3"
Título de la publicación: "Publicación 4"
Título de la publicación: "Publicación 5"
Título de la publicación: "Publicación 6"
Título de la publicación: "Publicación 7"
Título de la publicación: "Publicación 8"
Título de la publicación: "Publicación 9"
Título de la publicación: "Publicación 10"
Título de la publicación: "Publicación 11"
Título de la publicación: "Publicación 12"
Título de la publicación: "Publicación 13"
Título de la publicación: "Publicación 14"
Título de la publicación: "Publicación 15"

facebook> 

facebook> 

facebook> db.users.find().limit(2).pretty();
[
  { _id: ObjectId('6748d45b95d264db706f9f83') },
  { _id: ObjectId('6748d54495d264db706f9f85'), username: 'Catalina' }
]
facebook> 

facebook>

facebook> db.posts.find({ title: "Publicación 1" }).pretty();

facebook> db.posts.find({ title: "Publicación 2" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  }
]
facebook> 

facebook> db.users.deleteMany({ age: { $gt: 30 } });
{ acknowledged: true, deletedCount: 2 }
facebook> db.users.countDocuments();
15
facebook> db.users.find().pretty();
[
  { _id: ObjectId('6748d54495d264db706f9f85'), username: 'Catalina' },
  { _id: ObjectId('6748d59995d264db706f9f86'), username: 'Catalina' },
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  }
]
facebook> db.posts.countDocuments();
17
facebook> db.posts.find().pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8b'),
    title: 'Mi primera publicación',
    body: 'Este es el cuerpo de la primera publicación',
    username: 'Maria',
    comments: [
      { username: 'Carlos', body: 'Gran publicación!' },
      { username: 'Ana', body: 'Muy interesante!' }
    ]
  },
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8f'),
    title: 'Publicación 3',
    body: 'Cuerpo de la publicación 3',
    username: 'Pedro',
    comments: [
      { username: 'Laura', body: 'Comentario modificado' },
      { username: 'Sofia', body: 'Muy útil, gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f90'),
    title: 'Publicación 4',
    body: 'Cuerpo de la publicación 4',
    username: 'Sofia',
    comments: [
      { username: 'Pedro', body: 'Gracias por compartir' },
      { username: 'Laura', body: 'Me gustó mucho' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f91'),
    title: 'Publicación 5',
    body: 'Cuerpo de la publicación 5',
    username: 'Laura',
    comments: [
      { username: 'Pedro', body: 'Interesante lectura' },
      { username: 'Sofia', body: 'Muy claro todo' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f92'),
    title: 'Publicación 6',
    body: 'Cuerpo de la publicación 6',
    username: 'Ana',
    comments: [
      { username: 'Carlos', body: 'Gran explicación' },
      { username: 'Maria', body: 'Muchas gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f93'),
    title: 'Publicación 7',
    body: 'Cuerpo de la publicación 7',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: '¡Muy bueno!' },
      { username: 'Laura', body: 'Buen aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f94'),
    title: 'Publicación 8',
    body: 'Cuerpo de la publicación 8',
    username: 'Clara',
    comments: [
      { username: 'Luis', body: 'Me encantó' },
      { username: 'Laura', body: '¡Gracias por compartir!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f95'),
    title: 'Publicación 9',
    body: 'Cuerpo de la publicación 9',
    username: 'Laura',
    comments: [
      { username: 'Maria', body: 'Muy inspirador' },
      { username: 'Carlos', body: 'Buen contenido' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f96'),
    title: 'Publicación 10',
    body: 'Cuerpo de la publicación 10',
    username: 'Pedro',
    comments: [
      { username: 'Ana', body: 'Muy interesante' },
      { username: 'Carlos', body: 'Gracias por esto' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f97'),
    title: 'Publicación 11',
    body: 'Cuerpo de la publicación 11',
    username: 'Laura',
    comments: [
      { username: 'Luis', body: 'Muy educativo' },
      { username: 'Clara', body: '¡Gracias!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f98'),
    title: 'Publicación 12',
    body: 'Cuerpo de la publicación 12',
    username: 'Sofia',
    comments: [
      { username: 'Laura', body: 'Me ayudó mucho' },
      { username: 'Luis', body: 'Buen post' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9a'),
    title: 'Publicación 14',
    body: 'Cuerpo de la publicación 14',
    username: 'Maria',
    comments: [
      { username: 'Sofia', body: 'Excelente' },
      { username: 'Pedro', body: 'Muy bien explicado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9b'),
    title: 'Publicación 15',
    body: 'Cuerpo de la publicación 15',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: 'Muy útil' },
      { username: 'Laura', body: 'Gracias por compartir' }
    ]
  }
]
facebook> db.posts.find({ title: "Publicación actualizada" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  }
]
facebook> db.posts.find({ title: "Publicación 2" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  }
]
facebook> db.users.find({ username: { $in: ["Laura", "Sofia"] } }).pretty();
[
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  }
]
facebook> db.users.find({ username: "Luis" }).pretty();

facebook> db.posts.find().pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8b'),
    title: 'Mi primera publicación',
    body: 'Este es el cuerpo de la primera publicación',
    username: 'Maria',
    comments: [
      { username: 'Carlos', body: 'Gran publicación!' },
      { username: 'Ana', body: 'Muy interesante!' }
    ]
  },
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8f'),
    title: 'Publicación 3',
    body: 'Cuerpo de la publicación 3',
    username: 'Pedro',
    comments: [
      { username: 'Laura', body: 'Comentario modificado' },
      { username: 'Sofia', body: 'Muy útil, gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f90'),
    title: 'Publicación 4',
    body: 'Cuerpo de la publicación 4',
    username: 'Sofia',
    comments: [
      { username: 'Pedro', body: 'Gracias por compartir' },
      { username: 'Laura', body: 'Me gustó mucho' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f91'),
    title: 'Publicación 5',
    body: 'Cuerpo de la publicación 5',
    username: 'Laura',
    comments: [
      { username: 'Pedro', body: 'Interesante lectura' },
      { username: 'Sofia', body: 'Muy claro todo' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f92'),
    title: 'Publicación 6',
    body: 'Cuerpo de la publicación 6',
    username: 'Ana',
    comments: [
      { username: 'Carlos', body: 'Gran explicación' },
      { username: 'Maria', body: 'Muchas gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f93'),
    title: 'Publicación 7',
    body: 'Cuerpo de la publicación 7',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: '¡Muy bueno!' },
      { username: 'Laura', body: 'Buen aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f94'),
    title: 'Publicación 8',
    body: 'Cuerpo de la publicación 8',
    username: 'Clara',
    comments: [
      { username: 'Luis', body: 'Me encantó' },
      { username: 'Laura', body: '¡Gracias por compartir!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f95'),
    title: 'Publicación 9',
    body: 'Cuerpo de la publicación 9',
    username: 'Laura',
    comments: [
      { username: 'Maria', body: 'Muy inspirador' },
      { username: 'Carlos', body: 'Buen contenido' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f96'),
    title: 'Publicación 10',
    body: 'Cuerpo de la publicación 10',
    username: 'Pedro',
    comments: [
      { username: 'Ana', body: 'Muy interesante' },
      { username: 'Carlos', body: 'Gracias por esto' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f97'),
    title: 'Publicación 11',
    body: 'Cuerpo de la publicación 11',
    username: 'Laura',
    comments: [
      { username: 'Luis', body: 'Muy educativo' },
      { username: 'Clara', body: '¡Gracias!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f98'),
    title: 'Publicación 12',
    body: 'Cuerpo de la publicación 12',
    username: 'Sofia',
    comments: [
      { username: 'Laura', body: 'Me ayudó mucho' },
      { username: 'Luis', body: 'Buen post' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9a'),
    title: 'Publicación 14',
    body: 'Cuerpo de la publicación 14',
    username: 'Maria',
    comments: [
      { username: 'Sofia', body: 'Excelente' },
      { username: 'Pedro', body: 'Muy bien explicado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9b'),
    title: 'Publicación 15',
    body: 'Cuerpo de la publicación 15',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: 'Muy útil' },
      { username: 'Laura', body: 'Gracias por compartir' }
    ]
  }
]
facebook> db.posts.find({ username: "Carlos" }).pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  }
]
facebook> db.users.find({ age: { $gt: 20 } }).pretty();
[
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  }
]
facebook> db.users.find({ age: { $gte: 25, $lte: 30 } }).pretty();
[
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  }
]
facebook> db.users.find().sort({ age: 1 }).pretty();
[
  { _id: ObjectId('6748d54495d264db706f9f85'), username: 'Catalina' },
  { _id: ObjectId('6748d59995d264db706f9f86'), username: 'Catalina' },
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  }
]
facebook> db.users.countDocuments();
15
facebook> db.posts.find({}, { title: 1, _id: 0 }).forEach(post => {
...     print(`Título de la publicación: "${post.title}"`);
... });
Título de la publicación: "Mi primera publicación"
Título de la publicación: "Nuevo título de la publicación"
Título de la publicación: "Publicación actualizada"
Título de la publicación: "Publicación 2"
Título de la publicación: "Publicación 3"
Título de la publicación: "Publicación 4"
Título de la publicación: "Publicación 5"
Título de la publicación: "Publicación 6"
Título de la publicación: "Publicación 7"
Título de la publicación: "Publicación 8"
Título de la publicación: "Publicación 9"
Título de la publicación: "Publicación 10"
Título de la publicación: "Publicación 11"
Título de la publicación: "Publicación 12"
Título de la publicación: "Publicación 13"
Título de la publicación: "Publicación 14"
Título de la publicación: "Publicación 15"

facebook> db.users.find().limit(2).pretty();
[
  { _id: ObjectId('6748d45b95d264db706f9f83') },
  { _id: ObjectId('6748d54495d264db706f9f85'), username: 'Catalina' }
]
facebook> db.posts.find({ title: "Publicación 1" }).pretty();

facebook> db.posts.find({ title: "Publicación 2" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  }
]
facebook> db.users.find({ age: { $gt: 30 } }).pretty();

facebook> db.users.deleteMany({
...   $and: [
...     { username: { $exists: false } },
...     { email: { $exists: false } },
...     { age: { $exists: false } }
...   ]
... });
{ acknowledged: true, deletedCount: 1 }
facebook> db.users.insertMany([
...   {
...     username: "Luis",
...     email: "luis.nuevo@email.com",
...     age: 24
...   },
...   {
...     username: "Isabel",
...     email: "isabel.nueva@email.com",
...     age: 23
...   },
...   {
...     username: "Ricardo",
...     email: "ricardo.nuevo@email.com",
...     age: 22
...   }
... ]);
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6748ea8d95d264db706f9fa6'),
    '1': ObjectId('6748ea8d95d264db706f9fa7'),
    '2': ObjectId('6748ea8d95d264db706f9fa8')
  }
}
facebook> db.users.find({
...   $and: [
...     { username: { $exists: false } },
...     { email: { $exists: false } },
...     { age: { $exists: false } }
...   ]
... });

facebook> db.users.find().sort({ age: 1 }).pretty();
[
  { _id: ObjectId('6748d54495d264db706f9f85'), username: 'Catalina' },
  { _id: ObjectId('6748d59995d264db706f9f86'), username: 'Catalina' },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa8'),
    username: 'Ricardo',
    email: 'ricardo.nuevo@email.com',
    age: 22
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa7'),
    username: 'Isabel',
    email: 'isabel.nueva@email.com',
    age: 23
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa6'),
    username: 'Luis',
    email: 'luis.nuevo@email.com',
    age: 24
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  }
]
facebook> db.users.countDocuments();
17
facebook> db.users.find({
...   $or: [
...     { username: { $exists: false } },
...     { email: { $exists: false } },
...     { age: { $exists: false } }
...   ]
... }).pretty();
[
  { _id: ObjectId('6748d54495d264db706f9f85'), username: 'Catalina' },
  { _id: ObjectId('6748d59995d264db706f9f86'), username: 'Catalina' }
]
facebook> db.users.deleteOne({ _id: ObjectId('6748d54495d264db706f9f85') });
{ acknowledged: true, deletedCount: 1 }
facebook> db.users.deleteOne({ _id: ObjectId('6748d59995d264db706f9f86') });
{ acknowledged: true, deletedCount: 1 }
facebook> db.users.find({
...   $or: [
...     { username: { $exists: false } },
...     { email: { $exists: false } },
...     { age: { $exists: false } }
...   ]
... }).pretty();

facebook> db.users.countDocuments();
15
facebook> db.users.insertMany([
...   {
...     username: "Andrea",
...     email: "andrea.nueva@email.com",
...     age: 24
...   },
...   {
...     username: "Pablo",
...     email: "pablo.nuevo@email.com",
...     age: 25
...   }
... ]);
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6748eb6395d264db706f9fa9'),
    '1': ObjectId('6748eb6395d264db706f9faa')
  }
}
facebook> db.users.countDocuments();
17
facebook> db.users.find().pretty();
[
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa6'),
    username: 'Luis',
    email: 'luis.nuevo@email.com',
    age: 24
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa7'),
    username: 'Isabel',
    email: 'isabel.nueva@email.com',
    age: 23
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa8'),
    username: 'Ricardo',
    email: 'ricardo.nuevo@email.com',
    age: 22
  },
  {
    _id: ObjectId('6748eb6395d264db706f9fa9'),
    username: 'Andrea',
    email: 'andrea.nueva@email.com',
    age: 24
  },
  {
    _id: ObjectId('6748eb6395d264db706f9faa'),
    username: 'Pablo',
    email: 'pablo.nuevo@email.com',
    age: 25
  }
]
facebook> db.posts.countDocuments();
17
facebook> db.posts.find().pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8b'),
    title: 'Mi primera publicación',
    body: 'Este es el cuerpo de la primera publicación',
    username: 'Maria',
    comments: [
      { username: 'Carlos', body: 'Gran publicación!' },
      { username: 'Ana', body: 'Muy interesante!' }
    ]
  },
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8f'),
    title: 'Publicación 3',
    body: 'Cuerpo de la publicación 3',
    username: 'Pedro',
    comments: [
      { username: 'Laura', body: 'Comentario modificado' },
      { username: 'Sofia', body: 'Muy útil, gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f90'),
    title: 'Publicación 4',
    body: 'Cuerpo de la publicación 4',
    username: 'Sofia',
    comments: [
      { username: 'Pedro', body: 'Gracias por compartir' },
      { username: 'Laura', body: 'Me gustó mucho' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f91'),
    title: 'Publicación 5',
    body: 'Cuerpo de la publicación 5',
    username: 'Laura',
    comments: [
      { username: 'Pedro', body: 'Interesante lectura' },
      { username: 'Sofia', body: 'Muy claro todo' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f92'),
    title: 'Publicación 6',
    body: 'Cuerpo de la publicación 6',
    username: 'Ana',
    comments: [
      { username: 'Carlos', body: 'Gran explicación' },
      { username: 'Maria', body: 'Muchas gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f93'),
    title: 'Publicación 7',
    body: 'Cuerpo de la publicación 7',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: '¡Muy bueno!' },
      { username: 'Laura', body: 'Buen aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f94'),
    title: 'Publicación 8',
    body: 'Cuerpo de la publicación 8',
    username: 'Clara',
    comments: [
      { username: 'Luis', body: 'Me encantó' },
      { username: 'Laura', body: '¡Gracias por compartir!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f95'),
    title: 'Publicación 9',
    body: 'Cuerpo de la publicación 9',
    username: 'Laura',
    comments: [
      { username: 'Maria', body: 'Muy inspirador' },
      { username: 'Carlos', body: 'Buen contenido' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f96'),
    title: 'Publicación 10',
    body: 'Cuerpo de la publicación 10',
    username: 'Pedro',
    comments: [
      { username: 'Ana', body: 'Muy interesante' },
      { username: 'Carlos', body: 'Gracias por esto' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f97'),
    title: 'Publicación 11',
    body: 'Cuerpo de la publicación 11',
    username: 'Laura',
    comments: [
      { username: 'Luis', body: 'Muy educativo' },
      { username: 'Clara', body: '¡Gracias!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f98'),
    title: 'Publicación 12',
    body: 'Cuerpo de la publicación 12',
    username: 'Sofia',
    comments: [
      { username: 'Laura', body: 'Me ayudó mucho' },
      { username: 'Luis', body: 'Buen post' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9a'),
    title: 'Publicación 14',
    body: 'Cuerpo de la publicación 14',
    username: 'Maria',
    comments: [
      { username: 'Sofia', body: 'Excelente' },
      { username: 'Pedro', body: 'Muy bien explicado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9b'),
    title: 'Publicación 15',
    body: 'Cuerpo de la publicación 15',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: 'Muy útil' },
      { username: 'Laura', body: 'Gracias por compartir' }
    ]
  }
]
facebook> db.posts.find({ title: "Publicación actualizada" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  }
]
facebook> db.posts.find({ title: "Publicación 2" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  }
]
facebook> db.posts.find({ title: "Publicación 3" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8f'),
    title: 'Publicación 3',
    body: 'Cuerpo de la publicación 3',
    username: 'Pedro',
    comments: [
      { username: 'Laura', body: 'Comentario modificado' },
      { username: 'Sofia', body: 'Muy útil, gracias' }
    ]
  }
]
facebook> db.users.find({ username: { $in: ["Laura", "Sofia"] } }).pretty();
[
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  }
]
facebook> db.users.find({ username: "Luis" }).pretty();
[
  {
    _id: ObjectId('6748ea8d95d264db706f9fa6'),
    username: 'Luis',
    email: 'luis.nuevo@email.com',
    age: 24
  }
]
facebook> db.posts.find().pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8b'),
    title: 'Mi primera publicación',
    body: 'Este es el cuerpo de la primera publicación',
    username: 'Maria',
    comments: [
      { username: 'Carlos', body: 'Gran publicación!' },
      { username: 'Ana', body: 'Muy interesante!' }
    ]
  },
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8f'),
    title: 'Publicación 3',
    body: 'Cuerpo de la publicación 3',
    username: 'Pedro',
    comments: [
      { username: 'Laura', body: 'Comentario modificado' },
      { username: 'Sofia', body: 'Muy útil, gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f90'),
    title: 'Publicación 4',
    body: 'Cuerpo de la publicación 4',
    username: 'Sofia',
    comments: [
      { username: 'Pedro', body: 'Gracias por compartir' },
      { username: 'Laura', body: 'Me gustó mucho' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f91'),
    title: 'Publicación 5',
    body: 'Cuerpo de la publicación 5',
    username: 'Laura',
    comments: [
      { username: 'Pedro', body: 'Interesante lectura' },
      { username: 'Sofia', body: 'Muy claro todo' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f92'),
    title: 'Publicación 6',
    body: 'Cuerpo de la publicación 6',
    username: 'Ana',
    comments: [
      { username: 'Carlos', body: 'Gran explicación' },
      { username: 'Maria', body: 'Muchas gracias' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f93'),
    title: 'Publicación 7',
    body: 'Cuerpo de la publicación 7',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: '¡Muy bueno!' },
      { username: 'Laura', body: 'Buen aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f94'),
    title: 'Publicación 8',
    body: 'Cuerpo de la publicación 8',
    username: 'Clara',
    comments: [
      { username: 'Luis', body: 'Me encantó' },
      { username: 'Laura', body: '¡Gracias por compartir!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f95'),
    title: 'Publicación 9',
    body: 'Cuerpo de la publicación 9',
    username: 'Laura',
    comments: [
      { username: 'Maria', body: 'Muy inspirador' },
      { username: 'Carlos', body: 'Buen contenido' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f96'),
    title: 'Publicación 10',
    body: 'Cuerpo de la publicación 10',
    username: 'Pedro',
    comments: [
      { username: 'Ana', body: 'Muy interesante' },
      { username: 'Carlos', body: 'Gracias por esto' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f97'),
    title: 'Publicación 11',
    body: 'Cuerpo de la publicación 11',
    username: 'Laura',
    comments: [
      { username: 'Luis', body: 'Muy educativo' },
      { username: 'Clara', body: '¡Gracias!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f98'),
    title: 'Publicación 12',
    body: 'Cuerpo de la publicación 12',
    username: 'Sofia',
    comments: [
      { username: 'Laura', body: 'Me ayudó mucho' },
      { username: 'Luis', body: 'Buen post' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9a'),
    title: 'Publicación 14',
    body: 'Cuerpo de la publicación 14',
    username: 'Maria',
    comments: [
      { username: 'Sofia', body: 'Excelente' },
      { username: 'Pedro', body: 'Muy bien explicado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f9b'),
    title: 'Publicación 15',
    body: 'Cuerpo de la publicación 15',
    username: 'Luis',
    comments: [
      { username: 'Clara', body: 'Muy útil' },
      { username: 'Laura', body: 'Gracias por compartir' }
    ]
  }
]
facebook> db.posts.find({ username: "Carlos" }).pretty();
[
  {
    _id: ObjectId('6748de0d95d264db706f9f8c'),
    title: 'Nuevo título de la publicación',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      {
        username: 'Maria',
        body: 'Este comentario ha sido actualizado por Maria'
      },
      { username: 'Ana', body: 'Me encanta!' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8d'),
    title: 'Publicación actualizada',
    body: 'Cuerpo actualizado',
    username: 'Carlos',
    comments: [
      { username: 'Laura', body: 'Comentario actualizado' },
      { username: 'Sofia', body: 'Otro comentario actualizado' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  },
  {
    _id: ObjectId('6748e62795d264db706f9f99'),
    title: 'Publicación 13',
    body: 'Cuerpo de la publicación 13',
    username: 'Carlos',
    comments: [
      { username: 'Ana', body: 'Interesante' },
      { username: 'Laura', body: '¡Gran trabajo!' }
    ]
  }
]
facebook> db.users.find({ age: { $gt: 20 } }).pretty();
[
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa6'),
    username: 'Luis',
    email: 'luis.nuevo@email.com',
    age: 24
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa7'),
    username: 'Isabel',
    email: 'isabel.nueva@email.com',
    age: 23
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa8'),
    username: 'Ricardo',
    email: 'ricardo.nuevo@email.com',
    age: 22
  },
  {
    _id: ObjectId('6748eb6395d264db706f9fa9'),
    username: 'Andrea',
    email: 'andrea.nueva@email.com',
    age: 24
  },
  {
    _id: ObjectId('6748eb6395d264db706f9faa'),
    username: 'Pablo',
    email: 'pablo.nuevo@email.com',
    age: 25
  }
]
facebook> db.users.find({ age: { $lt: 23 } }).pretty();
[
  {
    _id: ObjectId('6748ea8d95d264db706f9fa8'),
    username: 'Ricardo',
    email: 'ricardo.nuevo@email.com',
    age: 22
  }
]
facebook> db.users.find({ age: { $lt: 23 } }).pretty();
[
  {
    _id: ObjectId('6748ea8d95d264db706f9fa8'),
    username: 'Ricardo',
    email: 'ricardo.nuevo@email.com',
    age: 22
  }
]
facebook> db.users.find().sort({ age: 1 }).pretty();
[
  {
    _id: ObjectId('6748ea8d95d264db706f9fa8'),
    username: 'Ricardo',
    email: 'ricardo.nuevo@email.com',
    age: 22
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa7'),
    username: 'Isabel',
    email: 'isabel.nueva@email.com',
    age: 23
  },
  {
    _id: ObjectId('6748eb6395d264db706f9fa9'),
    username: 'Andrea',
    email: 'andrea.nueva@email.com',
    age: 24
  },
  {
    _id: ObjectId('6748ea8d95d264db706f9fa6'),
    username: 'Luis',
    email: 'luis.nuevo@email.com',
    age: 24
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9c'),
    username: 'Pedro',
    email: 'pedro.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa4'),
    username: 'Manuel',
    email: 'manuel@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748eb6395d264db706f9faa'),
    username: 'Pablo',
    email: 'pablo.nuevo@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9d'),
    username: 'Sofia',
    email: 'sofia.nuevo@email.com',
    age: 26
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa5'),
    username: 'Fernanda',
    email: 'fernanda@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9f9e'),
    username: 'Laura',
    email: 'laura.nuevo@email.com',
    age: 27
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa2'),
    username: 'Karla',
    email: 'karla@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f8a'),
    username: 'Ana',
    email: 'ana.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa0'),
    username: 'Clara',
    email: 'clara@email.com',
    age: 29
  },
  {
    _id: ObjectId('6748e66b95d264db706f9fa3'),
    username: 'Diana',
    email: 'diana@email.com',
    age: 30
  },
  {
    _id: ObjectId('6748dd5895d264db706f9f89'),
    username: 'Carlos',
    email: 'carlos.nuevo@email.com',
    age: 30
  }
]
facebook> db.users.countDocuments();
17
facebook> db.users.find().limit(2).pretty();
[
  {
    _id: ObjectId('6748dcde95d264db706f9f87'),
    username: 'Juan',
    email: 'juan@email.com',
    age: 25
  },
  {
    _id: ObjectId('6748dcde95d264db706f9f88'),
    username: 'Maria',
    email: 'maria.nueva@email.com',
    age: 28
  }
]
facebook> db.posts.find({ title: "Publicación 1" }).pretty();

facebook> db.posts.find({ title: "Publicación 2" }).pretty();
[
  {
    _id: ObjectId('6748e62795d264db706f9f8e'),
    title: 'Publicación 2',
    body: 'Nuevo cuerpo de la publicación',
    username: 'Carlos',
    comments: [
      { username: 'Maria', body: 'Estoy de acuerdo' },
      { username: 'Ana', body: 'Gran aporte' }
    ]
  }
]
facebook> db.users.find({ age: { $gt: 30 } }).pretty();

facebook> 

