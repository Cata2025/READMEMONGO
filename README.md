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

<img width="951" alt="Captura de pantalla 2024-11-29 a las 1 13 26" src="https://github.com/user-attachments/assets/3ddb6b04-faec-4f45-8ce4-6a1eb43a6643">



