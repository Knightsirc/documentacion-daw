# Informe de Práctica: Despliegue de Docusaurus en GitHub Pages

¡Hola! Aquí recojo de forma detallada cómo he llevado a cabo la práctica paso a paso, los problemas con los que me he ido encontrando (y cómo los he solucionado) y los enlaces clave para comprobar que todo funciona correctamente.

## 1. Enlaces y Accesos del Proyecto
* **Repositorio de GitHub:** [https://github.com/Knightsirc/documentacion-daw](https://github.com/Knightsirc/documentacion-daw)
* **Página web publicada (GitHub Pages):** `https://Knightsirc.github.io/documentacion-daw/`
* **Historial de Actions (Demostración de los builds):** [https://github.com/Knightsirc/documentacion-daw/actions](https://github.com/Knightsirc/documentacion-daw/actions)

---

## 2. Desarrollo paso a paso (Bitácora personal)

### Paso 1: Puesta en marcha en la Máquina Virtual
Me conecté a la máquina virtual de Ubuntu Server a través del puerto configurado por SSH (`ssh dawserver@localhost -p 2222`). Comprobé que Node.js y npm estuviesen bien instalados y actualizados a una versión reciente para evitar incompatibilidades con Docusaurus.

Creé la carpeta del proyecto e inicié Docusaurus utilizando TypeScript con los siguientes comandos:
```bash
mkdir actividad-docusaurus-github
cd actividad-docusaurus-github
npx create-docusaurus@latest documentacion classic-typescript
```

Para asegurarme de que todo iba rodando bien en local antes de subir nada, lancé el servidor de desarrollo mapeando el host:
```bash
cd documentacion
npm install
npm run start -- --host 0.0.0.0
```
Desde el navegador de mi equipo anfitrión pude entrar sin problemas a `http://localhost:3000` y ver la plantilla por defecto funcionando.

### Paso 2: Creación de la estructura de contenido
Para cumplir con los requisitos mínimos de la práctica, monté la estructura de carpetas dentro del directorio `docs/` abordando las fases típicas de un proyecto software:
* `docs/intro.md` (Punto de entrada general)
* `docs/análisis/requisitos.md` (Requisitos funcionales y no funcionales)
* `docs/diseño/diagrama_clases.md` (Diseño técnico y de clases)
* `docs/implementación/estructura_proyecto.md` (Organización del código)
* `docs/pruebas/analisis_caja_blanca.md` (Validación y pruebas lógicas)
* `docs/despliegue/github_pages.md` (Apuntes sobre el despliegue automático)

### Paso 3: Ajustes de configuración (`docusaurus.config.ts`)
Este fue uno de los puntos clave. Al desplegar en GitHub Pages bajo una ruta que no es la raíz pura del dominio (sino dentro de `/documentacion-daw/`), tuve que modificar el archivo de configuración de Docusaurus para que los estilos y enlaces no petaran con un error 404:
```typescript
url: 'https://Knightsirc.github.io',
baseUrl: '/documentacion-daw/',
```

### Paso 4: Automatización con GitHub Actions
Para no tener que compilar y subir los archivos estáticos a mano cada vez que cambiase algo, configuré el archivo de despliegue automático en `.github/workflows/deploy-pages.yml`. 

Este script se activa cada vez que hago un `push` a la rama `main`, descarga el código, instala las dependencias mediante `npm ci`, genera la compilación estática (`npm run build`) y lo sube directamente a las GitHub Pages del repositorio.

### Paso 5: Subida al repositorio y despliegue final
Por último, inicialicé Git en la carpeta local, enlacé el repositorio remoto y subí todo el contenido:
```bash
git init
git branch -M main
git add .
git commit -m "Estructura de documentación y configuración inicial completadas"
git remote add origin https://github.com/Knightsirc/documentacion-daw.git
git push -u origin main
```

Una vez hecho esto, entré en la pestaña **Settings > Pages** de mi repositorio en GitHub, seleccioné **GitHub Actions** como fuente de despliegue, y tras unos minutitos... ¡la web quedó online y funcionando a la primera!