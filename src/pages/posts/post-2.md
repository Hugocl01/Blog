---
layout: ../../layouts/MarkdownPostLayout.astro
title: Cómo creé mi blog con Astro
author: Hugo Cayón Laso
description: "Un recorrido detallado por el proceso de creación de mi blog utilizando Astro."
image:
    url: "https://docs.astro.build/assets/arc.webp"
    alt: "Miniatura de los arcos de Astro."
pubDate: 2024-08-12
readingTime: 5 min
tags: ["Astro", "Bloguear", "Desarrollo web"]
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

En este paso, creo los layouts, que son los componentes esenciales que definen la estructura general que rodea a todo el contenido de nuestra web. Decidí crear dos layouts: uno para toda la página, en el que están la etiqueta &lt;head&gt; con los &lt;meta&gt; y los &lt;link&gt;.


BaseLayout.astro

```astro
---
import Header from "../components/Header.astro";
import Footer from "../components/Footer.astro";
import "../styles/global.css";
import ThemeChange from "../components/ThemeChange.astro";
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
        <slot />
        <Footer />
        <ThemeChange />
        <script>
            import "../scripts/menu.js";
        </script>
    </body>
</html>
```

El siguiente layout lo uso para dar formato a cada post escrito en Markdown y este es envuelto por el anterior.

MarkdownPostLayout.astro

```astro
---
import BaseLayout from "./BaseLayout.astro"; // Importa el layout base para la página
import { Picture } from "astro:assets"; // Importa el componente Picture para manejar imágenes
const { frontmatter } = Astro.props; // Extrae las propiedades de frontmatter
---

<BaseLayout pageTitle={frontmatter.title}>

    {/* Encabezado del artículo */}
    <header>
        <h1>{frontmatter.title}</h1> {/* Título del artículo */}
        <p>{frontmatter.pubDate.toString().slice(0, 10)}</p> {/* Fecha de publicación */}
        <p>{frontmatter.readingTime}</p> {/* Tiempo estimado de lectura */}
        <p><em>{frontmatter.description}</em></p> {/* Descripción del artículo */}
        <p>Escrito por: {frontmatter.author}</p> {/* Autor del artículo */}
    </header>

    {/* Imagen destacada */}
    <section class="featured-image">
        <Picture
            src={frontmatter.image.url}
            alt={frontmatter.image.alt}
            format="avif"
            inferSize={true}
            widths={frontmatter.image.width}
            decoding="async"
            loading="lazy"
        />
    </section>

    {/* Contenido del artículo */}
    <article>
        <slot /> {/* El contenido del artículo se insertará aquí */}
    </article>

    {/* Etiquetas del artículo */}
    <footer>
        <div class="tags">
            {frontmatter.tags.map((tag) => (
                <a href={`/tags/${tag}`} class="tag">
                    #{tag}
                </a>
            ))}
        </div>
    </footer>
    
</BaseLayout>
```