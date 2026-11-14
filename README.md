# Práctica CI/CD con GitHub Actions

**Instituto Tecnológico de Las Américas (ITLA)**  
**Asignatura:** Electiva 1 – Introducción a DevOps  
**Estudiante:** Kevin Francisco Fernández Ureña  
**Proyecto:** Implementación de un pipeline CI/CD para una aplicación web

## 1. Descripción del proyecto

Este proyecto consiste en una aplicación web sencilla para administrar una lista de tareas. Fue desarrollado utilizando Node.js y Express, con el objetivo de implementar un pipeline de integración continua y despliegue continuo (CI/CD) mediante GitHub Actions.

La aplicación permite agregar tareas, visualizar las tareas registradas y marcarlas como completadas. También se implementó una funcionalidad para eliminar tareas desde la API.

El proyecto utiliza pruebas automatizadas para comprobar las funcionalidades principales y GitHub Pages para publicar la interfaz web.

## 2. Tecnologías utilizadas

| Tecnología | Uso |
|---|---|
| HTML, CSS y JavaScript | Interfaz de usuario |
| Node.js | Entorno de ejecución |
| Express | API REST |
| Jest | Pruebas automatizadas |
| Supertest | Pruebas de integración de la API |
| Git y GitHub | Control de versiones |
| GitHub Actions | Automatización CI/CD |
| GitHub Pages | Publicación de la aplicación |
| Docker | Construcción de imagen |
| localStorage | Almacenamiento de tareas en GitHub Pages |

## 3. Funcionalidades

- Agregar tareas.
- Consultar las tareas registradas.
- Marcar tareas como completadas.
- Eliminar tareas mediante la API REST.
- Validar que no se creen tareas sin título.
- Consultar el estado de salud del servidor.
- Consultar métricas básicas de la aplicación.
- Conservar las tareas en GitHub Pages mediante localStorage.

## 4. Estructura del proyecto

```text
plantilla-devops-itla/
├── .github/
│   └── workflows/
│       └── ci.yml
├── public/
│   └── index.html
├── src/
│   ├── app.js
│   └── server.js
├── tests/
│   └── app.test.js
├── Dockerfile
├── .gitignore
├── package.json
├── package-lock.json
└── README.md
```

## 5. Instalación y ejecución

Es necesario tener instalado Node.js 20 o superior y Git.

Clonar el repositorio:

```bash
git clone https://github.com/Abalbuena00/practica-cicd-itla.git
```

Entrar en la carpeta:

```bash
cd practica-cicd-itla
```

Instalar las dependencias:

```bash
npm ci
```

Ejecutar la aplicación:

```bash
npm start
```

Abrir en el navegador:

http://localhost:3000

## 6. Pruebas automatizadas

El proyecto utiliza Jest y Supertest para verificar el funcionamiento de los endpoints.

Para ejecutar las pruebas:

```bash
npm test
```

Se implementaron ocho pruebas automatizadas:

1. Verificar la respuesta de `/health`.
2. Verificar la creación de tareas.
3. Validar títulos vacíos.
4. Comprobar la actualización del estado de una tarea.
5. Validar la respuesta ante tareas inexistentes al actualizar.
6. Consultar las métricas de la aplicación.
7. Comprobar la eliminación de una tarea.
8. Validar la eliminación de una tarea inexistente.

Las ocho pruebas se ejecutaron correctamente en el entorno local.

El comando `npm test` genera un reporte de cobertura de código en `coverage/lcov-report/index.html`.

## 7. Pipeline CI/CD

El pipeline se encuentra configurado en:

`.github/workflows/ci.yml`

Se ejecuta automáticamente cuando se realiza un `push` o un `pull request` hacia la rama `main`.

El proceso incluye las siguientes etapas:

**1. Descarga del código:** GitHub Actions obtiene la versión actual del repositorio.

**2. Configuración del entorno:** Se configura Node.js 20.

**3. Instalación de dependencias:** Se ejecuta `npm install`.

**4. Revisión estática:** Se ejecuta `npm run lint` para comprobar la sintaxis.

**5. Pruebas automatizadas:** Se ejecuta `npm test`, que también genera la cobertura.

**6. Construcción Docker:** Se construye una imagen de la aplicación.

**7. Despliegue:** Si los pasos anteriores se completan correctamente y el evento es un push a `main`, se publica el frontend en GitHub Pages.

## 8. Despliegue a GitHub Pages

Para habilitar el despliegue:

1. Entrar en el repositorio de GitHub.
2. Acceder a Settings.
3. Seleccionar Pages.
4. En Source, elegir GitHub Actions.
5. Subir los cambios a la rama main.
6. Verificar la ejecución en la pestaña Actions.

La versión publicada funciona de manera estática y utiliza localStorage para conservar las tareas dentro del navegador.

La API Express funciona cuando se ejecuta la aplicación mediante Node.js o Docker.

**URL del sitio:**  
https://Abalbuena00.github.io/practica-cicd-itla/

## 9. Resultados obtenidos

Se configuró un pipeline CI/CD capaz de automatizar la revisión del código, la ejecución de pruebas, la construcción de una imagen Docker y la publicación de la aplicación.

Se ejecutaron satisfactoriamente ocho pruebas y se confirmó que los dos trabajos del pipeline finalizaron correctamente en GitHub Actions.

También se comprobó que la versión publicada permite agregar tareas y conservarlas después de actualizar la página.

## 10. Conclusión

Esta práctica permitió comprender cómo funciona un proceso básico de integración continua y despliegue continuo.

La automatización de pruebas facilita la detección de errores antes de publicar cambios, mientras que GitHub Actions permite ejecutar el proceso sin intervención manual.

El uso de GitHub Pages permitió publicar una versión funcional de la aplicación y comprobar el resultado del despliegue.

El proyecto demuestra cómo pueden integrarse herramientas de desarrollo, pruebas, control de versiones y automatización en un mismo flujo de trabajo.