# Despliegue en GitHub Pages

Este proyecto utiliza **GitHub Pages** para alojar la documentación técnica generada automáticamente a partir de esta carpeta `docs/`.

## Pasos para el Despliegue Automático

1. **Configuración del Repositorio:**
   * Ir a la pestaña **Settings** del repositorio en GitHub.
   * Seleccionar la sección **Pages** en el menú lateral izquierdo.
   * En la sección *Build and deployment*, configurar la fuente (**Source**) como **GitHub Actions**.

2. **Acción de Despliegue (`workflow`):**
   El archivo `.github/workflows/deploy-docs.yml` se encarga de compilar y desplegar los cambios cada vez que se hace un `git push` a la rama `main`:

```yaml
name: Deploy Documentation
on:
  push:
    branches: [ main ]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs
