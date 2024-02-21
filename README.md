# [Astro](https://astro.build) Blog

![Astro Badge](https://img.shields.io/badge/Astro-Build-blue?style=flat&logo=astro&logoColor=fff)
[![🚀 Deploy Workflow](https://github.com/JonathanRangelB/blog/actions/workflows/main.yml/badge.svg)](https://github.com/JonathanRangelB/blog/actions/workflows/main.yml)
[![FTP Badge](https://img.shields.io/badge/Website_deployed_for_free_with-FTP_deploy_action-2b9348?style=flat)](https://github.com/SamKirkland/FTP-Deploy-Action)
![GitHub Issues](https://img.shields.io/github/issues/jonathanrangelb/blog)
![GitHub Pull Requests](https://img.shields.io/github/issues-pr/jonathanrangelb/blog)
![GitHub forks](https://img.shields.io/github/forks/jonathanrangelb/blog?style=flat)
![GitHub Repo stars](https://img.shields.io/github/stars/jonathanrangelb/blog?style=flat)


![Screenshot](https://github.com/JonathanRangelB/blog/assets/3516336/ba5dc96b-deae-45b0-9f2a-8cc4b0db7c48)

## 🚀 Estructura del proyecto

Dentro de tu proyecto Astro, verás las siguientes carpetas y archivos:

```
/
├── public/
│   ├── robots.txt
│   └── favicon.ico
├── src/
│   ├── components/
│   │   └── Tour.astro
│   └── pages/
│       └── index.astro
└── package.json
```

Astro busca archivos `.astro` o `.md` en el directorio `src/pages/`. Cada página se expone como una ruta basada en su nombre de archivo.

No hay nada especial en `src/components/`, pero es donde se coloca cualquier componente Astro/React/Vue/Svelte/Preact.

Cualquier archivo estático, como imágenes, puede colocarse en el directorio `public/`.

## 🧞 Comandos

Todos los comandos se ejecutan desde la raíz del proyecto, desde la terminal:

| Command           | Action                                       |
| :---------------- | :------------------------------------------- |
| `npm install`     | Installs dependencies                        |
| `npm run dev`     | Starts local dev server at `localhost:3030`  |
| `npm run build`   | Build your production site to `./dist/`      |
| `npm run preview` | Preview your build locally, before deploying |

## Agradecimientos
Gracias al usuario [Charca](https://github.com/Charca) por crear [este gran template](https://github.com/Charca/astro-blog-template). Dejenle su merecida ⭐
