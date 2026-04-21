# Plataforma de Oficios y Changas (MVP)

Este proyecto es un sistema web unificado para la intermediación de trabajos informales y oficios ("changas"), diseñado inicialmente para uso local con capacidad de escalabilidad mediante geolocalización.

## 1. Documento de Visión y Arquitectura

### Declaración del Problema
La contratación de oficios y trabajos informales se realiza de forma desordenada a través de redes sociales genéricas. Esto genera fricción, falta de un sistema de reputación confiable y dificultad para filtrar por disponibilidad y cercanía geográfica.

### Solución Propuesta
Un marketplace asimétrico de doble entrada donde la entidad principal es el `Usuario`, capaz de ejecutar ambos roles (Ofertante y Demandante) con la misma cuenta. El sistema filtra y renderiza ofertas y demandas basándose estrictamente en la ubicación geográfica.

### Stack Tecnológico
* **Backend:** PHP (v8.1+) con framework Laravel.
* **Frontend:** Livewire (SPA feel) y Tailwind CSS.
* **Base de Datos:** MySQL / PostgreSQL.
* **Infraestructura:** Docker (Laravel Sail).

---

## 2. Guía de Instalación con Docker (Laravel Sail)

El proyecto está completamente dockerizado. No necesitas instalar PHP, Node ni MySQL en tu máquina.

### Requisitos Previos
1. [Git](https://git-scm.com/downloads)
2. [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Asegurate de que esté abierto y corriendo antes de seguir)

### Paso 1: Clonar el repositorio
Abrí la terminal y ejecutá:
```bash
git clone [https://github.com/TU_USUARIO/changas-app.git](https://github.com/TU_USUARIO/changas-app.git)
cd changas-app
Paso 2: Instalar dependencias iniciales (Vendor)
Como no tenés PHP local, usamos un contenedor temporal de Docker para descargar los paquetes de Laravel. Ejecutá este comando exactamente como está:

En Linux / Mac:

Bash
docker run --rm -u "$(id -u):$(id -g)" -v "$(pwd):/var/www/html" -w /var/www/html laravelsail/php82-composer:latest composer install --ignore-platform-reqs
En Windows (PowerShell):

PowerShell
docker run --rm -v ${PWD}:/var/www/html -w /var/www/html laravelsail/php82-composer:latest composer install --ignore-platform-reqs
Paso 3: Configurar el archivo de Entorno (.env)
Tenés que crear tu copia del archivo de configuración:

Bash
cp .env.example .env
(En Windows usando CMD/PowerShell, el comando es copy .env.example .env)

Abrí el archivo .env nuevo y asegurate de que la conexión a la base de datos apunte al contenedor de Docker (generalmente ya viene así por defecto, pero verificalo):

Fragmento de código
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=changas_db
DB_USERNAME=sail
DB_PASSWORD=password
Paso 4: Levantar los contenedores
A partir de ahora, todos los comandos se ejecutan a través de Laravel Sail. Levantá la infraestructura en segundo plano (-d):

Bash
./vendor/bin/sail up -d
Paso 5: Preparar la Aplicación
Con los contenedores corriendo, generamos la clave de la app y creamos las tablas en la base de datos:

Bash
./vendor/bin/sail artisan key:generate
./vendor/bin/sail artisan migrate
Paso 6: Compilar el Frontend
Instalá los paquetes de JavaScript y dejá corriendo el compilador para ver los cambios en tiempo real:

Bash
./vendor/bin/sail npm install
./vendor/bin/sail npm run dev