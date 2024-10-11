# Configurar OSRM Localmente con Docker

Esta guía te ayudará a configurar Open Source Routing Machine (OSRM) localmente en tu máquina utilizando Docker. Usarás Docker para ejecutar un backend de OSRM para obtener rutas de *drive* y *walk*, lo que te permitirá consultar tiempos de viaje entre varias ubicaciones.

## 1. Instalar Docker

Para usar OSRM localmente, primero necesitas instalar Docker en tu máquina. Sigue las instrucciones a continuación según tu sistema operativo:

- **Para Windows**:  
  Descarga e instala Docker Desktop desde [este enlace](https://www.docker.com/products/docker-desktop/). Después de la instalación, asegúrate de que Docker esté funcionando abriendo Docker Desktop.

- **Para macOS**:  
  Descarga e instala Docker Desktop desde [este enlace](https://www.docker.com/products/docker-desktop/). Una vez instalado, puedes abrir Docker Desktop desde tu carpeta de Aplicaciones.

- **Para Linux**:  
  Instala Docker siguiendo las instrucciones oficiales para tu distribución desde [este enlace](https://docs.docker.com/engine/install/). Asegúrate de habilitar y ejecutar Docker después de la instalación.

Una vez que Docker esté instalado y corriendo, ya puedes proceder con la configuración de OSRM.

## 2. Descargar los Archivos de OSRM

Debes descargar los archivos necesarios para correr OSRM en tu computadora. Puedes encontrar estos archivos en el siguiente enlace de Google Drive:

[Enlace a los Archivos de OSRM](https://*drive*.google.com) 

Descarga y descomprime los archivos en una carpeta local en tu máquina.

## 3. Correr OSRM para Drive y Walk

Para correr OSRM, usa los siguientes comandos en tu terminal. Debes ajustar la ruta de la carpeta donde guardaste los archivos descargados.

### OSRM para Drive

Abre el terminal y ejecuta el siguiente comando (cambia la ruta `/ruta/a/tu/carpeta/OSRMData_Drive` por la ruta donde descargaste los datos):

```bash
docker run -t -i -p 5001:5000 -v /ruta/a/tu/carpeta/OSRMData_Drive:/data osrm/osrm-backend osrm-routed --algorithm ch --max-table-size 1000000 /data/chile-latest.osrm --mmap=0
```

Este comando correrá el servidor de OSRM para rutas *drive* en el puerto 5001.

### OSRM para Walk
Ahora, para rutas *walk*, ejecuta el siguiente comando en el terminal (cambia la ruta /ruta/a/tu/carpeta/OSRMData_Walk por la ubicación correcta):

```bash
docker run -t -i -p 5002:5000 -v /ruta/a/tu/carpeta/OSRMData_Walk:/data osrm/osrm-backend osrm-routed --algorithm ch --max-table-size 1000000 /data/chile-latest.osrm --mmap=0
```
Esto correrá el servidor de OSRM para rutas *walk* en el puerto 5002.

## 4. Cómo Probar
Después de ejecutar estos comandos, los servidores de OSRM estarán activos en tu máquina:

Drive: El servidor estará disponible en http://localhost:5001

Walk: El servidor estará disponible en http://localhost:5002

Puedes probarlos enviando solicitudes desde tu navegador o con alguna herramienta como Postman.

## 5. Notas Importantes
Asegúrate de tener Docker corriendo cada vez que quieras utilizar OSRM.
Si tienes problemas con los puertos, asegúrate de que no estén siendo utilizados por otros servicios.
¡Y eso es todo! Ya deberías tener tu OSRM corriendo localmente usando Docker.