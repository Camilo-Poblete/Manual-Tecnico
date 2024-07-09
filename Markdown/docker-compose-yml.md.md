```yaml

version: '3.8'

  

services:

  postgres:

    image: postgres:latest

    restart: always

    environment:

      POSTGRES_DB: jsonplaceholder_data

      POSTGRES_USER: postgres

      POSTGRES_PASSWORD: 1234567890

    ports:

      - "5432:5432"

    volumes:

      - postgres_data:/var/lib/postgresql/data

    networks:

      - dem

  

  pgadmin:

    image: dpage/pgadmin4:latest

    restart: always

    environment:

      PGADMIN_DEFAULT_EMAIL: admin@admin.com

      PGADMIN_DEFAULT_PASSWORD: pgadmin

      PGADMIN_LISTEN_PORT: 80

    ports:

      - "5000:80"

    depends_on:

      - postgres

    networks:

      - dem

  

  json_app:

    container_name: jsonplaceholder_container

    build:

      context: .

      dockerfile: Dockerfile

    environment:

      - DB_HOST=postgres

      - DB_DATABASE=jsonplaceholder_data

      - DB_USER=postgres

      - DB_PASSWORD=1234567890

      - DB_PORT=5432

    depends_on:

      - postgres

    networks:

      - dem

    command: ["python", "jsonplaceholder.py"]  # Comando para ejecutar el script Python

  

networks:

  dem:

    driver: bridge

  

volumes:

  postgres_data:

  
  
  
  

### Explicación del `docker-compose.yml`:

  

#### Servicio `postgres`:

- **Imagen**: Utiliza la imagen `postgres:latest`.

- **Reinicio**: Configurado para reiniciar siempre (`restart: always`).

- **Variables de entorno**:

  - `POSTGRES_DB`: Nombre de la base de datos, configurado como `jsonplaceholder_data`.

  - `POSTGRES_USER`: Usuario de PostgreSQL, configurado como `postgres`.

  - `POSTGRES_PASSWORD`: Contraseña del usuario de PostgreSQL, configurada como `1234567890`.

- **Puertos**: Mapea el puerto `5432` del contenedor PostgreSQL al puerto `5432` del host.

- **Volúmenes**: Monta un volumen `postgres_data` para persistir los datos de PostgreSQL.

- **Redes**: Se conecta a la red `dem`.

  
  
  

#### Servicio `pgadmin`:

- **Imagen**: Utiliza la imagen `dpage/pgadmin4:latest`.

- **Reinicio**: Configurado para reiniciar siempre (`restart: always`).

- **Variables de entorno**:

  - `PGADMIN_DEFAULT_EMAIL`: Correo electrónico por defecto para pgAdmin, configurado como `admin@admin.com`.

  - `PGADMIN_DEFAULT_PASSWORD`: Contraseña por defecto para pgAdmin, configurada como `pgadmin`.

  - `PGADMIN_LISTEN_PORT`: Puerto en el cual pgAdmin escucha, configurado como `80`.

- **Puertos**: Mapea el puerto `80` del contenedor pgAdmin al puerto `5000` del host.

- **Dependencias**: Depende del servicio `postgres`.

- **Redes**: Se conecta a la red `dem`.

  
  
  

