Para empezar, instalamos Docker de forma automatizada descargando y ejecutando su script oficial. Tras verificar el correcto funcionamiento de las herramientas mediante la comprobación de la versión de Docker Compose.

<img width="590" height="33" alt="image" src="https://github.com/user-attachments/assets/3640426c-f3bb-47d5-8a87-1252b055996f" />

<img width="514" height="48" alt="image" src="https://github.com/user-attachments/assets/4247f55d-7863-4f47-86bb-cf5f7093cb0f" />

La infraestructura del servidor web la definimos al completo dentro del archivo docker-compose.yml, estructurando tres servicios principales.

<img width="652" height="504" alt="image" src="https://github.com/user-attachments/assets/2af7959b-b52a-4489-aacb-2eef6bbd06ed" />

Para mantener la seguridad y separar las credenciales del código de orquestación, almacenamos los datos sensibles en un archivo independiente llamado file.env. En este archivo definimos la contraseña del administrador de la base de datos, el nombre de la base de datos mysql_db y el usuario con sus claves correspondientes. Asimismo, introdujimos los parámetros de conexión requeridos por WordPress para enlazarse de forma interna con el puerto del contenedor de la base de datos.

<img width="595" height="142" alt="image" src="https://github.com/user-attachments/assets/f7136b8b-7366-43be-8df5-25bc08ad420a" />

El comportamiento del proxy inverso lo determinamos editando el archivo nginx.conf. Dentro del bloque de escucha del puerto 80 para el dominio local , añadimos una sección de redirección que transfiere las peticiones entrantes directamente al puerto interno de nuestro contenedor de aplicaciones WordPress. En esta misma sección incluimos las cabeceras proxy necesarias para reenviar de forma transparente la IP real del cliente y el protocolo original. Adicionalmente, incrementamos el parámetro de tamaño máximo del cuerpo de las peticiones a 64M, una directiva crucial para permitir la subida de imágenes, temas o plugins pesados dentro de la plataforma sin sufrir bloqueos.

<img width="587" height="224" alt="image" src="https://github.com/user-attachments/assets/7fd2a8f3-0a3e-4160-9202-f02c9c691e65" />

Una vez que levantamos todos los servicios en la red, accedimos a la interfaz del asistente de configuración. Durante este proceso rellenamos los datos principales de la infraestructura web, definiendo el título del sitio como ProyectoFBM, creando el usuario administrador, estableciendo las contraseñas de acceso.

<img width="545" height="577" alt="image" src="https://github.com/user-attachments/assets/bade7b88-16ed-4a2b-8bde-46e53e4e9d88" />

Finalmente, entramos al panel de administración del gestor de contenidos para realizar el diseño visual inicial de la identidad corporativa mediante la herramienta Elementor. Durante esta fase subimos y configuramos el logotipo del sitio con la plantilla CoreStack , estructuramos los menús de navegación principales y definimos la paleta de colores global para mantener la homogeneidad visual en todos los encabezados, enlaces y fondos del portal.

<img width="605" height="221" alt="image" src="https://github.com/user-attachments/assets/d1592e67-afa9-4e7a-897b-e6e9644b03ff" />

<img width="195" height="222" alt="image" src="https://github.com/user-attachments/assets/0f96e1d8-78c3-4e1f-891a-b0762d603f0d" />

<img width="220" height="531" alt="image" src="https://github.com/user-attachments/assets/46678357-644a-4ff6-9c06-8beaf79b6593" />

<img width="1178" height="511" alt="image" src="https://github.com/user-attachments/assets/3671e1f2-4254-4997-93fb-d6cca79ba5a3" />
