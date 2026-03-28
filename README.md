# ◧ Calculadora de Retícula Editorial

**Herramienta pedagógica interactiva para el cálculo de retículas editoriales impresas**

Curso: Diagramación Editorial 
Docente: Mg. Mario Quiroz Martínez · 2026
Marca: d3magindesign

---

## Descripción

Aplicación web de una sola página (HTML, CSS y JavaScript puro, sin frameworks ni librerías externas) que permite calcular y visualizar en tiempo real la retícula editorial de cualquier formato de papel. Está diseñada como herramienta didáctica para estudiantes de diseño editorial, reproduciendo el mismo flujo de trabajo que se realiza en Adobe InDesign al configurar un documento profesional para impresión.

La calculadora traduce las decisiones tipográficas — cuerpo, interlineado, sistema de puntos — en una estructura modular visible: márgenes, columnas, medianiles, rejilla base y cuadrícula modular, todo renderizado proporcionalmente sobre un canvas HTML5.

---

## Objetivo pedagógico

Comprender el procedimiento matemático que subyace a toda retícula editorial profesional:

1. Definir el formato de papel (dimensiones en mm).
2. Establecer los cuatro márgenes (superior, inferior, interior, exterior).
3. Determinar el interlineado a partir del cuerpo tipográfico y un factor multiplicador.
4. Calcular cuántas líneas base enteras caben en el área de texto.
5. Ajustar el margen inferior sumando el sobrante, para que la rejilla base coincida exactamente con un número entero de líneas.
6. Dividir la mancha tipográfica en módulos (filas × columnas) con medianiles que sean múltiplos exactos del interlineado.

Este procedimiento es el mismo que se aplica en la práctica dirigida del curso al configurar documentos en InDesign con medidas tipográficas en picas y puntos.

---

## Funcionalidades

### Panel de controles

- **Formato de papel**: selector con ISO Serie A (A0–A5), ANSI/Imperial (Letter, Legal, Tabloid, Executive), JIS Serie B (B4–B6), formatos chinos K (8K, 16K, 32K) y opción de medidas personalizadas en milímetros.
- **Dimensiones**: campos de ancho y alto (mm) que se actualizan automáticamente al elegir un tamaño estándar, editables manualmente.
- **Márgenes**: superior (cabeza), inferior (pie), interior (lomo) y exterior (corte) en mm.
- **Sistema tipográfico**: selector entre anglosajón (PostScript/DTP) y Didot (francés), con conversión automática a milímetros.
- **Cuerpo e interlineado**: cuerpo en puntos y factor de interlineado (ej. 1.4) para calcular la rejilla base.
- **Columnas y módulos**: número de columnas, filas de módulos e intercampos (líneas base de separación entre módulos).
- **Criterio de coherencia**: los medianiles horizontal y vertical se derivan automáticamente del interlineado × intercampos, garantizando alineación con la rejilla base.

### Visualización en canvas

- Representación proporcional de la página completa, escalada automáticamente al área disponible.
- Seis capas activables/desactivables individualmente:
  - **Márgenes** (magenta de registro): sombreado sutil con etiquetas de medida en mm.
  - **Área de texto** (crema): la mancha tipográfica.
  - **Rejilla base** (cian): líneas horizontales equidistantes según el interlineado.
  - **Cuadrícula modular** (gris punteado): divisiones en filas y columnas de módulos.
  - **Medianil vertical** (verde): bandas entre columnas.
  - **Medianil horizontal** (amarillo/naranja): bandas entre filas de módulos.
- Marcas de registro (crop marks) decorativas en las esquinas.
- Indicador visual del sobrante cuando la rejilla no encaja exactamente.
- Controles de zoom (acercar, alejar, ajustar automáticamente).

### Cálculos y resultados

Todos los valores se muestran con sus unidades explícitas (mm y pt):

- Área de texto (ancho × alto) en mm y en puntos.
- Ancho de columna en mm y pt.
- Cuerpo tipográfico en pt y mm.
- Interlineado en pt y mm.
- Medianil (V = H) en mm, pt y número de líneas base.
- Total de líneas base ajustadas.
- Módulos (columnas × filas = total).
- Líneas por módulo (con indicación de sobrante si aplica).
- Alto y ancho de módulo en mm y pt.
- Equivalencia del punto según el sistema seleccionado.

### Ajuste de márgenes para rejilla exacta

Sección paso a paso que muestra el procedimiento de ajuste:

1. Cálculo del alto del área de texto.
2. Conversión del interlineado a mm.
3. División para obtener líneas enteras.
4. Cálculo del sobrante.
5. Suma del sobrante al margen inferior.
6. Botón para aplicar automáticamente el margen corregido.

### Tooltips educativos

Cada término técnico (formato, márgenes, cuerpo, interlineado, columnas, módulos, medianiles, intercampos, etc.) tiene una leyenda emergente al pasar el cursor que incluye:

- Definición del concepto.
- Equivalencia en Adobe InDesign (menú, panel o campo específico donde se configura).

### Equivalencias tipográficas

Panel desplegable con las tablas de referencia completas:

- **Sistema anglosajón**: 1 pt = 1/72" = 0.3528 mm · 1 pica = 12 pt = 4.2333 mm · 1" = 72 pt = 25.4 mm.
- **Sistema Didot**: 1 pt Didot ≈ 0.376 mm · 1 cícero = 12 pt Didot = 4.512 mm.
- Fórmulas de conversión entre mm, puntos anglosajones y puntos Didot.

---

## Constantes de conversión utilizadas

```
Punto anglosajón (PostScript/DTP):
  1 pt = 25.4 / 72 mm = 0.352778 mm
  1 pica = 12 pt = 4.23333 mm
  1 pulgada = 6 picas = 72 pt = 25.4 mm

Punto Didot (francés):
  1 pt Didot ≈ 0.376 mm
  1 cícero = 12 pt Didot ≈ 4.512 mm
```

---

## Fórmulas de cálculo

### Interlineado

```
interlineado (pt) = cuerpo (pt) × factor de interlineado
interlineado (mm) = interlineado (pt) × constante del sistema (mm/pt)
```

### Área de texto (mancha tipográfica)

```
ancho_texto = ancho_página − margen_interior − margen_exterior
alto_texto  = alto_página  − margen_superior − margen_inferior
```

### Líneas base

```
líneas_base = ⌊ alto_texto / interlineado (mm) ⌋
sobrante    = alto_texto − (líneas_base × interlineado)
```

### Ajuste de margen inferior

```
margen_inferior_ajustado = margen_inferior_original + sobrante
alto_texto_ajustado      = líneas_base × interlineado (mm)
```

### Medianil (criterio de coherencia)

```
medianil (mm) = interlineado (mm) × número_de_intercampos
```

### Módulos verticales (filas)

```
líneas_para_gutters = (filas − 1) × intercampos
líneas_para_módulos = líneas_base − líneas_para_gutters
líneas_por_módulo   = ⌊ líneas_para_módulos / filas ⌋
alto_módulo (mm)    = líneas_por_módulo × interlineado (mm)
```

### Ancho de columna

```
ancho_columna = (ancho_texto − (columnas − 1) × medianil) / columnas
```

---

## Equivalencia con Adobe InDesign

| Campo en la calculadora | Ubicación en InDesign |
|---|---|
| Formato (ancho × alto) | Archivo → Nuevo documento → Anchura / Altura |
| Márgenes (sup., inf., int., ext.) | Archivo → Nuevo documento → Márgenes, o Maquetación → Márgenes y columnas |
| Número de columnas | Maquetación → Márgenes y columnas → Número |
| Medianil de columnas | Maquetación → Márgenes y columnas → Medianil |
| Inicio de cuadrícula base | Preferencias → Cuadrículas → Cuadrícula base → Inicio |
| Incremento de cuadrícula base | Preferencias → Cuadrículas → Cuadrícula base → Incremento cada |
| Filas y columnas de módulos | Maquetación → Crear guías → Filas / Columnas |
| Medianil de filas/columnas (guías) | Maquetación → Crear guías → Medianil |
| Cuerpo tipográfico | Panel Carácter → Tamaño de fuente |
| Interlineado | Panel Carácter → Interlineado |
| Sistema de puntos | Preferencias → Unidades e incrementos → Puntos/Pica |

---

## Campos obligatorios

Los siguientes campos están marcados con asterisco rojo (*) y deben tener un valor válido para que el cálculo funcione correctamente:

| Campo | Unidad | Descripción |
|---|---|---|
| Sistema / Tamaño | — | Formato de papel o personalizado |
| Ancho | mm | Dimensión horizontal de la página |
| Alto | mm | Dimensión vertical de la página |
| Superior | mm | Margen de cabeza |
| Inferior | mm | Margen de pie (se ajusta para rejilla exacta) |
| Interior | mm | Margen de lomo |
| Exterior | mm | Margen de corte |
| Sistema de puntos | — | Anglosajón o Didot |
| Cuerpo | pt | Tamaño tipográfico |
| Factor interlineado | × | Multiplicador sobre el cuerpo |
| Columnas | cols | Divisiones verticales |
| Filas módulo | filas | Divisiones horizontales |
| Intercampos | lín. | Líneas base de separación entre módulos |

---

## Requisitos técnicos

- **Navegador**: cualquier navegador moderno (Chrome, Firefox, Safari, Edge) actualizado.
- **Dependencias externas**: ninguna librería JavaScript. Solo Google Fonts para tipografía (DM Sans, Syne, Crimson Pro, JetBrains Mono).
- **Servidor local**: no requiere. Se abre directamente como archivo HTML en el navegador.
- **Tecnologías**: HTML5, CSS3 (Grid, Flexbox, variables CSS, animaciones), JavaScript ES6+, Canvas API.

---

## Estructura del archivo

```
calculadora-reticula-v4.html    ← Archivo único autocontenido
```

Todo el código (HTML, CSS y JavaScript) está contenido en un solo archivo `.html` para facilitar su distribución, uso en aula y apertura directa en navegador sin servidor.

### Organización interna del código

- **CSS**: variables de color, tipografía y espaciado en `:root`; estilos organizados por sección (header, controles, tooltips, formularios, resultados, canvas, footer).
- **HTML**: estructura semántica con `<header>`, `<aside>` (controles), `<main>` (canvas), `<footer>`. Tooltips integrados inline dentro de elementos `.term`.
- **JavaScript**: IIFE autoejecutable con constantes de conversión documentadas, funciones de conversión (`ptToMM`, `mmToPt`), función principal `recalc()` que actualiza valores y canvas, y función `drawGrid()` para el renderizado en canvas con soporte HiDPI.

---

## Estilo visual

- **Concepto**: estética de «papel e impreso» — texturas de papel con ruido SVG inline, sombras que simulan una hoja sobre una mesa de trabajo, marcas de registro (crop marks) decorativas.
- **Paleta**: inspirada en la imprenta tradicional — negros y grises cálidos para tinta, acentos en colores CMYK de registro (cian, magenta, amarillo).
- **Tipografía**: Syne (titulares), DM Sans (cuerpo de texto), Crimson Pro (detalles editoriales), JetBrains Mono (valores numéricos y código).
- **Colores de retícula**: cada elemento tiene un color consistente y distinguible — magenta (márgenes), cian (rejilla base), gris (cuadrícula modular), verde (medianil vertical), amarillo (medianil horizontal).

---

## Uso en el aula

1. Abrir `calculadora-reticula-v4.html` en un navegador.
2. Seleccionar un formato de papel o ingresar medidas personalizadas.
3. Configurar los márgenes según el proyecto editorial.
4. Definir cuerpo tipográfico e interlineado.
5. Observar el procedimiento de ajuste de márgenes y presionar «Aplicar margen inferior corregido» si es necesario.
6. Configurar columnas, filas de módulos e intercampos.
7. Comparar los valores calculados con los que se configuran en InDesign.
8. Usar los tooltips (pasar el cursor sobre los términos subrayados) para consultar definiciones y su equivalencia en InDesign.
9. Activar/desactivar capas de visualización para estudiar cada componente de la retícula por separado.

---

## Historial de versiones

| Versión | Cambios principales |
|---|---|
| v1 | Calculadora funcional con controles manuales de medianiles, paleta sobria, leyenda de colores. |
| v2 | Criterio de coherencia: medianiles = rejilla base. Ajuste automático de margen inferior con procedimiento paso a paso. Estética «papel e impreso» con texturas, crop marks y paleta CMYK. |
| v3 | Introducción colapsable con propósito y objetivo pedagógico. Tooltips emergentes en todos los términos técnicos con definición + equivalencia en InDesign. Cambio de nombre del curso a «Diagramación Editorial». Campos obligatorios marcados con asterisco rojo. |
| v4 | Textos y números más grandes (base 16.5px). Unidades explícitas en todos los campos de entrada (mm, pt, ×, cols, filas, lín.) y en todos los valores de salida. Panel ampliado a 470px. Ancho de módulo añadido a resultados. |

---

## Licencia

Herramienta pedagógica desarrollada para uso académico en el curso de Diagramación Editorial . Año 2026.

**d3magindesign** · Mg. Mario Quiroz Martínez
