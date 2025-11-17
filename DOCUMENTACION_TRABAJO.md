# Documentación del trabajo

## 1. Datos del artículo

- Autor: (asumido) Equipo de investigación del sistema IOT agrícola (PDF proporcionado por el usuario)
- Año: (indeterminado) -- usar la fecha del PDF original
- Fuente: Documento/PDF suministrado por el usuario (maqueta e interfaz móvil)
- Enlace: (agregar enlace al artículo o PDF original aquí)

Nota: Asumí que el "artículo" es el PDF/screenshot que usaste para solicitar la recreación de la interfaz. Si tienes los metadatos exactos (autor, año, enlace), reemplaza las líneas anteriores.

**Aclaración importante:** El artículo/providencia original provista por el usuario describe la interfaz y los flujos de la aplicación móvil; no menciona arquitecturas distribuidas, microservicios ni detalles de backend. Cualquier referencia a microservicios en este documento es una propuesta opcional para evolución futura, no una característica extraída del artículo.

---

## 2. Tipo de diseño representado

Este trabajo implementa un prototipo de interfaz web responsive inspirado en una aplicación móvil de un sistema IOT agrícola. El tipo de diseño es:

- Diseño de interfaz de usuario (UI) y prototipo de experiencia (UX) para aplicación web.
- Arquitectura: SPA (aplicación de una sola página) basada en componentes (Vue 3 + Vite).
- Nivel de implementación: maqueta interactiva frontend-only (sin microservicios ni backend implementado).

---

## 3. Capturas / imágenes de la maqueta desarrollada

Incluye aquí capturas de pantalla generadas desde la aplicación en ejecución. Ejemplos de rutas/placeholder:

- `./screenshots/home.png` — Pantalla principal (Características)
- `./screenshots/soil-test.png` — Formulario de análisis de suelo (centrado)
- `./screenshots/market-release.png` — Historial de liberaciones y botón "View"
- `./screenshots/field-details.png` — Vista de detalles del campo

Nota: Actualmente los archivos de imagen son placeholders; añade las capturas reales exportadas desde el navegador en las rutas anteriores o reemplaza los enlaces.

Ejemplo de inserción de imagen en Markdown:

```
![Pantalla Principal](./screenshots/home.png)
```

---

## 4. Explicación — Cómo el diseño replica / interpreta el del artículo

El artículo/documento original presenta una aplicación móvil para gestión agrícola basada en IOT con las siguientes funcionalidades: creación de campos, registro de plantación, análisis de suelo, sugerencias de fertilizantes, seguimiento del ciclo cultivo/cosecha y liberación al mercado con generación de QR.

La réplica que he implementado interpreta y adapta esas funcionalidades así:

- Navegación y estructura: el original móvil contiene pantallas separadas; la réplica usa una SPA donde `App.vue` controla la vista activa (`currentView`) y muestra componentes por cada funcionalidad (Home, SoilTest, MarketRelease, FieldDetails). Esto imita el flujo de pantalla a pantalla del móvil.
- Interacciones: los formularios (Soil Test y Market Release) permiten crear entradas locales en memoria (arrays reactivos). En la app móvil estas acciones corresponderían a APIs; en la maqueta se simulan las operaciones para validar la UX.
- Historial y detalles: el historial de liberaciones (Market Release) incluye un botón "View" que emite un evento con el objeto seleccionado y lo pasa a `FieldDetailsView`, reproduciendo el flujo: historial → ver detalle. Esto corresponde exactamente al flujo descrito en las pantallas del artículo.
- Visual y estilo: se respetan jerarquías visuales (tarjetas para items, filas label/valor, fechas resaltadas) para mantener la legibilidad y la sensación de la app original.

Limitaciones y diferencias importantes:

- No se implementaron servicios ni persistencia remota; todos los datos son locales en memoria (reactive refs). En el artículo los datos probablemente vienen de sensores/servidores.
- El QR mostrado es un placeholder SVG. En producción se usaría una librería de generación de QR o un servicio.
- No hay rutas URL (vue-router) ni estado global (Pinia); la navegación está implementada manualmente con `currentView`.

Nota: reiteramos que el artículo original no describe microservicios ni una arquitectura de backend distribuido; las recomendaciones sobre APIs, Pinia o microservicios en este documento son propuestas de arquitectura para escalar la maqueta, no afirmaciones sobre el contenido del artículo.

---

## 5. Repositorio del código

El código fuente generado está en el repositorio local del workspace:

`/home/adre/storage/workspace/componente_desarrollo/agricultural-app`

Si deseas publicarlo en GitHub, puedes crear un repo y añadir la URL aquí. Ejemplo de comandos para publicar:

```bash
cd /home/adre/storage/workspace/componente_desarrollo/agricultural-app
git init
git add .
git commit -m "Initial UI prototype based on article"
# crea un repo en GitHub y añade el remoto, por ejemplo:
git remote add origin git@github.com:TU_USUARIO/REPO.git
git push -u origin main
```

---

## 6. Presentación (5 diapositivas - resumen)

### Diapositiva 1 — Título y contexto
- Título: Recreación de interfaz para sistema IOT agrícola
- Contexto breve: Maqueta web basada en un documento/screenshot provisto (funcionalidades: creación de campos, análisis de suelo, liberación al mercado).

### Diapositiva 2 — Objetivos del diseño
- Replicar la experiencia móvil en formato web
- Validar flujos: crear release, ver historial, ver detalle de campo
- Mantener diseño claro y responsivo

### Diapositiva 3 — Arquitectura y tecnologías
- SPA basada en componentes (Vue 3 + Vite)
- Estado local: refs reactivos para `releases` y `tests`
- Navegación: controlada por `currentView` y eventos `navigate`

### Diapositiva 4 — Mapeo entre artículo y maqueta
- Elemento del artículo → Implementación en la maqueta:
  - Historial de mercado → `MarketReleaseView` con lista y botón "View"
  - Detalle de campo → `FieldDetailsView` que recibe `selectedData`
  - Análisis de suelo → `SoilTestView` con formulario centrado

### Diapositiva 5 — Limitaciones y próximos pasos
- Falta persistencia y APIs (sugerido: añadir API + Pinia)
- Sugerencia: migrar a `vue-router` para deep links y mejor UX
- Generar QR real con librería `qrcode` y almacenar datos en backend

---

## 7. Instrucciones rápidas para ejecutar la maqueta

1. Instala dependencias e inicia el servidor de desarrollo:

```bash
cd /home/adre/storage/workspace/componente_desarrollo/agricultural-app
npm install
npm run dev
```

2. Abre la URL que muestre Vite (por defecto http://localhost:5173) y prueba las pantallas:
- Home → navegar a Market Release o Soil Test
- Market Release → crear release y hacer "View" para ver `FieldDetailsView`

---

## 8. Contacto / notas finales

Si quieres que genere el PPTX real (archivo .pptx) con estas 5 diapositivas o que publique el repositorio en GitHub, dilo y lo hago (para publicar necesitaré que me proporciones el enlace del repo o permiso para crear el remoto).

---

_Documento generado automáticamente a partir de la maqueta en el workspace. Reemplaza los placeholders de metadatos e imágenes según corresponda._
