---
layout: ../../layouts/MarkdownPostLayout.astro
title: Primeros pasos en PHP
author: Hugo Cayón Laso
description: "Una guia rápida a cerca de la instalación y configuración de un entorno de desarrollo en PHP"
image:
    url: "https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/PHP-logo.svg/1067px-PHP-logo.svg.png"
    alt: "Miniatura de los rayos de Astro."
pubDate: 2024-09-22
readingTime : 3 min
tags: ["PHP", "Backend", "Desarrollo web"]
---

## Introducción

Para comenzar a programar con PHP, el primer paso es tener un entorno de desarrollo. En este caso, elegiré Visual Studio Code, además de instalar XAMPP, ya que este software instalará un servidor Apache y MySQL.

## Requisitos previos

Antes de empezar, es importante asegurarse de que cuentas con los siguientes elementos instalados en tu máquina:

1. **Visual Studio Code (VS Code):** Un editor de código ligero pero potente. Puedes descargarlo desde [aquí](https://code.visualstudio.com/).
2. **XAMPP:** Un paquete que incluye Apache, MySQL y PHP, lo que facilita la configuración de un entorno de desarrollo completo. Puedes descargar XAMPP desde su [sitio oficial](https://www.apachefriends.org/es/index.html).

### Instalando Visual Studio Code

1. Dirígete a la [página oficial de VS Code](https://code.visualstudio.com/) y descarga la versión correspondiente a tu sistema operativo.
2. Sigue las instrucciones del asistente de instalación. Una vez instalado, abre el programa y personaliza la interfaz a tu gusto instalando las extensiones necesarias.

#### Extensiones recomendadas para PHP en VS Code

- **PHP Intelephense:** Ofrece autocompletado, resaltado de sintaxis y herramientas de análisis de código.
- **PHP Debug:** Permite depurar tus aplicaciones PHP directamente en VS Code.

Para instalar estas extensiones:
1. Abre VS Code y dirígete al menú de **Extensiones** (icono de cuadrados en la barra lateral izquierda).
2. Busca las extensiones mencionadas y haz clic en "Instalar".

### Instalando XAMPP

1. Ve al [sitio oficial de XAMPP](https://www.apachefriends.org/es/index.html) y descarga el instalador que corresponda a tu sistema operativo.
2. Ejecuta el instalador y sigue los pasos del asistente. Asegúrate de seleccionar **Apache** y **MySQL** durante el proceso de instalación.

Una vez instalado XAMPP:
- Abre el **Panel de control de XAMPP** y asegúrate de iniciar los módulos de **Apache** y **MySQL**. Apache será tu servidor local para ejecutar PHP y MySQL te permitirá gestionar bases de datos.

---

## Configurando el entorno PHP

### Verificando la instalación de PHP

Para asegurarte de que PHP está correctamente instalado en tu entorno, abre el **Panel de control de XAMPP** y enciende el servidor Apache. Luego, crea un archivo PHP simple para verificar:

1. Ve al directorio donde instalaste XAMPP, normalmente `C:\xampp\htdocs\`.
2. Crea una carpeta para tu proyecto, por ejemplo `mi-primer-proyecto`.
3. Dentro de esta carpeta, crea un archivo llamado `index.php` con el siguiente contenido:

```php
<?php
    echo "¡Hola, mundo!";
?>
```

4. Abre tu navegador y escribe en la barra de direcciones http://localhost/mi-primer-proyecto/. Si ves el mensaje "¡Hola, mundo!" en la pantalla, tu entorno está listo para trabajar con PHP.

## Conclusión

¡Y ahí lo tienes! Has dado tus primeros pasos en el mundo de PHP configurando un entorno de desarrollo con Visual Studio Code y XAMPP. Ahora puedes comenzar a explorar y crear tus propias aplicaciones web dinámicas.

Espero que este artículo te haya sido útil y que estés emocionado por comenzar tu aventura en PHP. ¡Gracias por leer y mucho éxito en tus proyectos! ¡Nos vemos en la próxima! 😊