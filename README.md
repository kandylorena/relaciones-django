# relaciones-django

## 🚀 Pasos Realizados para la Configuración y Pruebas del Proyecto

A continuación se detallan los pasos cronológicos seguidos para el levantamiento del entorno de desarrollo, la integración con la base de datos y la manipulación de datos a través del ORM de Django.

---

### 1. Infraestructura con Docker
* **Orquestación de Contenedores:** Se creó el archivo `docker-compose.yml` para levantar un entorno aislado con dos servicios clave:
  * **PostgreSQL (v17):** Base de datos relacional del proyecto, configurada inicialmente con credenciales por defecto y posteriormente ajustada a la base de datos definitiva (`relaciones`).
  * **pgAdmin 4:** Herramienta web para la administración gráfica de la base de datos (mapeada en el puerto `5050`).

* **Despliegue:** Se inicializó el entorno ejecutando el comando `docker-compose up --build`.

### 2. Configuración del Entorno de Python y Django
* **Entorno Virtual:** Se inicializó y activó un entorno virtual (`venv`) para el aislamiento de dependencias.
* **Dependencias:** Se instaló **Django** y el adaptador de PostgreSQL **`psycopg2-binary`**, guardando el registro final en el archivo `requirements.txt`.
* **Inicialización:** * Se creó el proyecto base de Django llamado `config`.
  * Se creó la aplicación interna `relaciones` y se registró correctamente dentro del arreglo `INSTALLED_APPS` en el archivo `settings.py`.
* **Conexión a la Base de Datos:** Se modificó el diccionario `DATABASES` en `settings.py` vinculándolo con los parámetros, credenciales y puerto (`5432`) definidos previamente en el contenedor de Docker.

### 3.  Modelos y Migraciones
* **Diseño de Modelos:** Se programaron las estructuras de datos en `models.py` abarcando los tres tipos de relaciones principales:
  * **Uno a Muchos (`ForeignKey`):** `Categoria` y `Producto`.
  * **Muchos a Muchos (`ManyToManyField`):** `Curso` y `Estudiante`.
  * **Uno a Uno (`OneToOneField`):** `Usuario` y `Perfil`.
* **Sincronización:** Se ejecutó `python manage.py makemigrations` para empaquetar los modelos y `python manage.py migrate` para impactar y crear las tablas físicas directamente en PostgreSQL.
* **Verificación:** Se accedió a pgAdmin en el navegador (`localhost:5050`) para registrar el servidor y validar visualmente la creación de las tablas de Django.

### 4. Manipulación de Datos a través de Django Shell
Se abrió la consola interactiva mediante `python manage.py shell` para realizar pruebas CRUD (Crear, Leer, Actualizar, Borrar) y experimentar con las relaciones del ORM:

* **Operaciones CRUD Básicas:** Creación de instancias con `.objects.create()`, lectura selectiva con `.get()`, listado general con `.all()`, modificaciones guardadas con `.save()` o `.update()`, y eliminaciones mediante `.delete()`.
* **Relaciones Uno a Muchos:** Uso de consultas inversas con el sufijo implícito `_set` (ej. `categoria.producto_set.all()`) y su respectiva lectura dinámica mediante ciclos `for`.
* **Relaciones Muchos a Muchos:** Pruebas de asignación y desasignación de registros cruzados mediante el uso de los métodos `.add()`, `.remove()`, y la limpieza masiva con `.clear()`.
* **Relaciones Uno a Uno:** Vinculación directa de perfiles a usuarios, demostrando el comportamiento de la relación bidireccional directa (ej. `perfil.usuario.nombre` y `usuario.perfil`).


comandos usado 
docker-compose up --build (Levanta la base de datos y pgAdmin en segundo plano)

python -m venv venv (Crea el entorno virtual)

source venv/bin/activate (Activa el entorno en Linux/macOS. En Windows usa: source venv/Scripts/activate)

pip install --upgrade pip (Actualiza pip)

pip install django psycopg2-binary (Instala Django y el conector de Postgres)

pip freeze > requirements.txt (Guarda las dependencias instaladas)

django-admin startproject config . (Crea el proyecto base en la carpeta actual)

python manage.py startapp relaciones (Crea la aplicación para tus modelos)

python manage.py migrate (Aplica las tablas base iniciales de Django)

python manage.py makemigrations (Genera los archivos de migración tras escribir tus modelos)

python manage.py migrate (Crea tus tablas de relaciones en PostgreSQL)

python manage.py shell (Abre la consola interactiva para poblar y probar los datos)

exit() (Sale de la consola interactiva de Django)


#enlace git https://github.com/kandylorena/relaciones-django.git