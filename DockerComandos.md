# Comprehensive Docker Cheatsheet

## Gestión de Imágenes

### Construir imágenes
```bash
docker build -t nombre_imagen:tag .
docker build -t nombre_imagen:tag -f Dockerfile.custom .
```

### Listar imágenes
```bash
docker images
docker image ls
```

### Eliminar imágenes
```bash
docker rmi imagen_id
docker image rm imagen_id
docker image prune  # Elimina imágenes sin usar
docker image prune -a  # Elimina todas las imágenes sin usar
```

### Inspeccionar imágenes
```bash
docker image inspect imagen_id
```

### Etiquetar imágenes
```bash
docker tag imagen_id nuevo_nombre:tag
```

### Guardar y cargar imágenes
```bash
docker save imagen > imagen.tar
docker load < imagen.tar
```

### Publicar imágenes
```bash
docker push nombre_usuario/nombre_imagen:tag
```

## Gestión de Contenedores

### Crear y ejecutar contenedores
```bash
docker run imagen
docker run -it --name mi_contenedor imagen  # Interactivo con nombre
docker run -d imagen  # En segundo plano
docker run -p 8080:80 imagen  # Mapeo de puertos
docker run -v /ruta/local:/ruta/contenedor imagen  # Montar volumen
```

### Listar contenedores
```bash
docker ps  # Contenedores en ejecución
docker ps -a  # Todos los contenedores
```

### Iniciar, detener y reiniciar contenedores
```bash
docker start contenedor_id
docker stop contenedor_id
docker restart contenedor_id
```

### Eliminar contenedores
```bash
docker rm contenedor_id
docker rm $(docker ps -aq)  # Eliminar todos los contenedores detenidos
```

### Ejecutar comandos en contenedores
```bash
docker exec -it contenedor_id comando
docker exec -it contenedor_id /bin/bash
```

### Logs de contenedores
```bash
docker logs contenedor_id
docker logs -f contenedor_id  # Seguir logs en tiempo real
```

### Copiar archivos
```bash
docker cp archivo.txt contenedor_id:/ruta/destino
docker cp contenedor_id:/ruta/origen/archivo.txt ./
```

### Inspeccionar contenedores
```bash
docker inspect contenedor_id
```

### Estadísticas de uso
```bash
docker stats
docker top contenedor_id
```

## Redes Docker

### Crear una red
```bash
docker network create mi_red
```

### Listar redes
```bash
docker network ls
```

### Conectar un contenedor a una red
```bash
docker network connect mi_red contenedor_id
```

### Desconectar un contenedor de una red
```bash
docker network disconnect mi_red contenedor_id
```

### Inspeccionar una red
```bash
docker network inspect mi_red
```

## Volúmenes Docker

### Crear un volumen
```bash
docker volume create mi_volumen
```

### Listar volúmenes
```bash
docker volume ls
```

### Inspeccionar un volumen
```bash
docker volume inspect mi_volumen
```

### Eliminar un volumen
```bash
docker volume rm mi_volumen
```

## Docker Compose

### Iniciar servicios
```bash
docker-compose up
docker-compose up -d  # En segundo plano
```

### Detener servicios
```bash
docker-compose down
```

### Construir o reconstruir servicios
```bash
docker-compose build
```

### Ver logs de servicios
```bash
docker-compose logs
```

### Ejecutar un comando en un servicio
```bash
docker-compose run servicio comando
```

## Limpieza y Mantenimiento

### Eliminar todos los recursos no utilizados
```bash
docker system prune
```

### Ver el uso de disco
```bash
docker system df
```

### Limpiar caché de construcción
```bash
docker builder prune
```

## Comandos Avanzados

### Crear una nueva imagen a partir de un contenedor
```bash
docker commit contenedor_id nueva_imagen:tag
```

### Exportar/Importar contenedores
```bash
docker export contenedor_id > contenedor.tar
cat contenedor.tar | docker import - nueva_imagen:tag
```

### Historial de una imagen
```bash
docker history imagen_id
```

### Esperar a que un contenedor termine
```bash
docker wait contenedor_id
```

### Pausar/Reanudar un contenedor
```bash
docker pause contenedor_id
docker unpause contenedor_id
```

### Crear un punto de control de un contenedor
```bash
docker checkpoint create contenedor_id checkpoint_name
```
### Configurar un contenedor Docker para que se inicie automáticamente
Always: El contenedor se reiniciará siempre, independientemente del estado de salida.  
```bash
docker run --name mi_contenedor --restart always -d mi_imagen:latest
```  
On-failure: El contenedor se reiniciará solo si sale con un código de error. Puedes especificar el número máximo de intentos de reinicio.  
```bash
docker run --name mi_contenedor --restart on-failure:5 -d mi_imagen:latest
```  
Unless-stopped: El contenedor se reiniciará a menos que sea detenido manualmente.  
```bash
docker run --name mi_contenedor --restart unless-stopped -d mi_imagen:latest
```  
Never: El contenedor no se reiniciará.  
```bash
docker run --name mi_contenedor --restart never -d mi_imagen:latest
```