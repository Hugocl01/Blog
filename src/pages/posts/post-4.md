---
layout: ../../layouts/MarkdownPostLayout.astro
title: Introducción a Composer
author: Hugo Cayón Laso
description: "Una guía rápida para instalar y usar Composer en proyectos PHP"
image:
    url: "https://getcomposer.org/img/logo-composer-transparent2.png"
    alt: "Logo de Composer"
pubDate: 2024-09-29
readingTime: 10 min
tags: ["PHP", "Composer", "Backend", "Desarrollo web"]
---

## Introducción

Composer es una herramienta de gestión de dependencias para PHP, que permite manejar librerías y paquetes externos en tus proyectos de manera eficiente. En este post, aprenderás a instalar Composer, configurarlo y usarlo para administrar dependencias en tus aplicaciones PHP.

## Requisitos previos

Antes de comenzar, asegúrate de cumplir con los siguientes requisitos:

1. **PHP instalado:** Composer requiere que tengas PHP en tu sistema. Si seguiste mi [guía de instalación de PHP con XAMPP](post-3), ya deberías tener PHP funcionando correctamente.
2. **Conexión a Internet:** Composer descarga las librerías desde repositorios en línea, por lo que necesitarás una conexión activa.

### Instalación de Composer

Sigue estos pasos para instalar Composer en tu sistema:

1. Dirígete a la [página oficial de Composer](https://getcomposer.org/download/) y descarga el instalador que corresponda a tu sistema operativo.
2. Si estás en Windows, ejecuta el archivo `.exe` descargado y sigue las instrucciones del asistente de instalación. Asegúrate de que el instalador detecte la ruta correcta de PHP (por ejemplo, `C:\xampp\php\php.exe` si usas XAMPP).
3. Para sistemas **Linux** o **macOS**, abre la terminal y ejecuta los siguientes comandos para descargar e instalar Composer globalmente:

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
```

4. Verifica que Composer esté instalado correctamente ejecutando **composer --version** en tu terminal. Deberías ver la versión de Composer instalada.

### Uso básico de Composer
Crear un proyecto PHP con Composer

Para crear un nuevo proyecto PHP usando Composer, sigue estos pasos:
 
1. Abre tu terminal y navega a la carpeta donde deseas crear tu proyecto.
2. Ejecuta el siguiente comando para iniciar un nuevo proyecto:

```bash
composer init
```

Composer te pedirá que ingreses información básica como el nombre del proyecto, la descripción y otros detalles opcionales.
Añadir dependencias

Ejemplo:

```bash
$ composer init
This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>): myvendor/myproject
Description []: Mi primer proyecto con Composer
Author [Your Name <you@example.com>, n to skip]: Hugo Cayón Laso <hugocayon@example.com>
Minimum Stability []: stable
Define your dependencies.
Use a comma to separate multiple packages.
Would you like to define your dependencies (require) now? (yes/no) [yes]: yes
Enter the packages you would like to add (or leave blank to skip): 
Package 1: phpmailer/phpmailer
Would you like to define your dev dependencies (require-dev) now? (yes/no) [no]: yes
Enter the packages you would like to add (or leave blank to skip): 
Package 1: phpunit/phpunit
What is the license of the package? (e.g. MIT, PSR-2) [proprietary]: MIT
Confirm changes made:
{
    "name": "myvendor/myproject",
    "description": "Mi primer proyecto con Composer",
    "require": {
        "phpmailer/phpmailer": "^6.9.2"
    },
    "require-dev": {
        "phpunit/phpunit": "^9.0"
    },
    "authors": [
        {
            "name": "Hugo Cayón Laso",
            "email": "hugocayon@example.com"
        }
    ],
    "minimum-stability": "stable",
    "license": "MIT"
}
Do you confirm generation? (yes/no) [yes]: yes
```

Una vez confirmado se creara un archivo **composer.json** similar a este:

```json
{
    "name": "myvendor/myproject",
    "description": "Mi primer proyecto con Composer",
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    },
    "require": {
        "phpmailer/phpmailer": "^6.9.2"
    },
    "require-dev": {
        "phpunit/phpunit": "^9.0"
    },
    "authors": [
        {
            "name": "Hugo Cayón Laso",
            "email": "hugocayon@example.com"
        }
    ],
    "minimum-stability": "stable",
    "license": "MIT"
}
```

Una de las características principales de Composer es su capacidad para manejar dependencias. Para instalar una nueva librería, usa el comando require seguido del nombre del paquete. Por ejemplo, para añadir PHPMailer, una popular biblioteca de PHP que se utiliza para enviar correos electrónicos, ejecuta:

```bash
composer require phpmailer/phpmailer
```

Composer descargará la librería y la añadirá al archivo composer.json, donde se listan todas las dependencias del proyecto.
Autoloading

Composer también facilita el autoloading de las clases en tu proyecto, evitando tener que incluir manualmente cada archivo PHP. Una vez que has instalado dependencias, puedes incluir el archivo autoload.php generado por Composer en tu proyecto de la siguiente manera:

```php
require 'vendor/autoload.php';
```

Este archivo se encuentra en la carpeta vendor, que es donde Composer almacena las librerías descargadas.

### Comandos basico de Composer

Actualizando dependencias

Para mantener tus librerías actualizadas, simplemente ejecuta el siguiente comando:

```bash
composer update
```

Composer revisará las versiones más recientes de las dependencias en el archivo composer.json y las actualizará si es necesario.