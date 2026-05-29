
DHCP

Antes de instalar los servicios, configuramos una IP estática en la interfaz de red principal ens37. El archivo de configuración que editamos fue /etc/netplan/00-installer-config.yaml. En la configuración inicial establecimos la dirección 192.168.10.10/24 y el servidor DNS en esa misma IP. Posteriormente, añadimos la dirección en bucle local 127.0.0.1 para la resolución interna del propio servidor. 

<img width="745" height="168" alt="image" src="https://github.com/user-attachments/assets/efe5dcdb-5026-4f25-aa67-6c4cd0861299" />

Para la instalación del servicio ejecutamos el comando sudo apt install isc-dhcp-server. 

<img width="745" height="35" alt="image" src="https://github.com/user-attachments/assets/cd8b45b4-36b3-490b-ab5b-6d3cb87b09be" />

La configuración de la interfaz de escucha la realizamos en el archivo /etc/default/isc-dhcp-server, donde definimos la variable INTERFACESv4 como "ens37". 

<img width="745" height="363" alt="image" src="https://github.com/user-attachments/assets/3f27422f-1493-4a7b-8930-f3ae16eb8180" />

La configuración global y de la subred la gestionamos en el archivo /etc/dhcp/dhcpd.conf 

<img width="752" height="238" alt="image" src="https://github.com/user-attachments/assets/271d2400-3c86-4ec8-aee2-11fac90700b9" />

Tras aplicar los cambios, reiniciamos el servicio con el comando sudo systemctl restart isc-dhcp-server y verificamos su estado activo y en ejecución mediante sudo systemctl status isc-dhcp-server. 

<img width="748" height="293" alt="image" src="https://github.com/user-attachments/assets/dabc1157-3134-450a-8d4b-afeb088db841" />




DNS

Instalamos los paquetes necesarios mediante el comando sudo apt install bind9 bind9utils bind9-doc. 

<img width="731" height="32" alt="image" src="https://github.com/user-attachments/assets/8b441f47-6f9e-4443-9eac-740fb7422613" />

En el archivo /etc/bind/named.conf.local declaramos las zonas maestra directa e inversa 

<img width="751" height="172" alt="image" src="https://github.com/user-attachments/assets/bfb9e846-7a59-417a-81d2-e81257115460" />

La base de datos de la zona directa la creamos copiando la plantilla db.local mediante el comando sudo cp /etc/bind/db.local /etc/bind/db.corestack.local 

<img width="750" height="368" alt="image" src="https://github.com/user-attachments/assets/25769cb4-51b2-459c-9358-bd42386e2172" />

La base de datos de la zona inversa la generamos copiando la plantilla db.127 mediante el comando sudo cp /etc/bind/db.127 /etc/bind/db.192.168.10. 

<img width="745" height="25" alt="image" src="https://github.com/user-attachments/assets/4e866a57-e23d-4092-b212-bac3440cede6" />

<img width="751" height="215" alt="image" src="https://github.com/user-attachments/assets/cb81f687-5811-46da-b41a-7cd6ac4998a9" />

Para la resolución de nombres externos, modificamos el archivo /etc/bind/named.conf.options introduciendo en la sección forwarders las direcciones de los servidores DNS públicos 8.8.8.8 y 1.1.1.1. 

<img width="747" height="319" alt="image" src="https://github.com/user-attachments/assets/29efa28e-395e-414e-9b52-ee8988fe3724" />

Para asegurar el correcto funcionamiento, validamos la sintaxis del archivo de configuración general con sudo named-checkconf y la zona específica con sudo named-checkzone corestack.local /etc/bind/db.corestack.local, obteniendo un resultado correcto antes de reiniciar el servicio con sudo systemctl restart bind9. 

<img width="1022" height="99" alt="image" src="https://github.com/user-attachments/assets/81f3e1af-5888-4665-b31c-ec2d26f751d8" />

<img width="684" height="35" alt="image" src="https://github.com/user-attachments/assets/2c4dfadc-8a99-426d-a2fb-e9ee21a721c2" />

La comprobación final de la resolución la efectuamos con el comando nslookup www.corestack.local, que nos devolvió de manera correcta la dirección IP 192.168.10.55. 

<img width="754" height="153" alt="image" src="https://github.com/user-attachments/assets/09f52cc0-2340-4ea8-af81-3a073cc667d9" />

Con el objetivo de permitir el acceso a internet a los equipos de la red interna, instalamos la herramienta para la persistencia de reglas con sudo apt update && sudo apt install iptables-persistent.

<img width="752" height="35" alt="image" src="https://github.com/user-attachments/assets/9ce8c75e-d4c9-4e79-93cc-66a5f03d9131" />

Aplicamos una regla de enmascaramiento en la interfaz de salida WAN ens33 mediante sudo iptables -t nat -A POSTROUTING -o ens33 -j MASQUERADE. 
Habilitamos el reenvío de paquetes entre la interfaz interna ens37 y la externa ens33 

<img width="601" height="50" alt="image" src="https://github.com/user-attachments/assets/430d1837-b9af-441b-8c6a-33001a18e76b" />
