# Creación de un Sitio Web Estático con MkDocs y GitHub Pages

En esta práctica he aprendido a crear desde cero una página web estática para documentar proyectos de forma súper rápida y profesional. Lo mejor de todo es que el contenido se escribe en texto plano y, con un poco de magia de automatización, se publica solo en internet.

## Herramientas y Tecnologías Utilizadas

**Generación del Sitio y Contenido:**  
![MkDocs](https://img.shields.io/badge/MkDocs-526CFE?style=for-the-badge&logo=material-design&logoColor=white)
![Markdown](https://img.shields.io/badge/markdown-%23000000.svg?style=for-the-badge&logo=markdown&logoColor=white)
![YAML](https://img.shields.io/badge/yaml-%23ffffff.svg?style=for-the-badge&logo=yaml&logoColor=black)

**Entorno de Desarrollo:**  
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)


**Alojamiento y Automatización (CI/CD):**  
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/github%20pages-121013?style=for-the-badge&logo=github&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)


## Resumen de la Práctica

El objetivo ha sido olvidarnos de escribir HTML/CSS a mano y centrarnos en el contenido. La práctica se divide en tres grandes bloques:

### 1. Entorno de Desarrollo Local con Docker 🐳
Para no tener que instalar un montón de dependencias en el ordenador, utilicé un contenedor de Docker con la imagen `squidfunk/mkdocs-material`. Con esto pude:
* Iniciar el proyecto base (`mkdocs new`).
* Levantar un servidor local (`mkdocs serve`) en el puerto 8000 para ir viendo en tiempo real cómo quedaba la web mientras la editaba.
* Generar los archivos finales (`mkdocs build`).

![](images/practica-final%20IAW%20cap%203.png)


### 2. Creación del Contenido y Diseño
* **Markdown:** Todo el texto de la web (como la página de inicio o el "Acerca de") está escrito en archivos `.md` dentro de la carpeta `docs/`. Es súper cómodo y rápido.
* **Configuración:** Utilicé el archivo `mkdocs.yml` para definir el nombre del sitio, el menú de navegación y aplicar el tema **Material for MkDocs**, que le da un aspecto moderno y profesional.

### 3. Automatización Total con CI/CD (GitHub Actions)
Configuré un *workflow* (flujo de trabajo) en GitHub para que la web se publique sola. 
* Creé el archivo `.github/workflows/build-push-mkdocs.yaml`.
* Funciona así: cada vez que hago un `push` a la rama `main` con nuevo texto en Markdown, una máquina virtual de GitHub instala MkDocs, compila la web a HTML y sube el resultado final a una rama llamada `gh-pages`.
* Finalmente, activé **GitHub Pages** para que lea esa rama y publique la web en internet de forma gratuita. (No hay que olvidarse de darle permisos de escritura al *GITHUB_TOKEN* en los ajustes del repo).

> *Esto es lo que hemos mencionado de lo de la rama main y la rama pages, para que funcione correctamente tendremos que ir a github y poner la siguiente configuración*:

![](images/practica-final%20IAW%20cap%204.png)


> *Aquí podemos ver que el action de nuestro workflow funciona correctamente y sin fallos*

![](images/practica-final%20IAW%20cap%202.png)


> *Aquí aún faltan los retoqeus que le hemos dado, aún así se adjunta un video para que se puedan ver todas las funciones que tiene nuestra página estática*

![](images/practica-final%20IAW.png)


> *Por último quiero explicar un poco el archivo mkdocs y lo que hemos hecho mediante la visualización del código con comentarios*:

```bash

site_name: IAW - Implantación de Aplicaciones Web
site_description: Documentación y despliegue de prácticas del módulo
site_author: Edwin Javier Cueva Berenguer

# Estas dos lineas son para que en la parte de arriba podamos acceder directamente a la rama de github donde esta alojado todo el proyecto
repo_name: ejcb06/ejcb06.github.io
repo_url: https://github.com/EJCB06/EJCB06.github.io.git

theme:
  name: material
  language: es # Todo en español
  
  # Le ponemos un icono de consola de comandos arriba a la izquierda
  icon:
    logo: material/console
  
  # Configuración de colores: Modo oscuro estilo "Matrix/Hacker" y opción de modo claro
  palette:
    # 1. Modo oscuro (Slate)
    - scheme: slate
      primary: black
      accent: cyan # El cyan sobre negro queda espectacular
      toggle:
        icon: material/weather-night
        name: Cambiar a modo claro
    
    # 2. Modo claro (Por si alguien prefiere que no le quemen los ojos de día)
    - scheme: default
      primary: black
      accent: teal
      toggle:
        icon: material/weather-sunny
        name: Cambiar a modo oscuro

  # Funcionalidades extra del tema (pestañas, botón de volver arriba, etc.)
  features:
    - navigation.tabs # Pestañas arriba
    - navigation.tabs.sticky # Las pestañas te persiguen al hacer scroll
    - navigation.top # Botón de la flechita para volver arriba del todo
    - content.code.copy # ¡IMPORTANTÍSIMO! Botón de "Copiar" en los bloques de código

# Extensiones de Markdown para que el código y las notas se vean de locos
markdown_extensions:
  - admonition # Para poner cajitas de "Nota", "Peligro", "Info"
  - pymdownx.details # Para hacer cajitas desplegables
  - pymdownx.superfences # Necesario para que los bloques de código se rendericen perfectos
  - pymdownx.highlight: # Resaltado de sintaxis (colores en el código)
      anchor_linenums: true

# Menú de navegación con iconos para darle rollo
nav:
  - Principal: index.md
  - Prácticas:
      - Práctica 1: practica.md
      - Práctica 2: practica2.md
  - ℹ️ Acerca de: about.md

```