Markdown
# Plataforma de Oficios y Changas (MVP)

Este proyecto es un sistema web unificado para la intermediación de trabajos informales y oficios ("changas"), diseñado inicialmente para uso local con capacidad de escalabilidad mediante geolocalización.

## 1. Documento de Visión y Arquitectura

### Declaración del Problema
La contratación de oficios y trabajos informales (limpieza, mantenimiento, soldadura, fletes) suele realizarse de forma desordenada a través de redes sociales genéricas. Esto genera fricción en la contratación, falta de un sistema de reputación confiable y dificultad para filtrar por disponibilidad y cercanía geográfica.

### Solución Propuesta
Un marketplace asimétrico de doble entrada donde la entidad principal es el `Usuario`, quien puede ejecutar ambos roles (Ofertante y Demandante) sin necesidad de tener cuentas separadas. El sistema filtra y renderiza ofertas y demandas basándose estrictamente en la ubicación geográfica (ciudad/barrio) seleccionada o detectada.

### Stack Tecnológico
* **Backend:** PHP (v8.1+) con framework Laravel.
* **Frontend:** Livewire (para interactividad SPA sin recargar página) y Tailwind CSS.
* **Base de Datos:** MySQL / PostgreSQL.
* **Distribución:** Arquitectura orientada a PWA (Progressive Web App).

---

## 2. Guía de Instalación para Desarrollo Local

A continuación, se detallan los pasos necesarios para levantar el entorno de desarrollo local desde cero.

### Requisitos Previos
Asegurate de tener instalados los siguientes programas:
- [PHP](https://www.php.net/downloads) (v8.1 o superior)
- [Composer](https://getcomposer.org/) (Gestor de dependencias de PHP)
- [Node.js y npm](https://nodejs.org/) (Gestor de paquetes de JavaScript)
- Motor de Base de Datos (MySQL, MariaDB o PostgreSQL)
- Git

### Paso 1: Clonar el repositorio
Abrí la terminal en el directorio donde quieras guardar el proyecto y ejecutá:
```bash
git clone [https://github.com/TU_USUARIO/changas-app.git](https://github.com/TU_USUARIO/changas-app.git)
cd changas-app
Paso 2: Instalar dependencias del Backend (PHP)
Descarga todas las librerías de Laravel necesarias.

Bash
composer install
Paso 3: Instalar dependencias del Frontend (Node)
Descarga las herramientas para compilar Tailwind CSS y el JavaScript.

Bash
npm install
Paso 4: Configurar el archivo de Entorno (.env)
Laravel usa un archivo .env para manejar la configuración local de la base de datos y otras variables. Este archivo no se sube al repositorio por seguridad.

Tenés que crear tu propia copia a partir del archivo de ejemplo:

Bash
cp .env.example .env
(En Windows usando CMD, el comando es copy .env.example .env)

Paso 5: Generar la Key de la Aplicación
Genera una clave criptográfica única para tu entorno local.

Bash
php artisan key:generate
Paso 6: Configurar la Base de Datos
Abrí tu gestor de base de datos (phpMyAdmin, DBeaver, o consola) y creá una base de datos vacía llamada changas_db (o el nombre que prefieras).

Abrí el archivo .env que creaste en el Paso 4.

Actualizá estas líneas con los datos de tu conexión local:

Fragmento de código
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=changas_db
DB_USERNAME=tu_usuario_local
DB_PASSWORD=tu_contraseña_local
Paso 7: Ejecutar las Migraciones
Crea todas las tablas necesarias en tu base de datos local.

Bash
php artisan migrate
Paso 8: Levantar los servidores locales
Para que la aplicación funcione y recompile los estilos en tiempo real, necesitás correr dos procesos en la terminal al mismo tiempo (abrí dos pestañas en tu consola).

Terminal 1: Servidor de PHP (Laravel)

Bash
php artisan serve
(Esto levantará la web en http://localhost:8000)

Terminal 2: Compilador de Frontend (Vite/Tailwind)

Bash
npm run dev
Una vez que ambos estén corriendo, ingresá a http://localhost:8000 en tu navegador.


***

Con esto, el repo ya queda documentado de punta a punta. ¿Hacés el `git commit` de este archivo y pasamos a armar el modelo de la base de datos para la gestión dual de usuarios y la geolocalización?