Instalamos prometheus-node-exporter tanto en el servidor web como en el servidor DHCP y DNS.

<img width="743" height="32" alt="image" src="https://github.com/user-attachments/assets/b35500cf-d9b8-49ba-b16e-b811fbb7c25a" />

Una vez finalizada la instalación, procedimos a habilitar y arrancar el servicio en segundo plano, asegurándonos de que estuviera correctamente activo.

<img width="841" height="207" alt="image" src="https://github.com/user-attachments/assets/996b19f3-0d29-40c4-b1c9-3323cdc8a1dd" />

Creamos un archivo docker-compose.yml donde definimos la infraestructura de dos servicios.

<img width="820" height="482" alt="image" src="https://github.com/user-attachments/assets/7366c5f5-ebb2-45be-b2b9-cc621c4b55bb" />

Editamos el archivo prometheus.yml y configuramos los trabajos de node-exporter y blackbox.

<img width="747" height="453" alt="image" src="https://github.com/user-attachments/assets/23bab7ec-6790-423c-a83f-1c8b44867217" />

Interfaz Prometheus

<img width="854" height="291" alt="image" src="https://github.com/user-attachments/assets/9888b5f8-d966-4142-ab7d-14e1e9f8ff69" />

Dashboards Grafana

<img width="753" height="174" alt="image" src="https://github.com/user-attachments/assets/2d92b38c-9567-40e2-b8f9-08d54edb303e" />

Web

<img width="1015" height="386" alt="image" src="https://github.com/user-attachments/assets/d95a0cde-40a3-4db0-809b-337130e51460" />

Servidor Web

<img width="1452" height="530" alt="image" src="https://github.com/user-attachments/assets/73f00ae3-830e-41c7-805a-f267749d72f3" />
<img width="1447" height="275" alt="image" src="https://github.com/user-attachments/assets/ab42fb2d-32cf-48e6-b446-c75fa8dc563d" />

Servidor DHCP-DNS

<img width="1453" height="524" alt="image" src="https://github.com/user-attachments/assets/9d97edf7-bcb4-47cb-99e8-2db5bc5dd67d" />
<img width="1448" height="271" alt="image" src="https://github.com/user-attachments/assets/47ecb921-7627-4ff9-a720-da8665b71399" />
