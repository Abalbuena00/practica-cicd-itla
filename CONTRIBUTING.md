# Guía de contribución

## 1. Introducción

Este documento establece las recomendaciones para contribuir al proyecto de implementación de CI/CD con GitHub Actions.

El objetivo es mantener el código organizado, facilitar la colaboración y garantizar que los cambios sean revisados mediante pruebas automatizadas antes de integrarse en la rama principal.

## 2. Requisitos

Para trabajar en el proyecto es necesario contar con:

- Git instalado.
- Node.js versión 20 o superior.
- Visual Studio Code u otro editor de código.
- Una cuenta de GitHub.
- Conocimientos básicos de JavaScript.

## 3. Preparación del entorno

Clonar el repositorio:

```bash
git clone https://github.com/TU_USUARIO/practica-cicd-itla.git
```

Acceder a la carpeta:

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

La aplicación estará disponible en http://localhost:3000.

## 4. Creación de nuevas funcionalidades

Para implementar una modificación se recomienda crear una rama independiente:

```bash
git checkout -b feature/nueva-funcionalidad
```

Los cambios deben mantener la estructura del proyecto y seguir el estilo de código existente.

Toda funcionalidad nueva debe incluir las pruebas correspondientes cuando sea posible.

## 5. Ejecución de pruebas

Antes de subir un cambio deben ejecutarse:

```bash
npm run lint
npm test
```

El primer comando verifica la sintaxis del código JavaScript configurado.

El segundo ejecuta las pruebas automatizadas mediante Jest y genera el reporte de cobertura.

Los cambios no deben enviarse a revisión si las pruebas presentan errores sin resolver.

## 6. Registro de cambios

Una vez comprobado el funcionamiento del código:

```bash
git add .
git commit -m "Agregar nueva funcionalidad"
git push origin feature/nueva-funcionalidad
```

Los mensajes de los commits deben describir de manera clara los cambios realizados.

## 7. Pull requests

Para proponer una modificación:

1. Subir la rama al repositorio remoto.
2. Crear un Pull Request hacia `main`.
3. Describir los cambios realizados.
4. Comprobar que GitHub Actions ejecuta correctamente las validaciones.
5. Revisar y corregir los problemas identificados.
6. Integrar los cambios después de la aprobación correspondiente.

## 8. Integración continua

El proyecto utiliza GitHub Actions para realizar automáticamente las siguientes actividades:

- Instalar dependencias.
- Comprobar la sintaxis.
- Ejecutar pruebas automatizadas.
- Generar cobertura.
- Construir la imagen Docker.

El despliegue a GitHub Pages ocurre después de una ejecución correcta del pipeline asociada a un push a la rama `main`.

## 9. Buenas prácticas

- Mantener el código sencillo y legible.
- Utilizar nombres descriptivos para variables y funciones.
- Evitar subir la carpeta `node_modules`.
- No incluir contraseñas, tokens ni credenciales en el repositorio.
- Documentar los cambios importantes.
- Ejecutar las pruebas antes de realizar un push.
- Corregir los errores detectados por el pipeline.

## 10. Conclusión

La aplicación de estas recomendaciones permite mantener un flujo de desarrollo organizado, favorece la colaboración y ayuda a prevenir la integración de cambios que no cumplan con las validaciones automatizadas del proyecto.