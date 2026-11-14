# Documentación del Pipeline CI/CD

## 1. Objetivo

El objetivo del pipeline es automatizar la validación, las pruebas y el despliegue de una aplicación web utilizando GitHub Actions.

El proceso permite comprobar la calidad básica del código antes de publicar una nueva versión de la aplicación.

## 2. Herramientas utilizadas

- GitHub Actions: automatización del pipeline.
- Node.js 20: entorno de ejecución.
- npm: administración de dependencias.
- Jest: ejecución de pruebas y generación de cobertura.
- Supertest: pruebas de los endpoints de la API.
- Docker: construcción de una imagen de la aplicación.
- GitHub Pages: publicación del frontend.

## 3. Archivo de configuración

El workflow se encuentra en:

`.github/workflows/ci.yml`

Este archivo define los eventos que activan el pipeline, los permisos necesarios y los trabajos de integración y despliegue.

## 4. Activación del pipeline

El pipeline se ejecuta automáticamente mediante dos eventos:

- **Push a main:** cuando se suben cambios a la rama principal.
- **Pull request hacia main:** cuando se solicita integrar cambios a la rama principal.

## 5. Etapas del pipeline

### Etapa 1. Obtener el código fuente

La acción `actions/checkout@v4` descarga el contenido del repositorio al entorno de GitHub Actions.

### Etapa 2. Configurar Node.js

La acción `actions/setup-node@v4` prepara Node.js 20 para ejecutar los comandos del proyecto.

### Etapa 3. Instalar dependencias

Se ejecuta:

```bash
npm install
```

Este comando instala las dependencias necesarias.

### Etapa 4. Revisión estática

Se ejecuta:

```bash
npm run lint
```

El script comprueba la sintaxis de los archivos JavaScript configurados en el proyecto.

### Etapa 5. Pruebas automatizadas

Se ejecuta:

```bash
npm test
```

Este comando utiliza Jest y Supertest para comprobar el comportamiento de la API y generar un reporte de cobertura.

El proyecto cuenta con ocho pruebas automatizadas que verifican la creación, actualización, eliminación y validación de tareas, además de los endpoints de salud y métricas.

### Etapa 6. Construcción de Docker

Se ejecuta el comando:

```bash
docker build -t plantilla-devops-itla:${{ github.sha }} .
```

El objetivo es comprobar que la aplicación puede construirse correctamente como una imagen de Docker.

Esta etapa no publica la imagen en un registro externo.

### Etapa 7. Despliegue a GitHub Pages

Una vez completado satisfactoriamente el trabajo `build-test`, GitHub Actions puede ejecutar `deploy-pages`.

El despliegue se realiza únicamente cuando el evento corresponde a un push a la rama `main`.

El workflow publica los archivos de la carpeta `public` mediante las acciones oficiales de GitHub Pages.

La versión publicada utiliza localStorage para guardar las tareas en el navegador, ya que GitHub Pages no ejecuta el backend Express.

## 6. Manejo de errores

Si falla un comando de instalación, revisión estática, pruebas o construcción de Docker, el trabajo `build-test` se marca como fallido.

Como `deploy-pages` depende de `build-test`, el despliegue de esa ejecución queda bloqueado.

Esto ayuda a evitar que una versión que no supera las validaciones se publique automáticamente.

## 7. Evidencia de ejecución

Se documentarán las siguientes situaciones:

- Pipeline exitoso con los trabajos en verde.
- Pipeline fallido por una prueba automatizada.
- Corrección de la prueba.
- Nueva ejecución exitosa del pipeline.
- Aplicación publicada en GitHub Pages.

## 8. Conclusión

La implementación de GitHub Actions permitió automatizar las verificaciones principales del proyecto.

El pipeline contribuye a detectar errores antes del despliegue y reduce la necesidad de ejecutar manualmente todas las comprobaciones después de cada modificación.

Esta práctica demuestra el funcionamiento básico de la integración continua y el despliegue continuo en un proyecto web.