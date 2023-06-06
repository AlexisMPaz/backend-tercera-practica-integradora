# Backend Proyecto Final para CoderHouse

Comisión: 39685
Alumno: Alexis Paz

Version node.js: 18.16.0

Antes de iniciar la aplicacion se debe instalar las dependencias con:

- npm i

**Las variables de entorno necesarias se encuentran en la entrega por la plataforma de Coder**
- Se ha agregado los datos del Admin a las variables de entorno

Para iniciar el servidor (script):

* (puerto 8080, entorno desarrollo): npm run dev

* (puerto 4000, entorno produccion): npm run prod

Para iniciar el frontend (Next.js 13):
- npm run dev

**POSTMAN**

Para testear la aplicacion con postman se debe agregar en los request, el header:
key: Origin         value: http://localhost:3000 (IMPORTANTE)
Tambien se puede comentar el codigo de cors para que no entre en conflicto con los request pero es necesario para que funcione el frontend asi que no se recomienda.

**tercera Practica Integradora**

## Backend

**Usuarios premium**

- Nuevo role para usuarios premium que permite agregar productos, modificar y elimar esos productos propios. No puede modificar productos que no son propios y tampoco puede agregar al carrito productos propios.

- El usuario admin tiene permisos para modificar y eliminar productos creados por un usuario premium.

- El schema de productos cuenta con un campo owner que referencia el id del usuario premium que lo creo o null si es un producto creado por admin.

Nueva ruta: ("api/users/premium/:uid") permite cambiar el rol de un usario comun a premiun y viceversa. El admin puede cambiarle el rol a cualquier usuario mintras que los usaurios comunes y premium solo pueden a ellos mismos. No tiene mucho sentido que el usuario pueda cambiarse el role pero es que faltaria un muro de pago o algo asi.

**Sistema de recuperacion de contraseña**

- Realizado un sistema de recuperacion usando nodemailer y jwt. Se puede testear todo desde POSTMAN, mandar en el body de la ruta reset, la nueva contraseña junto al token que se encuentra en el link del mail.

Nuevas Rutas:

- POST: "api/session/password/forgot" 
Recibe por el body el mail, comprueba que existe el usuario y crea un token que es enviado dentro de un mail al correo electronico del usuario.

(formato: {email})

- POST: "api/session/password/reset" 
Recibe por el body la nueva contraseña y el token, hace las validaciones correspondientes, como la verificacion de la token y que existe el usuario cuyo id fue guardado en la token, por ultimo se fija que la nueva contraseña no sea la misma a la antigua y si todo es correcto se actualiza el usario.

Formato del body: ({newPassword: "contraseña", token: "Aqui va el token de la url del link"})

## Frontend

- Se agregaron vistas simples para la recuperacion de contraseña. El boton en el login para recuperar contraseña te lleva a un formulario donde ingresar el email.

- El link del email te lleva a la vista para cambiar la contraseña.

- Le falta mucho trabajo a las vistas pero la funcionalidad basica esta.

- Para testear la recuperacion de contraseña crear un usuario con POSTMAN primero.

**Usuario para testear**
- rol "Usuario":
email: damian@gmail.com
password: damian1234

- rol "Admin":
Email y password en las variables de entorno.