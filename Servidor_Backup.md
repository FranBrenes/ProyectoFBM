Para garantizar un entorno aislado y ordenado, comenzamos creando un directorio dedicado al proyecto donde inicializamos y activamos un entorno virtual de Python(sin que el sistema nos solicitara contraseñas de manera constante).

<img width="579" height="137" alt="image" src="https://github.com/user-attachments/assets/df26607a-9478-4822-bc00-df73f1987b0b" />

Generamos un par de claves criptográficas SSH (pública y privada) con un cifrado de 4096 bits en los servidores DHCP-DNS y Web y en servidor de Backups. Posteriormente, transferimos la clave pública hacia nuestro servidor de almacenamiento, permitiendo así una autenticación automatizada y segura entre ambas máquinas a través de la red local.

<img width="764" height="513" alt="image" src="https://github.com/user-attachments/assets/81841d12-c436-4624-b95a-ea7b5c18f3a5" />

Desarrollamos un script principal en Python encargado de realizar las copias de seguridad periódicas de los servicios.

Define de forma estructurada los nombres de los volúmenes de Docker que contienen la información y las rutas locales del servidor.
Obtiene la fecha y hora exacta del sistema para renombrar los archivos.
Comprime los archivos en formato tar.
Transfiere los archivos generados desde el servidor de producción hacia el almacenamiento del servidor de backups.
Realiza una limpieza eliminando los archivos temporales creados en el servidor web para no saturar el disco.

<img width="600" height="307" alt="image" src="https://github.com/user-attachments/assets/5d538f1d-1841-432f-9628-13b0960ef783" />

<img width="603" height="30" alt="image" src="https://github.com/user-attachments/assets/ee1df119-75fc-4062-b5dd-8205198e47c2" />

Programamos un segundo script en Python enfocado en la recuperación de backups.

Muestra un menú en la terminal que nos permite elegir entre restaurar la base de datos o el código web de la aplicación.
Tras seleccionar la opción deseada, el script busca y detecta de manera automática cuál es el archivo de respaldo más reciente almacenado en el disco del servidor de backups.
Para evitar conflictos de permisos de escritura directa sobre los volúmenes de Docker, el sistema transfiere primero el archivo comprimido a un directorio temporal del usuario remoto.

<img width="693" height="418" alt="image" src="https://github.com/user-attachments/assets/713aa575-642b-4fc7-abae-1e07b9d8458b" />

<img width="672" height="78" alt="image" src="https://github.com/user-attachments/assets/ee5463bb-0755-4adc-ac08-cd7e68b29664" />

