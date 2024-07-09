# Guía Paso a Paso para Crear y Ejecutar una Aplicación Docker con PostgreSQL y Python

## 1. Configuración del Proyecto

### 1.1. Crear el Directorio del Proyecto
Crea un directorio para tu proyecto y navega hasta él:
```bash
mkdir jsonplaceholder
cd jsonplaceholder


# Instala las dependencias necesarias
pip install certifi==2024.7.4
pip install charset-normalizer==3.3.2
pip install idna==3.7
pip install psycopg2==2.9.9
pip install psycopg2-binary==2.9.9
pip install requests==2.32.3
pip install urllib3==2.2.2

# Genera el archivo requirements.txt con las dependencias instaladas
pip freeze > requirements.txt




# Usar la imagen base de Python
FROM python:3.12

# Establecer el directorio de trabajo en el contenedor
WORKDIR /app

# Copiar el archivo requirements.txt y el script Python al contenedor
COPY requirements.txt requirements.txt
COPY jsonplaceholder.py jsonplaceholder.py

# Instalar las dependencias
RUN pip install --no-cache-dir -r requirements.txt

# Comando para ejecutar el script Python
CMD ["python", "jsonplaceholder.py"]





