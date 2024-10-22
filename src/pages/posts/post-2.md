---
layout: ../../layouts/MarkdownPostLayout.astro
title: Cómo creé mi blog con Astro
author: Hugo Cayón Laso
description: "Un recorrido detallado por el proceso de creación de mi blog utilizando Astro."
image:
    url: "https://docs.astro.build/assets/arc.webp"
    alt: "Miniatura de los arcos de Astro."
pubDate: 2024-08-12
readingTime: 11 min
tags: ["Astro", "JavaScript", "HTML", "CSS", "Frontend", "Desarrollo web"]
---

## Introducción

Crear un blog puede parecer una tarea complicada, pero con las herramientas adecuadas, es un proceso bastante sencillo y divertido. En este artículo, compartiré mi experiencia al construir mi blog personal utilizando [Astro](https://astro.build), un moderno framework para construir sitios web rápidos y eficientes.

## ¿Por qué Astro?

Después de investigar varias opciones para construir mi blog, decidí usar Astro por varias razones:

- **Velocidad**: Astro genera sitios estáticos, lo que resulta en tiempos de carga increíblemente rápidos.
- **Flexibilidad**: Puedes usar componentes de cualquier framework como React, Vue o Svelte junto con Markdown.
- **Simplicidad**: La configuración inicial es muy simple, y su documentación es excelente.
- **Eficiencia**: Astro es muy eficiente al tratar contenido estatico.

## El proceso de creación

Ya que tenia conocimientos a cerca de como usar Astro comentare los aspectos fundamentales en la creación del blog, ya que como ayuda segui el [Tutorial: Construye un Blog](https://docs.astro.build/es/tutorial/0-introduction/) de la documentación oficial de Astro y hay ciertas cosas que son diferenes.

### 1. Instalación de Astro

El primer paso fue instalar Astro en mi máquina. Para ello, utilicé el siguiente comando:

```bash
npm create astro@latest
```

En las siguientes pantallas, decidí usar una plantilla vacía "Empty", que no usaría TypeScript y que deseaba instalar todas las dependencias, además de inicializar un repositorio, ya que para tener un control de versiones he usado Git y GitHub.

## 2. Creación de Layouts

En este paso, creo los layouts, que son los componentes esenciales que definen la estructura general que rodea a todo el contenido de nuestra web. Decidí crear los dos layouts siguientes:

### 2.1 BaseLayout.astro

El layout `BaseLayout.astro` es utilizado para toda la página, en el que están la etiqueta &lt;head&gt; con los &lt;meta&gt; y los &lt;link&gt;.

```astro
---
import Header from "../components/Header.astro"; // Importa el componente Header
import Footer from "../components/Footer.astro"; // Importa el componente Footer
import ThemeChange from "../components/ThemeChange.astro"; // Importa el componente que cambia el tema
import "../styles/global.css"; // Importa la hoja de CSS

const { pageTitle } = Astro.props;
---

<html lang="es">
    <head>
        <meta charset="utf-8" />
        <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
        <meta name="viewport" content="width=device-width" />
        <meta name="generator" content={Astro.generator} />
        <title>{pageTitle}</title>
    </head>
    <body>
        <Header />
        <main>
            <slot />
        </main>
        <Footer />
        <ThemeChange />
        <script>
            import "../scripts/menu.js";
        </script>
    </body>
</html>
```

### 2.2 MarkdownPostLayout.astro

EL layout `MarkdownPostLayout.astro` lo uso para dar formato a cada post escrito en Markdown y este es envuelto por el layout anterior.

```astro
---
import BaseLayout from "./BaseLayout.astro"; // Importa el layout base para la página
import { Picture } from "astro:assets"; // Importa el componente Picture para manejar imágenes
const { frontmatter } = Astro.props; // Extrae las propiedades de frontmatter
---

<BaseLayout pageTitle={frontmatter.title}>
    <section>
        {/* Encabezado del artículo */}
        <header>
            <h1>{frontmatter.title}</h1>
            {/* Título del artículo */}
            <p><em>{frontmatter.description}</em></p>
            {/* Descripción del artículo */}
            <p>Escrito por: {frontmatter.author}{/* Autor del artículo */}</p>
            <p>{frontmatter.pubDate.toString().slice(0, 10)}</p>
            {/* Fecha de publicación */}
            <p>Tiempo de lectura: {frontmatter.readingTime}</p>
            {/* Tiempo estimado de lectura */}
        </header>

        {/* Imagen destacada */}
        <Picture
            src={frontmatter.image.url}
            alt={frontmatter.image.alt}
            format="avif"
            inferSize={true}
            widths={frontmatter.image.width}
            decoding="async"
            loading="lazy"
        />
        {/* Etiquetas del artículo */}
        <div class="tags">
            {
                frontmatter.tags.map((tag) => (
                    <a href={`/tags/${tag}`} class="tag">
                        #{tag}
                    </a>
                ))
            }
        </div>

        {/* Contenido del artículo */}
        <article>
            <slot />
            {/* El contenido del artículo se insertará aquí */}
        </article>
    </section>
</BaseLayout>
```

## 3. Componentes

A continuación, veremos los diferentes componentes que he creado para mi blog con Astro. Cada componente tiene un rol específico en la estructura y funcionalidad del sitio.

### 3.1 CardPost.astro

El componente `CardPost.astro` se utiliza para mostrar un resumen de las publicaciones del blog. Cada tarjeta incluye un título, una imagen destacada y un breve resumen, lo que facilita la navegación por diferentes entradas del blog.

```astro
---
import { Picture } from "astro:assets";

const { title, url, date, readingTime, description, image, tags } = Astro.props;

// Creo un objeto Date con la fecha de publicacion pubDate que llega a traves de date para formatear la fecha en español
const formattedDate = new Date(date).toLocaleDateString("es-ES", {
    year: "numeric",
    month: "long",
    day: "numeric",
});
---

<article class="card">
    <header class="card-header">
        <h2 class="card-title">{title}</h2>
        <div class="card-meta">
            <p class="card-date">📅 {formattedDate}</p>
            <p class="card-reading-time">⏳ {readingTime}</p>
        </div>
        <figure class="card-image">
            <Picture
                src={image.url}
                alt={image.alt}
                format="avif"
                inferSize={true}
                widths={image.width}
                decoding="async"
                loading="lazy"
            />
        </figure>
    </header>
    <div class="tags">
        {
            tags.map((tag) => (
                <a
                    href={`/tags/${tag}`}
                    class="tag"
                    title={"Ver publicaciones con la etiqueta " + tag}
                    onclick="event.stopPropagation();"
                >
                    #{tag}
                </a>
            ))
        }
    </div>
    <p class="card-description">{description}</p>
    <footer class="card-footer">
        <a
            href={url}
            class="card-link"
            title="Leer el artículo completo"
            onclick="event.stopPropagation();">Leer más →</a
        >
    </footer>
</article>

<script>
    document.addEventListener("DOMContentLoaded", function () {
        // Selecciona todos los elementos con la clase "card"
        let articles = document.querySelectorAll(".card");

        // Recorre cada artículo y añade el evento de clic
        articles.forEach(function (article) {
            // Selecciona el elemento <a> con la clase "card-link" dentro del artículo actual
            let urlElement = article.querySelector(".card-link");

            // Verificar si el elemento .card-link existe y tiene un href válido
            if (urlElement && urlElement.hasAttribute("href")) {
                article.addEventListener("click", function () {
                    window.location.href = urlElement.getAttribute("href");
                });
            }
        });
    });
</script>

<style>
    .card {
        background-color: var(--background);
        border: 1px solid var(--box-shadow);
        border-radius: 12px;
        box-shadow: 0 6px 20px var(--box-shadow);
        overflow: hidden;
        transition:
            transform 0.3s ease,
            box-shadow 0.3s ease;
        padding: 1.5rem;
        color: var(--text-color);
    }

    .card:hover,
    .card:focus {
        cursor: pointer;
        transform: translateY(-8px);
        box-shadow: 0 10px 30px #24b8f2;
    }

    .card-header {
        margin-bottom: 1rem;
    }

    .card-title {
        font-size: 1.75rem;
        font-weight: 700;
        color: var(--text-h3);
        margin-bottom: 0.5rem;
    }

    .card-meta {
        font-size: 0.875rem;
        color: var(--text-color);
        display: flex;
        justify-content: space-between;
        gap: 1rem;
    }

    .card-image {
        margin: 1rem 0;
        border-radius: 12px;
        overflow: hidden;
    }

    img {
        width: 100%;
        height: auto;
        max-height: 420px;
        border-radius: 12px;
        object-fit: contain;
        background-color: rgba(128, 128, 128, 0.5);
    }

    .card-description {
        font-size: 1rem;
        line-height: 1.6;
        color: var(--text-p);
        margin-bottom: 1.5rem;
    }

    .card-footer {
        display: flex;
        justify-content: flex-end;
    }

    .card-link {
        font-size: 1rem;
        color: #007acc;
        text-decoration: none;
        font-weight: 700;
        transition: color 0.3s ease;
    }

    .card-link:hover,
    .card-link:focus {
        color: #005a99;
    }
</style>
```

### 3.2 Footer.astro

El componente `Footer.astro` maneja el pie de página del sitio, donde se incluyen los derechos de autor y enlaces a mis redes sociales.

```astro
<footer class="footer">
    <div class="nav">
        <a href="/">Inicio</a>
        <a href="/posts">Posts</a>
        <a href="/tags">Etiquetas</a>
    </div>
    <div class="buttons">
        <a href="https://www.linkedin.com/in/hugo-cayon-laso/" target="_blank">
            <span>
                <svg
                    height="16"
                    width="16"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <title>LinkedIn</title>
                    <path
                        fill="currentColor"
                        d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"
                    ></path>
                </svg>
            </span>
            LinkedIn
        </a>
        <a href="https://github.com/Hugocl01" target="_blank" class="github">
            <span>
                <svg
                    fill="#000000"
                    width="16"
                    height="16"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <title>GitHub</title>
                    <path
                        fill="currentColor"
                        d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"
                    ></path>
                </svg>
            </span>
            GitHub
        </a>
    </div>
    <div class="copyright">
        &copy; 2024 Hugo. Todos los derechos reservados.
    </div>
</footer>

<style>
    footer {
        color: var(--text-a);
        padding: 2rem;
        text-align: center;
        margin-top: 2.5rem;
    }

    footer .nav {
        margin-bottom: 2rem;
    }

    footer .nav a {
        color: var(--text-a);
        text-decoration: none;
        margin: 0 16px;
    }

    footer .buttons {
        margin-bottom: 2rem;
    }

    footer .buttons a{
        color: var(--text-a);
        display: inline-flex;
        align-items: center;
        justify-content: center;
        border: 1px solid var(--border-a);
        padding: 4px 8px;
        border-radius: 6px;
        transition: all 0.3s ease;
    }

    footer .buttons a:hover{
        color: var(--text-a-hover);
        background-color: var(--background-a-hover);
    }

    footer .buttons a span{
        margin-right: 4px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    footer .copyright {
        font-size: 1rem;
    }
</style>
```

### 3.3 Hamburger.astro

El componente `Hamburger.astro` añade un menú tipo "hamburguesa" que es especialmente útil para la navegación en dispositivos móviles. Este menú se despliega para mostrar enlaces a diferentes secciones del sitio cuando se hace clic en el ícono.

```astro
<div class="hamburger">
    <svg
        xmlns="http://www.w3.org/2000/svg"
        width="48"
        height="48"
        fill="#24b8f2"
        class="bi bi-list"
        viewBox="0 0 16 16"
    >
        <path
            fill-rule="evenodd"
            d="M2.5 12a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5m0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5m0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5"
        ></path>
    </svg>
</div>
```

### 3.4 Header.astro

El componente `Header.astro` se encarga de la cabecera del sitio, que incluye la barra de navegación principal y, en algunos casos, un logo o el menú hamburguesa en dispositivos móviles.

```astro
---
import Hamburger from "./Hamburger.astro";
import Navigation from "./Navigation.astro";
---

<header class="main-header">
    <nav>
        <Hamburger />
        <Navigation />
    </nav>
</header>
```

### 3.5 Navigation.astro

El componente `Navigation.astro` es una versión más completa de la navegación, que se puede utilizar para secciones específicas o para tener un control más detallado sobre los enlaces mostrados en el sitio.

```astro
<div class="nav-links">
    <a href="/">Inicio</a>
    <a href="/posts">Posts</a>
    <a href="/tags">Etiquetas</a>
</div>
```

### 3.6 ThemeChange.astro

El componente `ThemeChange.astro` permite a los usuarios cambiar entre el tema claro y el tema oscuro. Este componente mejora la accesibilidad y personalización del sitio, proporcionando una mejor experiencia de usuario.

```astro
<div class="theme-button-wrapper no-print">
    <label class="theme-button" for="checkbox">
        <input type="checkbox" id="checkbox" />
        <div class="button">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="currentColor"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="feather feather-sun"
            >
                <circle cx="12" cy="12" r="5"></circle>
                <line x1="12" y1="1" x2="12" y2="3"></line>
                <line x1="12" y1="21" x2="12" y2="23"></line>
                <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
                <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
                <line x1="1" y1="12" x2="3" y2="12"></line>
                <line x1="21" y1="12" x2="23" y2="12"></line>
                <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
                <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
            </svg>
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="currentColor"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="feather feather-moon"
            >
                <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"
                ></path>
            </svg>
        </div>
    </label>
</div>

<style>
    .theme-button-wrapper {
        position: fixed;
        bottom: 20px;
        right: 20px;
    }

    .theme-button {
        cursor: pointer;
        display: flex;
        align-items: center;
    }

    .button {
        width: 40px;
        height: 40px;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
        overflow: hidden; /* Para asegurar que el contenido no se salga del círculo */
        transition: all 0.3s ease;
    }

    /* Estilo del checkbox (puedes personalizarlo según tus necesidades) */
    #checkbox {
        display: none;
    }

    /* Estilo de los iconos dentro del botón */
    .theme-button svg {
        width: 20px; /* Ajusta el ancho del icono */
        height: 20px; /* Ajusta la altura del icono */
    }

    /* Estilo específico para el sol y la luna */
    .feather-sun,
    .feather-moon {
        display: none; /* Oculta los SVG por defecto */
    }

    /* Estilo específico para el sol */
    #checkbox:checked + .button .feather-sun {
        display: block; /* Muestra el sol cuando el checkbox está marcado */
    }

    #checkbox:checked + .button {
        border: 1px solid var(--border-a);
        color: var(--text-a);
    }

    #checkbox:checked + .button:hover {
        color: var(--text-a-hover);
        background-color: var(--background-a-hover);
    }

    /* Estilo específico para la luna */
    #checkbox:not(:checked) + .button .feather-moon {
        display: block; /* Muestra la luna cuando el checkbox no está marcado */
    }

    #checkbox:not(:checked) + .button {
        border: 1px solid var(--border-a);
        color: var(--text-a);
    }

    #checkbox:not(:checked) + .button:hover {
        color: var(--text-a-hover);
        background-color: var(--background-a-hover);
    }
</style>

<script>
    // Obtiene el elemento "body"
    const body = document.body;

    // Obtiene el elemento con el ID "checkbox" y aseguramos que sea un elemento de entrada (checkbox) utilizando la conversión "as HTMLInputElement"
    const checkbox = document.getElementById("checkbox") as HTMLInputElement;

    // Función para aplicar el tema según la preferencia del sistema
    function applySystemTheme() {
        const prefersDarkMode = window.matchMedia(
            "(prefers-color-scheme: dark)"
        ).matches;

        // Si no hay preferencia guardada, usa la preferencia del sistema
        if (!localStorage.getItem("theme")) {
            if (prefersDarkMode) {
                body.setAttribute("data-theme", "dark");
                checkbox.checked = true;
            } else {
                body.setAttribute("data-theme", "light");
                checkbox.checked = false;
            }
        }
    }

    // Función para aplicar el tema almacenado
    function applyStoredTheme() {
        const theme = localStorage.getItem("theme");

        if (theme) {
            body.setAttribute("data-theme", theme);
            checkbox.checked = theme === "dark";
        } else {
            applySystemTheme(); // Si no hay preferencia almacenada, aplica el tema del sistema
        }
    }

    // Llama a la función para aplicar el tema almacenado antes de que la página esté completamente cargada
    applyStoredTheme();

    // Agrega un escuchador de eventos "DOMContentLoaded" para el resto del código
    document.addEventListener("DOMContentLoaded", function () {
        // Agrega un escuchador de eventos "change" al elemento checkbox
        checkbox.addEventListener("change", function () {
            const newTheme = this.checked ? "dark" : "light";
            // Establece el atributo "data-theme" del elemento "body" y guarda la preferencia en localStorage
            body.setAttribute("data-theme", newTheme);
            localStorage.setItem("theme", newTheme);
        });
    });
</script>
```

¡Gracias por leer mi experiencia creando este blog con Astro! Espero que este recorrido te haya resultado útil y te inspire a crear tu propio sitio web. Si necesitas mas soporte, puedes visitar el [repositorio de GitHub](https://github.com/Hugocl01/Blog) con todo el codigo

Nos vemos en el próximo artículo, ¡hasta pronto!